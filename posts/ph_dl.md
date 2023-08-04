# Postfix Haskell Devlog
Here is a development timeline for the programming language I worked on 2020-2023.

## 2020.10.7 - Idea and PoC
This is a POC for first ~1/3 of compiler for new language I'm working on... This demo is just a shell for part of compiler that handles:
- Lexing
- Parsing (weird bc lang is postfix)
- Some optimizations
- Majority of type-checking and validation

![image](https://user-images.githubusercontent.com/15305612/257604440-cd948b2a-4cdd-459f-b945-f500d59ad473.png)

## 2020.10.19 - Types Prose
I wrote some prose while planning out the type system. This example is smilar to using named-tuple in Python but methods/getters are defined as overloaded operators.

![image](https://user-images.githubusercontent.com/15305612/257605649-432f6d53-c497-463f-b049-660a98471f85.png)

(typo: should be seq .value and seq .count, not $seq )

Here's a more complex example with 'inheritance'/parametric types. Not sure if everything here is doable, but definitely a goal. Also i don't like having to do \_t suffix... feel like there should be a way to do it as prefix instead, maybe capital letters?

![image](https://user-images.githubusercontent.com/15305612/257606109-0e2d5ada-ba0a-4e81-9e12-bfcf21b72e4d.png)

Forgetting to escape/unescape identifiers is going to be a running theme for me with this language. It's too similar to my previous language -- [YodaScript](https://github.com/dvtate/yodascript) which almost always uses escaped identifiers. Line 25 should be $sequence_t.


## 2020.11.9 - More Types Prose
I made some changes to my thinking for the typesystem. I know that I've definitely added some complexity but I think this design improves the consistency and adds some more useful tools instead of having types feeling out of place.

![image](https://user-images.githubusercontent.com/15305612/257606982-db74ce01-ac71-48ee-a905-4d6f55c69b82.png)
![image](https://user-images.githubusercontent.com/15305612/257607021-ab70f0a5-ffdc-42ab-9da5-b03b6526903e.png)
So I guess there are two distinct concepts

Types: Let us a way to check what data is/can be held by the value
Classes: let us distinguish data of the same type but associated with a different purpose/functionality

So with this in mind, classes would be replaced with 'traits' which would just be numerical flags that you can add to a value to assign functionality implemented by checking to see if the argument has the given 'trait'. Some downsides but simplifies language a bit

So here's what that would look like, although I think this gives the user a more power and does a better job of exposing what's actually going on, there's some lost safety and way more boilerplate code so probably going to use plan from first post in thread

![image](https://user-images.githubusercontent.com/15305612/257607161-b27fd2ab-9f85-4bf5-9514-1779a217a441.png)

## 2020.11.16 - TypeSystem Prototype
I made a demo over the weekend which adds types to the language.

![image](https://user-images.githubusercontent.com/15305612/257607635-f37ec0b2-c8fc-46c8-9d09-4c645f9a009c.png)

## 2020.11.22 - More TypeSystem Implementation
Most of original plan implemented. 

![image](https://user-images.githubusercontent.com/15305612/257608617-a5c5700c-2393-47fa-9ea5-54b97071325e.png)

## 2020.11.30 - Starting on Standard library
Logical provided by standard library. To clarify, the compiler does provide logic out of the box but the operators are user-level. Also again, sorry the language isn't easy to read... really picked the worst of both worlds for that by making it stack-based and functional in addition of the other weird stuff
![image](https://user-images.githubusercontent.com/15305612/257608974-93044a5d-9963-42a9-b983-6ea5c8ff6ff7.png)
![image](https://user-images.githubusercontent.com/15305612/257618458-b9a94634-ba1e-45d9-91a0-6859951c907f.png)

## 2020.12.8 - VSCode Syntax Highlighting Plugin
![image](https://user-images.githubusercontent.com/15305612/257618606-a70970a8-92e6-4332-a68f-69e6b18c0008.png)

## 2020.12.13 - TypeSystem Demo
![image](https://user-images.githubusercontent.com/15305612/257618795-7a2a2fc5-3078-4f06-b2f0-bec7e6649cf5.png)
![image](https://user-images.githubusercontent.com/15305612/257618824-f1a9f36f-fb74-4ec7-b74f-0e67a31145ae.png)

## 2020.12.7 - Recursion
Recursion was a big painpoint... I came up with a way to implement it while taking a university exam but implementation was not so straightforward.
![image](https://user-images.githubusercontent.com/15305612/257621017-4af4010c-2f64-46d1-9275-af9252e22652.png)
![image](https://user-images.githubusercontent.com/15305612/257621077-81700240-8932-4e8e-ada6-ddfbc71f92a7.png)

## 2020.12.22 - Terrible Namespace Prose
![image](https://user-images.githubusercontent.com/15305612/257621366-ac6bc6cb-2f1b-4d4d-bd17-0a2dc75a335b.png)
![image](https://user-images.githubusercontent.com/15305612/257621391-6b3e6ce9-5c69-49d8-bf93-99a3b58551a9.png)

## 2020.12.28 - Copiling to WebAssembly
![image](https://user-images.githubusercontent.com/15305612/257621503-c4ded600-cb57-422b-9362-2a3626bf7c3a.png)
![image](https://user-images.githubusercontent.com/15305612/257621593-d8ee09cf-0224-45df-9ffa-05e6404d3c68.png)

## 2021.1.25 - Using binaryen to clean up WebAssembly
![image](https://user-images.githubusercontent.com/15305612/257621808-aa886b10-3d41-47ba-8770-e1793681e3a1.png)

## 2021.1.29 - Inline PH within JS/TS
The following demo shows the language getting used within a javascript program. It compiles a webassembly module from the PH code given in a string template literal.

![image](https://user-images.githubusercontent.com/15305612/257622270-c38f5365-9260-4c66-a010-58769578b610.png)

Using short circuit logic without good optimizations led to some ugly WebAssembly being generated.

![image](https://user-images.githubusercontent.com/15305612/257623066-89ae2f2a-260c-4877-a0d5-36f89a98c066.png)

## 2021.2.7 - Binaryen optimizer

![image](https://user-images.githubusercontent.com/15305612/257623386-ba5ca06d-fc06-4e20-ae19-8ebcfa1df4a7.png)

## 2021.3.13 - RECURSION
Recursion type inference algorithm:
1. try to compile function as if non-recursive
2. detect it's recursive, throw and start over
3. trace to infer func type
4. trace again, handling bindings for recursive call

and because there are no type annotations, we cannot recycle the inferred types. So every single recursive function invocation requires 3 attempts to compile it in order to determine all the context-sensitive datatypes and stuff

ocaml has a "rec" specifier for functions, if I were to adopt something this it would have made things slightly better (only 2 traces and less complexity), but I've already kinda done it the hard way so I prob should just finish it as is without doing weird stuff with syntax

![image](https://user-images.githubusercontent.com/15305612/257623782-486540fb-a3f2-41bb-8fb2-e06653457618.png)
![image](https://user-images.githubusercontent.com/15305612/257623810-4dc294e0-a271-4cae-9285-7db5256e6ca7.png)

This only supported tail recursion.

## 2021.5.2 - String Literals
Some thinking was done to plan out the optimal way to pack the data for string literals into linear memory in order to reduce duplication. Strings are implemented as a pointer + an length as opposed to being null-terminated like in C.

![image](https://user-images.githubusercontent.com/15305612/257625532-2c98927a-f308-46a4-bfb3-b821d96bac77.png)
![image](https://user-images.githubusercontent.com/15305612/257625556-29c4e51d-37c7-41ff-8a5a-47dbbd012ee2.png)

## 2021.5.5 - Host environment bindings
![image](https://user-images.githubusercontent.com/15305612/257627129-d8a2948a-1dc8-4b75-88fc-9a00451bff85.png)

## 2021.5.7 - Hello World demo
![image](https://user-images.githubusercontent.com/15305612/257627262-1331fb32-ebbf-40c9-a8c7-6452d6c924ff.png)

## 2021.5.9 - Fizzbuzz demo
![image](https://user-images.githubusercontent.com/15305612/257627461-6b35bcc8-a843-417e-b30d-76158576f741.png)
![image](https://user-images.githubusercontent.com/15305612/257627487-80180da7-59ba-47af-a1e9-e3213db28ef6.png)

Removed bug workaround:

![image](https://user-images.githubusercontent.com/15305612/257627543-62fa2c32-e736-432a-aacb-6ab4971973a2.png)

## 2021.7 - Namespaces, modules
![image](https://user-images.githubusercontent.com/15305612/257627724-8e07b384-f96d-4624-a172-813fb410d63e.png)
I added namespaces. Plan is to make the `import` keyword return a namespace macro. So unfortunately this ugly syntax is probably gonna get used a lot

- use: promotes everything within namespace
- use_some: `use` all that match first regex except those that match second
- include: load a file as a namespace (later changed to require)
- rec: actually does stuff now and compiler trusts it (img 3 is when forgotten) :D

Images: demo mostly related

![image](https://user-images.githubusercontent.com/15305612/257628048-7c37b4ed-29d4-4177-8172-4ba39ce7de32.png)
![image](https://user-images.githubusercontent.com/15305612/257628070-e25e8e84-9b35-4041-bfdc-a24152a845db.png)
![image](https://user-images.githubusercontent.com/15305612/257628097-851fed54-961f-493b-9425-c285a1104344.png)
![image](https://user-images.githubusercontent.com/15305612/257628148-f6cea6d1-6591-412c-bd3b-dd0df9f0571d.png)

## 2021.7.22 - Polymorphic JS imports
![image](https://user-images.githubusercontent.com/15305612/257628316-af0b82cf-d5e6-4115-acaf-6e27a75ca264.png)
![image](https://user-images.githubusercontent.com/15305612/257628337-15625a90-2ac4-4bcd-b762-8e839682b446.png)

## 2021.8.26 - Non-TCO recursion
Support was added for non-tail-recursive macro recursion

![image](https://user-images.githubusercontent.com/15305612/257628627-2a6f3fdf-aae8-4393-9119-70e1e0f5c0bc.png)

So I haven't posted on lang here in a while. Previously it only supported tail-recursive functions but that's obviously pretty useless so I reverted that and now it only sometimes does TCO. It works by moving the recursive parts into helper functions.

![gnome-shell-screenshot-0X8N80](https://user-images.githubusercontent.com/15305612/257628750-cee6e845-85b6-45e2-bf63-11189e49c5eb.png)

Image 1: Notice that the compiler passes lexically scoped variables to the recursive helper function as parameters so that they stay in scope

![gnome-shell-screenshot-M7HO80](https://user-images.githubusercontent.com/15305612/257628771-47daf0c9-5bf5-4611-9d62-c2a807d8b658.png)

Image 2: it now recognizes and evaluates recursive functions where all the arguments are constants at compile time. Also a more realistic example without using binaryen's optimizer which removes some excess variables

How it works:
1. it moves relevant lexically scoped variables/parameters to parameters of the helper function (bad memory scaling but probably best option)
2. Compiler recognizes and evaluates recursive constant expressions at compile time

I also added the `defer` keyword to get around the constant propagation of part 2 in previous post in case someone was doing a really big calculation or something and intentionally wanted it to happen at runtime with the faster speeds of WASM... kinda niche.

![image](https://user-images.githubusercontent.com/15305612/257628952-473f535b-e0c7-4457-95f2-fc581ca441f1.png)
![image](https://user-images.githubusercontent.com/15305612/257628977-3c3cdbd7-8983-4a1d-b3f5-cccc9f213799.png)

## 2021.9.7 - Moving Features to Standard Library using Inline Assembly
I moved a bunch of internal compiler features to the standard library by adding tools for inline assembly. 

![image](https://user-images.githubusercontent.com/15305612/257629458-9acf1bf4-1b81-407f-b1bc-6f59e4d013f7.png)
![image](https://user-images.githubusercontent.com/15305612/257629518-7ed2d952-4063-4597-bc44-c978216f1472.png)

Unfortunately these changes dramatically increased compile-time. I managed to determine that most of the problem was caused by the == operator which was overloaded to operate on a variety of datatypes as well as types themselves... This polymorphic behavior resulted in slower builds. Also writing the compiler in TypeScript/JS doesn't help.

## 2021.9.13 - Hacking direct memory access
Directly reading from and writing to linear memory isn't usually considered best practice by functional programmers but I wanted to make some demos where this would be useful.

![image](https://user-images.githubusercontent.com/15305612/257630062-cbff5651-4478-403c-869b-dfd227126840.png)

## 2021.9.16 - Custom Compiler Macros
So I wanted a really niche compiler macro that gave me some relevant data for debugging so I just added one which runs provided js code using eval().

![image](https://user-images.githubusercontent.com/15305612/257630518-ae7a3ed5-3e9a-41d2-b415-90e63364caf0.png)

## 2021.9.23 - Using direct memory access to make art
![image](https://user-images.githubusercontent.com/15305612/257630676-568eb0f9-87ba-4c5f-986e-0d870adbb2b2.png)
![image](https://user-images.githubusercontent.com/15305612/257630699-f867765e-596b-460b-95f9-2dad991869e3.png)
![image](https://user-images.githubusercontent.com/15305612/257630713-a17647ba-b7ed-49da-b9a2-624eeca2041d.png)
![image](https://user-images.githubusercontent.com/15305612/257630742-53d6d8ed-b80d-4c1c-aafb-208c21f81269.png)
![image](https://user-images.githubusercontent.com/15305612/257630779-9c9efde6-a34c-4659-9981-aab0c6c76de0.png)
![image](https://user-images.githubusercontent.com/15305612/257630801-a62ac535-890a-4f79-85a4-8a7388208c3b.png)

## 2021.9.17 - Breakout/single player pong - https://github.com/dvtate/breakout
![Screenshot from 2023-08-01 15-20-30](https://user-images.githubusercontent.com/15305612/257632027-dd78a73d-d4aa-41db-ab2c-1881c2bef3ee.png)

## 2021.10.2 - Flappy bird clone demo - https://github.com/dvtate/phlappy-bird
![image](https://user-images.githubusercontent.com/15305612/257631521-7462f2c2-4933-45a9-b2b0-38e2e0410643.png)
![image](https://user-images.githubusercontent.com/15305612/257632469-2b4615b3-b822-4f36-830d-c15f9d8b446b.png)
![image](https://user-images.githubusercontent.com/15305612/257632495-6ced0402-ed71-491a-84a7-633847e0ff89.png)

- https://www.youtube.com/shorts/cjX_qp3xuYo

## 2021.10.14 - Significant Syntax Change Planning
Planning a major syntax change in order to accomodate type signatures.

![image](https://user-images.githubusercontent.com/15305612/257633210-0f92dbff-942d-4eb7-ac45-3527e3aa7013.png)

One issue is that not all values in the language have a type for example, `type(I32)` is undefined but it's convenient being able to pass these to macros for metaprogramming (and standard library relies on this). Also only way to give case/fun types is w/ wrappers (ie - `(()(I32): act )`).

Another example which actually shows how it can reduce boilerplate and even eliminate some of the usage of the metaprogramming features described above

![image](https://user-images.githubusercontent.com/15305612/257634848-2f072f15-b221-4492-bc0b-36cf126cdda2.png)

## 2021.10.18 - Identified source of slow compile time
(syntactic sugar for multiple assignment was the culprit)

## 2021.10.19 - Added dedicated tuple syntax (...) 
This replaced the older `pack` operator

![image](https://user-images.githubusercontent.com/15305612/257635347-bfd33e0a-e6d4-46f9-8158-c5db44f96620.png)

## 2021.10.19 - Improving Compile Times
Plan is to improve compile-times (by making identifiers not capture their scope) but will have to refactor how namespaces and modules work (pretty sure I was drunk when I designed the first one) but anyway I think it should be better

Plan:
Before -> After

![image](https://user-images.githubusercontent.com/15305612/257635610-ef125b07-3410-434b-858b-15cc5ec83914.png)
![image](https://user-images.githubusercontent.com/15305612/257635633-67295aa0-971e-4b49-800e-1ffb2418d539.png)

To clarify what I'm changing

```
10 $a =
5  { $a = { $a a } } @ @
# a - both say 5
:data
# $a - live: 5, with changes: 10
unescape :data
```

For whatever reason I thought that it would be intuitive to make escaped ids use the scope they were made in... but it's espensive and not useful

Added some syntactic sugar and a bunch of breaking changes. Also managed to reduce compile time by around 60%. I'm now updating all my demos so that they work again

![image](https://user-images.githubusercontent.com/15305612/257635825-e87b565f-638c-48a1-858c-81fa463bde72.png)

## 2021.10.23 - Syntax Change done
I've just finished implementing the syntax change and updating the standard library and most of my demos. Compile time somehow decreased by half again (so now it's ~80% faster than before syntax change).

![image](https://user-images.githubusercontent.com/15305612/257636067-f7b55f6a-8ead-40a1-bc3c-725cd0c7183b.png)
![image](https://user-images.githubusercontent.com/15305612/257636093-3854a359-cf26-456f-a97a-a125b58a20c0.png)

## 2021.11.8 - GC
> So I guess it's time for me to start moving towards a GC... sigh, this brings me so much pain to do... Currently the language is limited such that there's no need to have a GC (ie - everything statically allocated), but that's gonnna have to change it seems :/
> Idk, just not super happy with this... Even tho it's basically just a more explicit version of what haskell does
> 
> Currently trying to think about all the different things I'm gonna need to store on the heap since planning out implementation for a moving GC was hurting my head

![image](https://user-images.githubusercontent.com/15305612/257637066-63ab0a1b-ae09-4c21-b887-d714d0966770.png)

The issue with doing a moving GC in WASM is that part of the process is updating all the references to the objects stored in the nursery but WASM doesn't let you access values currently on the stack so the only real solution is to use a separate stack for refs or custom virt  mem

Ok so I'm choosing to do the 'separate stack' approach. I now have like 75% of a plan for how to implement the runtime for the GC

I think there's enough work involved with implementing all the associated features that the compiler could double in size
https://github.com/dvtate/postfix-haskell/blob/master/planning/implementation/lm.md

Wrote the GC runtime in WASM by hand (see link) now I just have to test it and then I'll have to figure out how to implement recursive types
https://github.com/dvtate/postfix-haskell/blob/master/lib/rt.wat

Everything's working :D

Some general categories of bugs encountered:
- endianness
- forgetting to * sizeof(i32)
- doing math for i64 instead of i32
- forgettting to i32.load
- general typos
- etc.

![image](https://user-images.githubusercontent.com/15305612/257637450-4cabb1ce-c876-462d-a780-4fca8c625603.png)
![image](https://user-images.githubusercontent.com/15305612/257637472-62976f40-31b0-4ee2-8b41-8df265b0dbf9.png)

## 2021.12.13 - Mechanization
I wrote a paper regarding this language for a class on programming language theory. 
https://github.com/dvtate/PLT-coursework/blob/master/project/CS595_final_project.pdf

## 2022.6.20 - Compile-time only types
The type-system is now expanded with types for the compile-time only constructs in image 2 albiet with limited contexts

With these changes I've removed 3 keywords and improved compile-time ~30%

![image](https://user-images.githubusercontent.com/15305612/257641685-8f47ac07-b82c-4cd4-b154-f5906bac5b14.png)
![image](https://user-images.githubusercontent.com/15305612/257641710-3fcc1a57-c716-4121-88a6-2607ff370e57.png)

## 2022.6.22 - Pretty printing type
Minor quality of life improvement for debugging types and stuff
![image](https://user-images.githubusercontent.com/15305612/257642121-ba46d341-4e4c-4e30-a3ed-b0c83f1562c9.png)

## 2022.6.23 - Enums 
Working on enums now, using the rust version of the word since it's shorter than the more accurate "tagged-union" and the language already uses a lot of words incorrectly altho maybe will rename them to "variant" eventually.

The code on lines 17-26 is hard so for now I'm just adding `match` operator.

![image](https://user-images.githubusercontent.com/15305612/257642259-f28c527d-e634-4bbd-98b9-0caf08714cfd.png)

### 2022.6.25 - Big refactor
There are 3 parts to this:
- Convert Source to IR (ie: type system): not done but also not problematic
- Convert IR to WASM: Wow this is gonna have to be a pretty major refactor wtf
- Runtime (ie: GC): mostly planned, tested, and documented 

![image](https://user-images.githubusercontent.com/15305612/257642573-3d9bfbf7-a28e-400e-8c7c-1bc84d384c8c.png)

### 2022.6.26 - Thinking about improved memory usage
This change would eliminate the system with two deteached stacks at the cost of some increased compiler complexity and potentially minor performance hits. It would definitely be more intutive at least and probably better memory efficiency.

![image](https://user-images.githubusercontent.com/15305612/257643163-c86746ff-2661-4df8-893e-533d513ac482.png)

### 2022.6.26 - Fixed-point combinator macro/type syntax
> Thinking about making this syntax change. It would allow recursion without binding to an identifier makes it easier to parse recursive enum types and improve compile time. 
> Currently for classes and enums it generates the type every time it gets used. So lots of room for improvement.

![image](https://user-images.githubusercontent.com/15305612/257643315-0ae6aa75-f68a-4efe-8c5f-2b3f72aacecd.png)

### 2022.7.19 - Enums Demo
Made a better demo and by that I of course mean I stole the idea from Haskell's understanding monads wikibook (image 1).

Also went on a bit of a tangent implementing math functions in the standard library (images 2-4).

![image](https://user-images.githubusercontent.com/15305612/257644515-fb550af2-3194-461b-870c-ffe00c804ad1.png)
![image](https://user-images.githubusercontent.com/15305612/257644543-411cdcdb-55f8-4b47-873e-168a621ac078.png)
![image](https://user-images.githubusercontent.com/15305612/257644565-51855118-8c4f-4823-98d8-6e39cf536395.png)
![image](https://user-images.githubusercontent.com/15305612/257644573-bb1702f5-3b7b-41de-8524-d5b3643c1272.png)

## 2022.7.3 - Made my day
![image](https://user-images.githubusercontent.com/15305612/257643874-5f83d741-e332-4fa3-8ee4-9ccaad2273ee.png)

## 2022.7.28 - Recursive DataTypes
Recursive datatypes working at compile-time. Might have runtime demo later tonight.

The weird macro syntax on line 12 will probably be removed/optional eventually

Still unsure about making a dedicated list syntax to hide this ugliness like haskell does

![image](https://user-images.githubusercontent.com/15305612/257644910-303d2de8-4695-43cb-913a-455e2be314aa.png)

Also a runtime demo:

![image](https://user-images.githubusercontent.com/15305612/257645225-f9a7eac0-0bc3-4f02-a80d-0012e0763552.png)

## 2022.7.29 - Potential for optimizations
The generated code has a lot of room for optimizations as a result of how I've built the compiler. Thankfully there's a lot of cases where [A] negates [B] so eventually could probably add another compilation step 

![image](https://user-images.githubusercontent.com/15305612/257645397-e7dc758c-a91a-4c19-bf02-2bcaada229db.png)
![image](https://user-images.githubusercontent.com/15305612/257645407-c1291983-3a1f-4901-90e7-0b3c4dc07f80.png)

Also TCO didn't understand the `match` keyword at the time.

Another idea I had was to add a form of scoping for locals. This way we can recycle variables thus reducing the amount of memory used and importantly for references it would allow objects to be free'd as soon as they're no longer needed.

![image](https://user-images.githubusercontent.com/15305612/257645546-6febe81c-44b8-4005-be59-90b4bf2a2881.png)

## 2022.8.5 - String/list planning
I could emulate Haskell's String type by doing:
```
I32 $Char =
I32 List $String =
```
But below I explain why I probably won't make that the default string implementation.

Because in my lang, each node in a linked list has 128 bits of overhead (in addition to whatever actual data is being stored, chars would be represented as i32s), I'm thinking that the default string implementation should not be a linked list

![image](https://user-images.githubusercontent.com/15305612/257645842-38c49acd-435a-4c7d-937b-6caeeefa6bc9.png)

Haskell has similar memory usage here (potentially worse, as they didn't include GC metadata)... But seems it's common to use different string implementations in Haskell due to this so plan is to just make equivalent to Data.Text the default

![image](https://user-images.githubusercontent.com/15305612/257645938-ca7f7a1a-4edb-42e6-b262-24495d466807.png)
![image](https://user-images.githubusercontent.com/15305612/257645962-fb43667f-87b3-4841-8eae-18eff7e4f7c2.png)

## 2022.10.26 - List demo improvements 
Made the list demo more interesting, also I started towards improving the memory efficiency by making some temporary locals generated by the compiler automatically removed so that they don't waste as much space since I noticed that wasm optimizers aren't able to do this by themselves
![image](https://user-images.githubusercontent.com/15305612/257646506-8739850c-56c3-432b-8a1b-cf2e2914cbac.png)
![image](https://user-images.githubusercontent.com/15305612/257646523-bd259094-f874-4696-957a-4210f0406e72.png)
![image](https://user-images.githubusercontent.com/15305612/257646538-0be5a399-a59d-4882-97d7-89e6c41d4b57.png)

## 2022.10.26 - Lost of optimism for project
I don't forsee this language fulfilling my original goals (ie - bad fit for target use case) but it's so far along at this point that I kinda want to just keep working on it so I can do cooler demos. But would be nice to have a new long-term side-project.

![Screenshot from 2023-08-01 16-32-33](https://user-images.githubusercontent.com/15305612/257647048-d4cc3c1a-7713-4256-977d-c038af303a74.png)

## 2023.8.1 - About this devlog archive
I started on a big demo in this language -- a raytracer. But I never was able to get it working and I honestly doubt that I ever will. This project was very fulfilling for me to work on. I learned a lot and wish I had a similar project in my life now that would challenge me to think and innovate. I leave this devlog archive as a way for people to look back at how the language came to be. 

Please read this related blog post about the language: https://blog.dvtt.net/posts/ph.2022.5.6