# Postfix Haskell 2022.5.6

For the past 2 years in my freetime I've been working on a [postfix, functional programming langauge which compiles to webassembly](https://github.com/dvtate/postfix-haskell). Admittedlty it still has a good ways to go before it's usable for my intended purposes and even further to go before it's production ready. But I've at least been able to use it to make [some small demos](https://github.com/dvtate/phlappy-bird).

I've taken a bit of a break from working on it these past few months as I recently moved and started a new job but I'm looking to get back into it and start implementing runtime closures, enums, etc.
[![organized list of language tasks to work on](https://www.wasm.builders/remoteimages/uploads/articles/jpa785owidbov394k7jc.png)](https://docs.google.com/spreadsheets/d/1HZEsRAPhoAOnP-zT70_9bgLTrJVC9NmNyxKYWxsTT8Q/edit?usp=sharing)
 
The compiler is written in TypeScript (and runtime is hand-written WAT) as I'd like to eventually be able to compile programs in the browser. The code is well documented and commented for anyone curious. It's still a long ways off from being self-hosted. ![Screenshot of typescript code from the compiler](https://www.wasm.builders/remoteimages/uploads/articles/t16leffr7prldwiu4eb6.png)

The langauge is pretty interesting, [the standard library actually defines a lot of basic operations](https://github.com/dvtate/postfix-haskell/blob/master/planning/stdlib/prelude.phs) (ie - math, logic, comparisons, etc.) in terms of inline WASM and/or the langauge itself. While this shows how powerful the langauge is and it gives the user a lot of control over the language and optimizations it also contributes to a somewhat sluggish compile time. Additionally, the langauge doesn't require type annotations and as a result is very context sensitive and polymorphic.

![Screenshot of code from standard library](https://www.wasm.builders/remoteimages/uploads/articles/87tl01psou7iki9b3ntx.png)

Of course the most noticable thing is that the language is postfix, giving it a small but existent barrier to entry but I've found most programmers are able to pretty quickly get comfortable with using a postfix language and it makes many operations more natural and less ambiguous, and most importantly my initial plan for this language was as the compilation target for visual tool and this syntax definitely helps.
![Implementation of fizzbuzz in the language](https://www.wasm.builders/remoteimages/uploads/articles/jcqmwluohr2u5y401cib.png)
 
I'm currently struggling with [how to add runtime closures into the language](https://github.com/dvtate/postfix-haskell/blob/master/planning/brainstorm/Closures.md) as the way I've designed the compiler makes it difficult to detect this when it's needed. Additionally I'm still not fully confident with [my design for enum types](https://github.com/dvtate/postfix-haskell/blob/master/planning/brainstorm/Enums.md).

Another, mostly solved, design challenge has actually come from WebAssembly itself. Beacuse locals and the stack are not stored in addressable linear memory (good for security, but bad for usability) it makes it challenging to create [a moving, tracing garbage collector](https://github.com/dvtate/postfix-haskell/blob/master/lib/rt.wat) as not only do we need to be able to see all the object pointers currently in use but we have to be able to change them without old addresses being used later on in the program. This required adding to the runtime two virtual stacks in [linear memory](https://github.com/dvtate/postfix-haskell/blob/master/planning/implementation/lm.md), one similar to function locals and another similar to the WASM stack for garbage collected object pointers.

I've posted pretty regular updates as I developed this language to a twitter thread for those interested: https://twitter.com/hoffridder/status/1355760499057680395

Anyways, I'm not really sure what I'm hoping to achieve with this post but I did feel like sharing after seeing that this community exists and maybe getting some feedback if anyone checks out the language, compiler, runtime, etc. that I can use once I get enough courage to jump back into working on it Or if anyone wants to contribute, send a pr or [reach out to me](https://dvtate.com)!
