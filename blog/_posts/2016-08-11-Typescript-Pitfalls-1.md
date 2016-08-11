---
layout: post
title: Typescript pitfalls: Type casting and JSON
tags:
- javascript
- typescript
- json
- api
description: Typescript pitfalls: Type casting and JSON
---

I am currently writing two books on Angular2 for Packt Publishing ([Angular 2 Design Patterns and Best Practices](https://www.packtpub.com/web-development/angular-2-design-patterns-and-best-practices) and Mastering Angular2).
So, I do A LOT of typescript and, in this post series, I go on and on about what's bother me...

<!--more-->


I've always h-a-t-e-d JavaScript. I was using it, sure, but only when it was necessary. I distinctly remember my first internship interview, back when I was a freshman at eXia.Cesi - a French computer engineering school. I only knew C and some Java, and I was asked to help on an intranet that mostly worked with homemade AJAX libraries. It was pure madness and can of steer me away from the web aspect of computer engineering for a while. I find nothing likable in the following:

{% highlight js %}
var r = new XMLHttpRequest(); 
r.open("POST", "webservice", true);
r.onreadystatechange = function () {
    if (r.readyState != 4 || r.status != 200) return; 
    console.log(r.responseText);
};
r.send("a=1&b=2&c=3");
{% endhighlight %}


How ugly is that? Of course, with jQuery modules and some separation of concerns it can be usable, but still not as comfortable as I would like.
Fortunately for me, Typescript came to save me...or is it ?

## Ultra quick overview of typescript.

TypeScript is a typed superset of Javascript; which means that, with TypeScript, you can do everything you used to do in JavaScript and more! To name a few advantages: user-defined types, inheritance, interfaces, visibility, ... And the best part is that TypeScript is transpiled into JavaScript so that any modern browser can run it.  In fact, with the use of [polyfill](https://www.wikiwand.com/en/Polyfill), even our good old IE6 can almost execute the final output. We'll get back on that in the next chapter. The [transpilation](https://www.wikiwand.com/en/Source-to-source_compiler) is different from compilation (e.g., from C to executable or .java to .class)  as it only translates TypeScript into JavaScript. 

While TypeScript is typed it only proposes four base type for you to use out of the box. The four types are string, number, boolean and any. These types can, using the “:” operator, type variables var name:String or function arguments and return type function add(a:number, b:number):number. Also, void can be used for functions to specify that they don't return anything. On the object-oriented side, string, number and, boolean specialize any. Any can be used for anything. It's the TypeScript equivalent of the Java Object for instance.
If you need more than these types, well, you have to create them yourself ! Thankfully, this is pretty straightforward. Here's the declaration of the  user class containing one property. 

{% highlight js %}
class Person{
    name:String;
}
{% endhighlight %}

You can create a new Person's instance with the simple:

{% highlight js %}
var p:Person = new Person();
p.name = “Mathieu”
{% endhighlight %}

Here, I create a variable p that statically (e.g. left-hand side) and dynamically (e.g. right-hand side) a Person. Then, I affect “Mathieu” to the name property. Properties are, by default, public, but you can use the public, private and, protected keywords to refine their visibility. They'll behave as expected of any object-oriented programming language.
Typescript supports interface, inheritance and polymorphism in a very simple fashion. Here is a simple hierarchy composed of two classes and one interface. The interface—People—define the string that will be inherited by any People implementation. Then, Employee implements People and adds two properties: manager and title. Finally, the Manager class defines an Employee array.

{% highlight js %}
interface People{
    name:string;
}

class Employee implements People{
    manager:Manager;
    title:string;
}

class Manager extends Employee{
    team:Employee[];
}
{% endhighlight %}

Functions can be overridden by functions that have the same signature, and the super keyword can be used to refer to the parent implementation.
Interface People {

    name: string;
    presentSelf():void;
}

{% highlight js %}
class Employee implements People {

    name: string;
    manager: Manager;
    title: string;

    presentSelf():void{

        console.log(

            "I am", this.name, 
            ". My job is title and my boss is", 
            this.manager.name

        );
    }
}


class Manager extends Employee {

    team: Employee[];

    presentSelf(): void {
        super.presentSelf();

        console.log("I also manage", this.team.toString());
    }
}
{% endhighlight %}

The last thing you need to know about Typescript before we move on to the best practices is the difference between let and var. In typescript, you can use both to declare a variable.
Now, the particularity of variables in typescript is that it let you decide between function and block scope for variables using the var and let keyword. Var will give your variable a function scope while let will produce a block scoped variable. A function scope means that variables are visible and accessible from and to the whole function. Most programming languages have block scope for variables (i.e. c#, java, c++, …). Some languages also offer the same possibility as typescript such as Swift 2. More concretely, the output of the following snippet will be 456:

{% highlight js %}
var foo = 123;
if (true) {
    var foo = 456;
}
console.log(foo); // 456
In opposition, if you use let, the output will 123 because the second foo variable only exists in the if block.
let foo = 123;
if (true) {
    let foo = 456;
}
console.log(foo); // 123
{% endhighlight %}

Now that we powered through the language, let's see what's broken !

## Type casting and JSON

Let's assume that we have an User class with two private variables: lastName:string and firstName:string. 
In addition, this simple class proposes the method hello that prints "Hi I am", this.firstName, this.lastName. 

{% highlight js %}
class User{
    constructor(private lastName:string, private firstName:string){
    }
    hello(){
        console.log("Hi I am", this.firstName, this.lastName);
    }
}
{% endhighlight %}

Now, consider that we receive users through a JSON API. Most likely, it'll look something like that 

{% highlight js %}
[{"lastName":"Nayrolles","firstName":"Mathieu"}...]. 
{% endhighlight %}

With the following snippet, we can create a User. 

{% highlight js %}
let userFromJSONAPI: User = JSON.parse('[{"lastName":"Nayrolles","firstName":"Mathieu"}]')[0];
{% endhighlight %}

Until now; the typescript compiler doesn't complain, and it executes smoothly. It works because the parse method returns any (e.g., the TypeScript equivalent of the Java Object). Surely enough, we can convert the any into User. However, userFromJSONAPI.hello(); will yield:

{% highlight js %}
json.ts:19
userFromJSONAPI.hello();
                 ^
TypeError: userFromUJSONAPI.hello is not a function
    at Object.<anonymous> (json.ts:19:18)
    at Module._compile (module.js:541:32)
    at Object.loader (/usr/lib/node_modules/ts-node/src/ts-node.ts:225:14)
    at Module.load (module.js:458:32)
    at tryModuleLoad (module.js:417:12)
    at Function.Module._load (module.js:409:3)
    at Function.Module.runMain (module.js:575:10)
    at Object.<anonymous> (/usr/lib/node_modules/ts-node/src/bin/ts-node.ts:110:12)
    at Module._compile (module.js:541:32)
    at Object.Module._extensions..js (module.js:550:10)
{% endhighlight %}

Why? Well, the left side of assignation is defined as User, sure, but it'll be erased when we transpile it to JavaScript. 

The type safe TypeScript way to do it will be:

{% highlight js %}
let validUser = JSON.parse('[{"lastName":"Nayrolles","firstName":"Mathieu"}]')
.map((json: any):User => {
    return new User(json.lastName, json.firstName);
})[0];
{% endhighlight %}


Interestingly enough, the typeof function won't help you either. In both cases it'll display “Object” instead of “User” as the very concept of “User” doesn't exists in JavaScript.