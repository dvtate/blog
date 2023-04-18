# What's Wrong with WebAssembly? 2023.4.18

For those who don't know WebAssembly is a no longer new addition to web which allows you to get near native performance within the browser. It's a convenient compilation target and can Just-In-Time compile into whatever instruction set your machine uses.

After working at a company using webassembly for engineering simulations and spending the better parts of 2 years making a programming language that compiles to WebAssembly I've come to the realization that it's far from perfect and seems to be getting worse.

I'm probably going to upload something related to this to [my YouTube channel](https://youtube.com/dvtt) but I'll post the rough script here for now as motivation and update it later to include video links.

## \*.store operands wrong order
This one is kinda technical. So webassembly is designed to have stack-machine-like semantics which means that you write the operands before the operators.

```wast
;; function that adds two i32s together and adds 1 to the result
func $sum_plus_1 (params $a i32 $b i32) (result i32) 
	local.get $a
	local.get $b
	i32.add
	i32.const 1
	i32.add
	return
end
```

And this is actually an awesome thing! Although I'm slightly biased given that I've made several languages with similar semantics.

Anyways lets use an example to start to understand what I think is the problem.

`1 - 2 * 3` becomes `1 2 3 * -` and this seems fairly intuitive to me and you can do the same thing in webassembly

```wast
i32.const 1
i32.const 2
i32.const 3
i32.mul
i32.sub
```

but what happens when we try to assign it to a variable?

we can assign it to a `local` which is comparable to using a register in assembly using `local.set` which is pretty easy to use and makes sense.
```wat
i32.const 3
local.set $a
```

However storing it to a location in memory (for example - an array or object) is a bit different. 

```wat
...location in memory...
i32.const 3
i32.store
```

This works fine, why don't I like this? While at first glance it might seem intuitive to keep the order of operands that we use in infix, I found out the hard way that this isn't ideal.

`a = 1 + 2 * 3`     => `2 3 * 1 + a =`
									 or => `a 2 3 * 1 + =` ?

In a language I made in early 2019, I the same operand order for assignment and found that every time, I found it problematic for writing macros - I very often had to use a `swap` operator to get a value from the stack. Except webassembly does not have a swap operator.

```
# wasm ordering
$match_types (:
	dup $v2 swap = type $T swap = $v1 swap =
	v1 T cast v2 
) =
# vs.
(:
    dup $v2 = type $T = $v1 =
    v1 T cast v2
) $match_types =
```

Additionally because my most recent language uses a moving garbage collector, we can place an address onto the Webassembly stack but the operations required to compute the value that we want to store in it could invalidate that memory address and webassembly provides no efficient way to `swap` operands and no way to access or update pointers on the stack when we GC.

So to get around this I had to add extra locals to store the values in before writing them to memory... potentially incuring a performance hit because of the not ideal semantics.

These sematics might make sense in a language like C where the operations on the left side need to happen before those on the right, but I'd argue that it makes less sense in a postfix language and more importantly made my life more annoying.
```
int32_t* pn = malloc(8);
pn[0] = 1953789540;
*(pn + 1) = 1952804398;
printf("%s\n", pn);
```

## Things I'll probably mention in video
- No interface to the JS GC
- Manual memory management in JS
- No stack access
- Designed to be compilation target for langs not designed for it
- Resources for learning are pretty bad and dominated by propaganda and buzzwords
- What it gets used for vs what we hoped it would do
- WASM vs WASI different goals, different approaches
	- WASM soydevs who barely know JavaScript
	- WASI rust evangelists
- Soydevs in the CG probably going in bad directions
- limited DOM access
- WASM modules can be bigger than JS
