# Writing WebAssembly by Hand

In this video I'm going to give a quick intro to webassembly and and show my development process for writing it by hand. Last thing I made like this was a garbage collector for my programming langauge.

## BUT WAIT THIS IS USEFUL AND NOT THAT HARD

Normally people say "the compiler will almost always generate better code than you" and while this is generally true, WebAssembly is still somewhat new and quite different than other compilation targets. Many popular languages are micro-optimized for x86 and arm and the algorithms they use don't port over well to Webassembly. For example, they had to add memory operations because many compilers have algorithms for memcpy/memset/etc. that just don't translate well into WASM [1](https://github.com/WebAssembly/design/issues/977), [2](https://github.com/rust-lang/rust/issues/92436), [3](https://github.com/rust-lang/compiler-builtins/issues/339), [4](https://github.com/WebAssembly/binaryen/issues/4403). For comparison, in my code, I was able to use an implementation that had limitations but gives better performance.

can see there's a 
As you'll see the syntax isn't too scary, at least compared to other assembly languages.

## Basic Syntax
So we're going to be working with WebAssembly text format. 

Similar to x86, webassembly's text format has two syntaxis, however you can usually mix and match the two. The default syntax is similar to LISP with prefix notation and lots of parens.


```c
double square(double x) {
	return x * x;
}
```
```rust
fn square(x: f64) -> f64 {
	x * x
}
```

```wat
(func $square (param $x f64) (result f64)
	(f64.mul (local.get $x) (local.get $x)))
```

However the syntax is flexible so you can also remove the parens and use postfix syntax
```wat
(func $square (param $x f64) (result f64)
	local.get $x
	local.get $x
	f64.mul
)
```

For many people this might seem a bit backwards, this actually a design consideration of the language. It's a stack-machine, if you're familiar with FORTH this should be straight forward

```forth
:SQUARE DUP *;
```

```wat
func $square (param $x f64) (result f64)
	local.get $x ;; push x
	local.get $x ;; push x
	f64.mul      ;; take two values from the stack, push product
	return       ;; not actually needed but it
end
```

## Editing
For mass appeal I'm using vscode with an extension that add syntax highlighting for webassembly [link](https://marketplace.visualstudio.com/items?itemName=dtsvet.vscode-wasm). But you can use any text editor and I know that emacs and vim both work great.

Webassembly text files use the extension [wat](https://www.destroyallsoftware.com/talks/wat). Yes, wat, like the famous Gary Bernhardt screencast that you should definitely watch after this.

*fast forward*
> make new project from new folder
> make new file : demo.wat

All webassembly programs are modules, so this is the simplest webassembly program you can make. Let's convert this to a binary
```wat
(module)
```

## Building

To do this we're going to use the [webassembly binary toolkit](https://github.com/webassembly/wabt).  Which has a number of tools but the two that matter to us are `wat2wasm` which converts our webassembly text to binary format. And `wasm2wat` which does the opposite. Both are super straightforward to use.

Building is simple. The generated file is 8 bytes, \<rant>which seems like a lot considering it does nothing but really when you think about it if we actually tried to use this it would still have to validate the module and then if they add new features it has to maintain backward compatibity... \</rant> ... but anyways .... we did it!
```console
$ wat2wasm demo.wat -o demo.wasm
$ xxd demo.wasm
00000000: 0061 736d 0100 0000                      .asm....
$ wasm2wat demo.wasm
(module)
```

## Using it in the browser
I probably should have started with this but what makes webassembly so powerful is that it can run in the browser with near native performance. So lets see how to do that before moving on to a more fun demo.

## Optimizer
Unlike most assembly languages, WebAssembly has some pretty powerful tools for optimizing binaries. I was playing around with doing some manual optimization techniques, and decided to pass the whole thing through binaryen's wasm-opt and it was smart enough to
1. find an optimization that I missed
2. recognize that the version of the optimized and unoptimized functions were the same and combine them

We can add in the code from before
```wat
(module
	(func $square (param $x f64) (result f64)
		local.get $x
		local.get $x
		f64.mul
	)
)
```

