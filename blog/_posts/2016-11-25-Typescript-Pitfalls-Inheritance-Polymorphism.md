---
layout: post
title: Typescript pitfalls&#58; Inheritance and Polymorphism
tags:
- javascript
- typescript
- inheritance
- polymorphism
description: Typescript pitfalls&#58; Inheritance and Polymorphism
---

This is the second post of my _Typescript Pitfalls_ serie. You can find the first post about typecasting and json [here](http://mathieunls.github.io/blog/Typescript-Pitfalls-1/).
In this one I explore the problems with inheritance and polymorphism of typescript (or any language transpiled from OO to anything else, really).

<!--more-->


Let's assume that we have a simple inheritance hierarchy as follows. We have an interface Animal that defines the method `eat():void` and `sleep():void`. 

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=interface-animal.ts"></script>


Then, a class `Mammal` that implements the Animal interface. This class also adds a constructor and leverages the private name:type notation we saw earlier. For the `eat():void` and `sleep():void` methods, this class prints "Like a mammal".

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=Mammal.ts"></script>


We also have a `Dog` class that extends `Mammal` and override the `eat():void` so it prints "Like a Dog".

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=dog.ts"></script>

Finally, we have a function that expects an `Animal` as parameter and, invokes the `eat()` method. 

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=index.ts"></script>

The output is:

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=output.sh"></script>

Now, the last creation: `let abomination: Dog = new Mammal("abomination");` should not be possible as per object oriented principles. Indeed, the left side of the affectation is more specific than the right side, which should not be allowed by the Typescript compiler. If we look at the generated JavaScript, we can see what happens. The types disappear and are replace by functions. Then, the types of the variables are inferred at creation time. 

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=index.js"></script>

When in doubt, it is always a good idea to look at the transpiled javascript. You will see what's going on at execution and maybe discover other pitfalls! On a side note, the Typescript transpiler is fooled here because, from a JavaScript point of view, Mammal and Dog are not different; they have the same properties and functions. If we add a property in the Dog class (i.e. private race:string), then it won't transpile anymore. It means that overriding methods is not sufficient to be recognized as type, you must be semantically different. 

This example is a bit far fetch, and I agree that this Typescript specificity won't haunt you every day. However, if we are using some bounded genericity with a strict hierarchy, then, we have to know about it. Indeed, the following example, unfortunately, works:

<script src="https://gist.github.com/MathieuNls/8d874d32142aa917f7a10a62c7728f49.js?file=genericity.ts"></script>
