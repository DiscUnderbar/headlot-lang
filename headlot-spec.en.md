# Headlot Programming Language Plan

> Status: draft (alpha 0.1) · Written 2026-07-07 · Updated 2026-08-29
> Implementation language: **C++** · Purpose: a tool that can actually be used

---

The reason the language is named Headlot is that H shows a rigid form. And ead, inside that rigid form there are features that move freely, and lot, there are a lot of those features. There really are many. But the H form can be seen as just one thing. It is the argument function and a few remaining forms.

## killer use case

This language gave up on the learning curve.

**Why did it give up on the learning curve**: that was the purpose of this language from the start. In a way it is one of the killer use cases.\
Other languages originally have one problem. The code is very complicated. In an if statement `{}` is the block, but then when you iterate an array with `.forEach`, `() => {}` is used like a block.\
And when you just want to say "if this condition holds, run this", you can't write

```
this.runIf (1 == 1) {
   print("Hello, World!");
}
```

like that. Instead you have to do the complicated

```
let condition: condition = {
   values: [pointEnum.ch, "~"],
   opeartors: ["same"],
};
this.runIf(condition, () => {
   print("Hello, World");
});
```

In the first place this throws form to the dogs and works around what the language doesn't allow in some other way, so the code gets more complicated. Who would like a language where you write code like this?

A language like Java is at least tolerable, but you still have to write code in that style. In Java a few parentheses just disappear and the keywords all look tidied up, that's all.

Headlot solves this, and this kind of code is possible.

```headlot
this.runIf (this.ch == "~"):{
   Line.addLine("Hello, World!");
};
```

Much better to look at. The if statement too

```headlot
if (1 == 1):{
   Line.addLine("Hello, World!");
};
```

It caught two birds with one stone, consistency included.

But there is an obvious trade-off. It is way too hard to learn. Really hard. In exchange the code becomes much cleaner. If you are a coding beginner, I hope you drop this document right now and go study an easy language like Python first.

---

And you could point out Lisp's dialect problem. This part will only make sense after you understand the whole grammar of Headlot, but I still recommend at least skimming it. What kind of language this is, why it is needed, its advantages, why you should use it.

In Lisp, the project chooses a dialect. But in Headlot, the project creates a framework that fits it — that is, a dialect — and builds the project with it. The two look similar but they are entirely different. Lisp makes dialects. But then the project has to choose the dialect that fits it.\
The downside is that when you go to another project you **can't understand** what it means.

But Headlot is different. Even when you go to another project, the form is kept and the grammar is kept, so even if you don't know what a function does, you **can still understand** what it means. Because everything is unified into countries, small countries, and argument functions, so with that, whatever you'd call another project's dialect or framework,\
unlike Lisp, you **can roughly understand it.**

This is a bit hard, so let's take an example. Common Lisp among the Lisp dialects **implemented** even OOP with macros. But the downside is big. Users of other Lisp dialects **can't understand** what this dialect means.

But look at Headlot code. Even if every project uses a completely new dialect and uses that dialect's framework, everything is still the same `self.runIf ():{}`, and in a way you **can tell** from the FuncKind, the shape of the argument function, that `()` here is the condition and `{}` is where the block will come. It is not a new concept, it is **an existing concept**.

If you still don't understand it well, just read the whole official grammar document. This concept is one you can only understand by understanding that.

Still, one last comparison:

Lisp is not at the level of dialects, it is at the level of different languages. *English, Korean, Japanese* — the two only share the form of being a language, and in fact they **look very different**. That is a Lisp dialect.

Headlot is a regional accent. Each project, that is each region, has developed to fit its place, and anyway as long as it isn't at the level of a deep Appalachian holler accent, you **can understand** another region's accent.

But even so you can ask: the dialect problem still remains, how are you going to solve it?

It is actually **the exact opposite**. There is no dialect problem, and it solved the dialect problem of other languages. What does that mean?

Look at NumPy in another language, Python. It is just a different language; `a[:, None, ::2]`, which you can't figure out on first sight, and `a[a > 3]`, which you can't even tell what it is. That is a dialect. The reason this dialect got ugly is that the language forces you to work around this part because there is no other way. To make your own block in Python you have to work around quite a lot. You make a new function and put it in the callback part, and thank goodness there's at least lambda — if there weren't even that... horrifying.

And in JavaScript and TypeScript the workarounds continue. When you do something like "skip if this condition holds" in a compiler and you substitute an expression, what gets passed is the result of it, that is, with `this.ch == "~"` the expression itself is not passed, true or false is passed. That is the weak point of other languages.

So other languages, to work around this again, give birth to data structures like `{values: [thisObjectEnum.ch, "~"], operators: ["same"]}`. *WOW!!!* Really hard to look at. So for maintainability you write code that converts `this.ch == "~"` into that form, and then for that you write a parser and a tokenizer... you end up making a whole programming language because of this one simple thing. *WOW!!!* Really absurd. Why can't we just pass `this.ch == "~"` as it is? For reference, this is the core background behind the appearance of Headlot's IOP.

And as for the dialect problem of NumPy's strange symbols, Headlot makes the meaning visible. When you first see that you can't tell what it means, because Python doesn't support that kind of thing so it **worked around it.** But Headlot doesn't create a reason to work around and removes the need to work around. The code turns from those strange `::2`, `:` symbols you can't understand into a real language, into direct words.

(While writing this I didn't know NumPy's syntax and tried my best to interpret what that means, but I really couldn't interpret what `a[:, None, ::2]` means, so I couldn't make a usage example in Headlot directly. Sorry.)

Then you can ask: **other languages keep one form to begin with, but doesn't Headlot get dialects even where ordinary languages don't, because of the new control structure called the argument function and the macro called expand?**

No. If you clearly know when to use an argument function or a country in a Headlot function, you can use the function even without knowing its declaration — just knowing roughly which country of this function, which number country it is, is enough.

First, when do you use a country in this function? When you need a callback. But in other languages callbacks are complicated. Somewhere you have to put which callback in which parameter position, and an if statement uses `{}` like a callback but the user can't make that, and to implement it you have to... and when you look at the result it is truly amazing. **WOW!!!** goto gets thrown around, while loops are nested several layers deep, and code gets completed that gives you no clue what it does when you look at it! As an example, if you go to [example project](https://www.chiark.greenend.org.uk/~sgtatham/mp/), you can see how much this person struggled for his own Loop.

So Headlot's callback country rule is this. One bundle is kept bundled up as a country. So the code that makes this is kept as a country called doing, in that style. And in the first place, worrying about which countries there are is the same as worrying about which position in the order a callback is.

And in the first place, if you look at a new project and its functions are usable from the start and don't sound like weird alien language, that would be stranger. Sounding like weird alien language is just how every language is. You can only use it once you understand the code. If you just hate this, go vibe code with an AI. And in the first place Headlot's country and small country system will look like alien language at first too. But it is clearer. You use this function by using the callback directly as a block called an argument function, and this is actually easier to look at than forcing a callback in as a function while keeping only the form "put arguments into a function". It is easier to learn too. Because the form is clear. A callback always goes `{}` or `():{}`. Really clear. If anything, this callback part is easier to learn.

Also expand is just something similar to a macro. Also, unlike Lisp, it **cannot change even the control structures**. With Lisp macros you can make an entirely different language. But Headlot can't do that. Because expand is used when you need to run code fitted to that environment, and using an argument function in a different shape or using a function in a different shape with it is absolutely impossible. expand does not support writing code in a completely different way; it is just used when running that code fitted to the environment of the side that uses it.

> For reference, I added some emotional words.

## Target users — who is this language for

Headlot is a language for **skilled power users — systems- and performance-oriented developers**. People who want **both** native performance and maximum freedom (redefining even control structures), and are willing to pay the learning curve as the price. Close to the crowd that uses Zig, Rust, and Lisp.

**Reason for the difficulty**: the learning difficulty is really high, Headlot is really high. Because the amount of already-existing concepts used here is close to zero. But the funny thing is that almost every concept that appears here actually exists. expand is Zig's comptime, type magic is C#'s expression\
But those weren't used knowing they really existed; after making them, they just looked conceptually similar. Even so it is hard to learn, because those concepts from other languages are interpreted in Headlot's own way. The argument function is for passing the arguments together clearly at once when a callback is needed\
Type magic is for avoiding disasters like `{values: [1, 1], operators: ["same"]}`, and Headlot came up with those concepts differently, and because of that the learning difficulty goes up.

**Design purpose**: Headlot is a general-purpose language. But the first target program is games — so that I can write code the way I want. When a design splits, "which side do you need when writing a game" is the judge. Same as how C was general-purpose while taking Unix as its judge.\
Headlot can also be used in zevring, but it is not zevring-only — the fate of the language is not staked on the success of a browser. (The zevring-only language is zevra.)\
It will also be used when making the game called World War.

Explicitly **not** the target:

- Beginners / first language — lowering the entry barrier is a lower priority (1-B #4).
- Large organizations that put team uniformity first — a language that keeps freedom closed (Go and such) suits them.

**Why nail this down first (the criterion for judgment)**

Once "who uses it" is decided, every future "easy vs powerful" decision resolves automatically. On conflict, Headlot puts **power, freedom, and performance above the entry barrier**. When you're wondering whether to add sugar for beginners, the answer is "the target is power users, so only to the extent that it doesn't hurt expressiveness or performance."

However, readability (1-A #2) is still important — being for power users does not mean it's fine to be hard to read. "Write freely, but readably" is the goal.

**Two birds with one stone / trade-off**

- **Advantage**: when the target is clear, the design doesn't wobble. The "freedom vs easiness" argument is closed, and this language's central tension (open core + performance, data.md #1) is also justified as "the user wants that and can handle it."
- **Disadvantage**: mass appeal and beginner inflow are given up. The user base gets narrow. But a narrow, sharp identity is this language's reason for existing.

And sometimes when I say this language is similar to this one, that doesn't mean this feature was just taken from that language. Except where I say it was taken directly from there, everything is just similar in function, not taken.\
The reason I spell this out is that later, when learning these features, if you misunderstand a feature as being taken from that language, you might understand the feature differently, so I did it this way.

For reference, these are the things that really were referenced or taken from somewhere.

- **Yulist**: took Lua's Metatable in the form of interception + data structure.
- **expand**: while trying to make a macro feature for Headlot, it was created to make up for the problems of macros. Took Lisp's macro feature in a different form.
- **global id :: naming = ...**: taken from a programming language called zevra. That is also a language I made, but zevra is a different language from Headlot, so I spelled it out.

---

## 1. Settled decisions

- **Implementation language:** C++
- **Execution method:** native compiler (AOT) — compiles source into a machine-code executable
- **Compiler name:** CHeadlot. Went with CHeadlot to give a C++ feel.
- **Backend:** LLVM — converts the AST to LLVM IR, delegates optimization and machine code generation to LLVM
- **Design principle:** Deep Module (narrow interface + deep implementation)
- **Extension:** `.hl`. You can tell at a glance that it's Headlot.
- **Type system** static, but dynamic is also possible. Really both static and dynamic work.
- **Standard library scope** is at the level of supporting almost everything. The standard library is used directly without `take` (details → 1-C modules).
- **Compile-time mechanism:** what generics, argument function customization, constant computation, and inlining used to do is all done by expand alone. There are no separate macros or templates — it is not a C-style text macro but a compile-time expansion that works on units of meaning. (1-A #10, no duplication. Details → 1-C expand)
- **Execution model:** hierarchical actors based on cooperative scheduling — Stack / Sub-stack / Queue + message passing, with worker promotion (real parallelism) when needed. Messages instead of shared memory. (Introduced from the zevring runtime, details → 1-D)
- **Data structure:** unified into Yulist alone. Arrays, linked lists, and dictionaries are Yulists with a few settings already applied. (Details → 1-C Yulist)
- **Memory:** end with free (destroyed immediately when the country ends) + send = automatic migration + SM (substitution memory). Leak prevention and safety are the compiler's responsibility. (Details → 1-C memory management)

## 1-A. Design philosophy (implementation principles)

> Core: lowering implementation complexity is more important than anything else.

The principles kept when building Headlot itself.

1. **Performance comes first.** Not even noise-level performance waste is allowed. Otherwise weird code appears for the sake of performance.
2. **Readability matters.** If readability is bad, weird code looks weird.
3. **Save memory as much as possible.** Otherwise, code that is ugly and incomprehensible is born for the sake of saving memory.
4. **Use Deep Module.** (narrow interface, deep implementation)
5. **Don't create a new abstraction for a trivial reason.** A shallow indirection layer like a wrapper is a waste of memory and performance.
6. **Don't even provide the pretext for creating unnecessary indirection layers.** The language design must not create a reason to make wrappers.
7. **Jumps must be minimized.** Jumps break the flow while reading and lower readability.
8. **Jumps between files must be nearly eliminated.** Jumps between files make the work hard.
9. **Don't separate user and system.** Don't make calling a built-in function look like System.print(); and calling a function you made yourself look like User.print();. That actually lowers freedom a lot.
10. **Never put in several copies of the same feature.** Similar features — for example a keyword-adding feature and a function feature — there is no difference at all. It only makes the language complicated.
   And similar features are distinguished using representation orientation.
11. **When adding a feature, if duplication appears, don't delete the feature — remove the room where the duplication appeared.** When a feature is added, if it overlaps with something else — e.g. you wanted `//` for comments but it overlaps with the operator that returns the quotient of a division — don't remove the feature; remove the very reason the duplication could appear — e.g. if the `//` comment symbol overlaps with something else, use `@...` for comments instead of removing the feature.
12. **The IDE does not raise readability.** The grammar itself must have high readability.

    (0xd is an ominous number so it is skipped — it is not a typo.)

14. **The language does not force a particular mechanism.** Things like the memory management method and the error handling method are not nailed down to one by the language; the user chooses. A forced mechanism takes away the freedom of users who don't want it.
15. **The language must be flexible.** A language should originally be able to express many things more easily. If it isn't flexible, readability drops a lot, in order to implement what the language doesn't support.
16. **The language compiler must be specified to skip `/\s/`.** Distinguishing by indentation would raise readability like Python, but in places where whitespace isn't shown properly, like markdown or GPT, the meaning may not be conveyed correctly.
17. **Code that looks safe is guaranteed to be safe, and dangerous things look dangerous.** First, something dangerous looking safe is the worst situation. It's dangerous but looks safe, so you might change it slightly by mistake and something big blows up.
   But blocking all somewhat dangerous work is also bad. Because then there are too many tasks you can't do with the language.
   So the solution to those two problems is: code that looks safe is guaranteed safe, and dangerous things look dangerous.
   Because if what looks safe is guaranteed safe, the programmer can definitely write code in the safe-looking sections with peace of mind.
   And for what looks dangerous, the programmer writes code while being tense on purpose, and then can do a lot of things while writing safe code.

Also Headlot is a Representation-Oriented-Programming (ROP) and Information-Oriented-Programming (IOP) language. Before explaining what ROP and IOP are, I'll explain why they exist.

These two programming orientations come from one principle: to remove workarounds. Of these, IOP removes lack of information among the reasons for working around, and ROP came from the workaround reason of being unable to represent.

First, representation orientation is simply taking anything not as an option but as a representation. For example, it doesn't take whether this is a loop; it takes that the kind of this is a loop.\
That is, rather than picking from options — twenty questions, "is this separated by `;`?", "is this block `{}`?" — it just lets the user represent it.\
That is representation orientation. Why does it exist? Because if you simply take options, you can't make your own new structure. Not at all. But representation orientation lets you make your own new structure. You can put something into a slot that takes values in an unusual way,\
or you can go and make a data structure that doesn't exist in this world at all. That is representation orientation. The way to tell whether something is representation-oriented is whether you can make a new structure here.

An example of representation orientation.

```
for (
   int i;
   start = 10;
   end = 20;
) {
   ...
}
```

This directly represents and states how much to repeat.

Now let's look at the opposite of ROP, OPOP (Option Oriented Programming) (for reference, the reason Option Oriented Programming is OPOP and not OOP is that calling it OOP could be confused with Object Oriented Programming.)

```
for (
   variableNameIsA = false;
   variableNameIsB = false;
   variableNameIsC = false;
   variableNameIsD = false;
   variableNameIsE = false;
   ...
   variableNameIsi = true;
   startIsOne = false;
   startIsTwo = false;
   startIsThree = false;
   startIsFour = false;
   startIsFive = false;
   ...
   startIsTen = true;
   endIsOne = false;
   endIsTwo = false;
   endIsThree = false;
   endIsFour = false;
   endIsFive = false;
   ...
   endIsTwenty = true;
) {
   ...
}
```

This is OPOP

(\
   For reference, OPOP doesn't only have downsides. If instead of `isArgs = true;` you make the user parse the argument-taking directly,\
   it's too hard for the user to use.\
   So if you don't want to make the user do all of that, using OPOP is also a method.\
   But Headlot is extreme ROP and does not use OPOP.\
)

Information orientation preserves all the information needed when something is passed. So for example, an ordinary language, when it takes a function as a callback, doesn't take the name, it just takes the function itself; instead, in information orientation\
it records and gives even what the name of this function is, where it was called from, where this call site is.\
More precisely, information is simply preserved. A programming style that preserves even things like the function name or where the function is used\
is information orientation.

Then you might wonder — isn't information orientation a waste of memory? Headlot's answer is **information baking**: information is not carried, it is baked.

Information orientation has two layers.

- **Static layer (most cases):** the information of functions and values — name, declaration site, call site, kind, spec — is all known at compile time. Only the fragment the code actually accesses is baked in place as a constant by expand. For example, if you use `f.name`, a name string constant is embedded at that spot, and information that isn't accessed doesn't exist in the executable at all — that's not memory saving, it's zero memory. Information that differs per call, like the call site, is inserted by expand at the call site.
- **Dynamic layer (rare):** only real dynamic queries that walk arbitrary values and ask for information refer to an **information table** that exists one per type. There is only one table in the program, so there is no copy per value, and this cost is paid only by code that used a dynamic query (cost honesty).

And you could ask "if you're going to use information orientation, can't you just mark it at the top in advance", but Headlot hates jumps. This isn't just made up — it's because in Python, when I imported something directly, breaking the code flow and going all the way to the top to add the import was really annoying. With information baking there's no need for marking at all — you just access it and the compiler bakes it. There's no reason to go up.

(The information-oriented queues and val boxes of the previous design are discarded — the cost of creating a queue every time a value is passed and the request-response latency disappear. → CHANGELOG. Inspiration: obtained from the lineage of Zig's comptime reflection. However, the combination of "bake only the fragment you use + call-site injection + optional information table" was derived from Headlot's expand and two-layer principles.)

For reference, the core of Headlot's features is really this. Almost everything uses a similar form. That is, instead of separating Array and Dict apart from Yulist, everything is done with Yulist. Even without keywords, everything uses the form of a function with an argument function. So the advantage that comes out here is that instead of having to know several weird features to know how to use something, just looking at the argument function form makes it easy to memorize how to use it. In other languages, no matter how long you've done it, over time you're bound to get confused about taking arguments. Because there's no such thing as "this kind of argument goes in the x-th parameter." But Headlot is just one form. It's a feature you get a rough sense of even without knowing, and if the usage is really clear, you can tell even without knowing how to put in parameters. With JS events you have to know that `"onClick"` comes in the first parameter. But Headlot is like this: `when eventName {code}`. In my opinion this is far from being a dialect — on the contrary it seems to remove dialects. The dialect of parameter order.

**The `expression` type — taking a formula with it preserved.** This is a representative surface where information orientation shows up at the parameter level. An ordinary language, when it takes `1 + 2 == 3` as a parameter, just crushes it into a single boolean (`true`/`false`). In Headlot, if you set the parameter type to `expression`, **the formula itself** arrives with its information preserved.

- `.calculation` — the calculation process. e.g. `1 + 2 == 3` → `[1, operator.plus, 2]`
- `.result` — the result value. e.g. `3`

Thanks to this, when making something like `change` (change, as in money — a function that tells you how different the value a formula represents is from the actual value), you can just naturally pass `1 + 2 == 3` without the complicated workaround of taking operators as strings like `"add"`, `"star"`, `"divide"`.

- **Why:** making operators be taken as strings is both hard to represent and bad for readability. If you preserve the formula as a value and take it, you can make `change`-type things (assertions, symbolic computation, analysis tools) far more flexibly. **The cost is opt-in** — the preservation cost is paid only when you take it as `expression`, and the performance of the default boolean path is not hurt (cost honesty).
- **Precedent:** in C#, if you assign a lambda to the `Expression` type, an expression tree is captured instead of code, and LINQ stands on top of that. Being decided by the type declaration alone is the Headlot way.

> Summary: a language's goodness must come from the language grammar, not from the compiler.

## 1-B. Execution style (language behavior principles)

The way the Headlot language behaves as seen by the user.

1. **Callbacks are passed only as functions.**
2. **Control structures are callbacks too.** Things like `if` and `while` are not special syntax either; they are handled as callbacks (closures) passed to a function. → the user can define their own control structures as functions.
3. **A name is only an appearance, it does not carry the functionality.** Name-based magic (a specific name automatically behaving specially) is forbidden. Functionality is decided only by explicit structure.
4. **Implementation freedom matters.** For the sake of freedom it's fine to give up a low entry barrier.
5. **Give enough freedom that the user can add features to the language.**
6. **A file may be a Yulist, may be a function, may be another variable, etc.** A file can take any form. A file may be a Yulist (a type), or may be made into a function. (To raise freedom.)
7. **Functions are first-class citizens.** If functions aren't first-class citizens, freedom drops a lot. Therefore functions are first-class citizens.
8. **Don't use weird abbreviations.** Weird abbreviations are also strange to pronounce so conveying information is hard.
   They also cause confusion with other abbreviations.
   But nobody will interpret i as an abbreviation of ideas instead of index.
   Nobody will interpret md as monday instead of markdown.
   If an abbreviation doesn't cause confusion like this, it's fine to use.

(For reference, name magic isn't something like this.emitEvent == "onClick"; it's things like `__init__` being for when a function runs and the `main` function just being the entry point — that is what's called name magic. Name magic.)

> Direction: minimal built-in syntax + maximal freedom of extension. A language where the user can build even control structures themselves.

The core benefit of the argument function / country / small country (and special country) system is that **you can write code flexibly.**

## 1-C. Grammar

The grammar of the Headlot language.

### Argument function (real func, argument func)

The reason the argument function is needed: other languages mostly separate blocks with `{}`. But that isn't consistent (it isn't even clear why they do it that way). So Headlot made the **argument function**, on the premise that a block is passed in callback form. The argument function is the core of the core of Headlot. In Java terms it corresponds to a Class, in JavaScript terms to the `{}` block syntax.

The argument function is a second-class citizen, and **its base form is `(args):{body}`, writing only the arguments and the body.** The parameter and return type slots are omitted by default — parameters are injected as small countries, and by default there is no concept of returning either.
However, if needed you can attach extension slots and write `(args):(slot1):{body}:(slot2)`, using, say, slot1 as parameters and slot2 as the return type.

For reference, the reason the argument function was made `(args):{body}` is that there's no need to make it complicated. Making the most-used symbol in this language complicated as `newRealFunc(args, () => {body})` would be more confusing. It just became `(args):{body}` by making it as short as possible. For reference, it used to be `{args}:(body)`, but since other languages mostly do it like `if (1 == 1) { console.log("Hello, World!"); }`, it was changed to `(args):{body}`.

First, here's how to write an argument function (base form)

```headlot
(args):{body};
```

And the `if`, `while` and such that come before this `{body}` (form 2-2) are function names. If a function name that isn't registered comes before `{body}` (form 2-2), an error occurs.

If you don't write `;`, everything up to the next argument function is treated as the same argument function, so `;` is very, very important.

In the base form, parameters are not slots of the argument function but are injected as small countries (in the extended form you can write the parameter slot directly), and static parameters that specify a type like `x :: int` are the norm.

And an argument function can take several argument functions, and an argument function that gathers such argument functions is called a multi-country argument function.

For example, in an `if` statement you have to make it possible to also write `else` after the `if`, but the argument function written after `if` and the argument function written after `else` have to be different while sharing things with each other. So argument functions have a thing called a country.

Countries work roughly like this.

In an `if` statement, the argument function after `if` is country 1, and `else` and `else if` are country 2.

Here country 2 can only be used if country 1 exists, and country 3 can only be used if country 2 exists. What that means is

```headlot
else {

};
```

This makes no sense. Because there's no `if` in front and `else` came straight away.\
So `if` is country 1. And else or else if is country 2.

And you can pass information from country 1 to country 2, from country 2 to country 3, and so on.

That is,

when sending information from country x to country y,

x <= y

must hold. In other words, information is passed **only from a lower country to a higher one (1→2), or between countries of the same number.** The reverse direction (higher country → lower country) is impossible.

Because a country's information is destroyed immediately when that country finishes its job, and a lower country runs and exists before a higher one. If the direction is fixed to one way (lower→higher), reading information that may already have been destroyed can't happen in principle, so "destroyed safely the moment the country ends" holds.

And exchanging information between countries like this is called inter-country communication. For inter-country communication, to save memory, the information is destroyed as soon as that country finishes all its work.

- **Why:** as with `if`→`else`, there are many cases where several blocks connect to each other (sharing information) while each plays a different role. If you put each block in a separate function there's no way to exchange information, and if you put them all in one function the roles get mixed. Country reveals the "connected stages" in the grammar and solves both at once. (An argument function that bundles several countries is the multi-country argument function above.)
- **Advantage:** the stage order (lower→higher) and the timing of information passing and destruction are fixed by the grammar, so connected structures like `if`→`else` can be built safely without hidden shared state. The user can also define their own multi-stage control structures as countries (1-B #2, #5).
- **Disadvantage:** you have to know "which number country this is" and "from which country to which country information goes", so there's one more concept to learn than a simple block.

And what comes right before this argument function, right after the function name, is called naming.

```headlot
func moveTo (x :: int, y :: int, z :: int):(
   @... body
):();
```

Here `func` is the function name and `moveTo` goes in as naming[0]. If you attach several labels, you access them like an array as `naming[0]`, `naming[1]`.

(Note: this example used to use `class Point`, but class has been removed — structural types are now made with Yulist. → the `Why Yulist exists` section.)

- **Why:** something like the `moveTo` in `func moveTo`, "a name attached after the function name", is a third thing that is neither a value nor a parameter. If you cram it into the argument or parameter position, "name" and "data" get mixed and the meaning gets muddy. naming pulls this label out into a dedicated position and handles it clearly.
- **Advantage:** things that are awkward to take in the argument (`()`) position — things that aren't values or data, like labels — can be taken easily with naming. It's like taking them through a dedicated channel without polluting the argument slot. Also, since names don't get mixed with actual arguments and parameters it's easier to read, and by accessing like an array with `naming[0]` you can handle multiple names regularly. It also ties in with "a name is only an appearance and does not carry the functionality" (1-B #3) — a name is just data called naming and does nothing special.
- **Disadvantage:** you have to learn one more concept called naming, and since the name doesn't look like a value, it can be confusing at first where it goes in.

So an argument function is the argument you put in when calling a function.

tmi
The terminology is probably a bit strange, and you'll probably think this is quite far from functions. Actually at first it was fairly close to functions, but as it got more systematic it drifted further from functions.

### mapping real func, mapping argument func

A mapping real func is just an argument function converted into an executable form. Basically the execution method is just running an argument function according to a specific form. And it runs in the manner of pasting the code here as-is. And since a mapping real func is on the second-class citizen side, creating a new one is possible, but passing it directly as a value and so on is impossible. If you do that the value becomes never outright. Also this type is never. Because first, in Headlot values are alive even at runtime. But a mapping real func disappears at runtime. In the end there is no value at all and as a result it becomes never. It isn't that information was passed either. A problem occurred in the information passing, so systemically the information isn't passed at all, and that's why it's never. For reference, that's why it's never and not nothing.

The execution form is `argumentFunctionForm mappingRealFunc`. So an ordinary function is this: `func argumentFunction`, for example `print ():{};` in that style. But a mapping real func is different. It's `[]:[]mappingRealFunc`.

Also the argument function form is written like this.

`[]:[]`

That's the basic one.

`[]`

This form also works

For example, if the form were this


(args):{
   code
};

then you'd have to do this.

`[ARGS]:[CODE]`

And if it were


(X :: int, y :: int):{
   code
}:(type);

it goes like this.

`[NAME(PascalCase)<TYPE>, REPEAT]:[CODE]:[TYPE<NONE -> nothing>]`

To interpret it: first, `[]:[]:[]` means there are three slots.

And NAME means it takes the arguments through Naming. That is, it takes those and in the execution, that is in CODE, you can take that NAME and use it directly. And in `NAME()<>`, inside `()` you write the gentleman's agreement naming convention, and inside `<>` you write the type, which is mandatory (when TYPE comes in the constraint part of NAME, the rule becomes to write it as `:: type`). And `, REPEAT` means that form keeps repeating.

Also the TYPE at the end means one type comes there, and inside it `NONE -> nothing` means that if the slot is empty, nothing is automatically put in.

Also, the way to make this mapping real func is to use the mapping function.

`mapping argumentFunction` — then that argument function is mapped and returned. That's how it's done.

```headlot
var helloWorldRealFunc :: never = mapping ():{
   Line.addLine("Hello, World!");
};
[]:[CODE]helloWorldRealFunc; @= after compiling, the body of that argument function, Line.addLine("Hello, World!");, gets pasted in
```

That's how it goes. Also, that is precisely a second-class citizen, so it uses cammelCase.

// TODO: complete this properly

### Principle 0 — every construct is an abbreviation of the argument function

Everything in Headlot (literals, values, control structures, the Yulist data structure) is a special case and abbreviation of a single form — the **argument function**. The base form is `(args):{body}` (form 3), and if needed you can attach extension slots and write `(args):(slot1):{body}:(slot2)`, using, say, slot1 as parameters and slot2 as the return type.

- The literal `5` is the same as `(5):{}`. (The value `5` being passed as an argument.)
- A literal is a special argument function with no body slot. Since it has no code to embed, it can go anywhere, so it's first-class. The boundary between first-class and second-class = whether it has a body slot.
- `if`, `while`, `switch` and such are merely "function names" that come before this structure. They are not special syntax. (An error occurs if an unregistered function name comes.)

**Why do it this way (WHY)**

If a language effectively has only one construct, there's only one thing to learn and duplication is impossible in principle. This is the extreme realization of 1-A #10 (no duplicate similar features), and it completes 1-B #2 and #5 (control structures are callbacks too, the user defines control structures directly). If the user registers a new function name, they can make their own control structure used like `if`.

**Two birds with one stone (advantages vs disadvantages)**

- Advantage: learn one form and the whole language opens up. The parser and grammar get simpler, and the dissonance of "this is syntax and that is a function" disappears (1-B #7, functions are first-class citizens).
- Disadvantage: you can't type `(5):{}` every time just to use one value. → so **abbreviated forms (forms 1 and 2)** exist for frequently used shapes. In exchange there's a learning cost of having to learn the abbreviation rules.

**Performance (expand)**

Core control like if/while is defined with expand. expand expands calls at compile time, so the callback call cost is 0. Keeping an open core while preserving native performance — expand is the answer to this decisive point.

### The shapes of the argument function

Arguments are separated by `;`. (Arguments are a **function-side boundary**, hence `;`. Element boundaries of data like arrays and lists are `,` — a different axis. Same as how function parameters and lists differ in TS.)

- **Form 1** `"aa"; "bb"` — values. Values are passed as arguments. (Abbreviation of `("aa"; "bb"):{}`)
- **Form 2** `("aa"; "bb")` — values wrapped in parentheses (separated by `;` or `,`). Passed as arguments.
- **Form 2-2** `{body}` — the form where you write only the body without arguments. It's the abbreviation of `():{body}` with the empty argument `()` deleted. Countries with no arguments to take, like `else` and `expand`, fall here.
- **Form 3 (base form)** `(args):{body}` — `()`=arguments, `{}`=body. The base shape of the argument function. The parameter and return type slots are omitted by default (parameters are injected as small countries, no return concept by default).

For reference, in an argument function

**Why forms 1 and 2 are needed**: the basic shape is form 3 `(args):{body}`. But writing `("1"):{}` every time when only passing a value is wasteful (→form 1), so there's an abbreviation that passes values wrapped in parentheses (→form 2). That is, forms 1 and 2 are abbreviations of form 3. Conversely, when there are no arguments at all, you use form 2-2 (`{body}`) with the empty `()` deleted — this is also an abbreviation of form 3.

**Form 1 vs form 2 rule**: form 1 isn't wrapped in `()` so it's concise when simple, but when the arguments get complicated readability drops and there's a risk the compiler interprets it wrongly. **Therefore in complicated cases you must use form 2 (`( ; )`).** Forms 1 and 2 have the same meaning, and form 2 is the safe, explicit one.

**Separating by `,` vs by `;` in forms 1 and 2**: for a plain function call, separate with `,`, and when it gets complicated — many arguments in the argument part of an argument function with many line breaks — separating with `;` is recommended. It isn't forced. If there were something like "separate by l when there's a `\n`", the principle that `/\s/` is ignored would break.

- **Why:** most callbacks (e.g. the block passed to `if`/`while`) need neither parameters nor a return. Making the default the omitted form means the most common case is written the shortest. But removing the slots entirely would make it impossible to express cases that really do take parameters and return values, like `func`, so the slots aren't deleted but left as options.
- **Advantage:** the common case is concise (omitted form), and the necessary case doesn't lose expressiveness (extended form). One grammar catches two birds with one stone.
- **Disadvantage:** the same argument function can have different slot counts, so the reader has to distinguish "how many slots is this". If this distinction and the parsing rules aren't nailed down firmly in the `func` design, it could get ambiguous (which is why the rule is listed as an undecided item).

### The path by which a value comes out

- In forms 1 and 2, **the argument itself is the value.** (`5` → 5)
- The base-form argument function has no return concept. That is, unless the return type slot is turned on, there's no path to send a value out with `return`.
- Return only has meaning in the extended form when the return type slot is attached (typically an ordinary function), and the exact way it's specified and handled is settled when designing the function structure (`func`) (→ undecided item).

**Why**: if the base form's value path is fixed to arguments only (forms 1 and 2), no hidden returns or hidden control flow appear. The slot is turned on explicitly only when a return is needed, so the return path is always visible in the code (principle 3).

### Execution vs reference

**If a minimal argument function comes after a function name it's execution (a call); if not, it's a reference.**

```headlot
anything b = break ();   @... a minimal argument function () came after break → execution (call)
anything b = break ;     @... no argument function came after break → reference (not executed)
```

- `f ()` = call, `f` = reference. Same as the convention of most languages (`f()`/`f`).

**Why**: whether it executes is shown not by a separate symbol but by **the presence of a following argument function (structure)**. Doing it this way means (1) no new symbol for marking execution is needed at all (counting `;;`, a separate separator `\`, etc.) — `;` just stays as statement termination — (2) since execution is shown by structure it's unambiguous, and (3) it's the `f()`/`f` convention so the learning cost is low. It catches **unambiguity, familiarity, and symbol economy at the same time.** (It derives directly from principle 0 — "function name + argument function = call".)

- **Disadvantage/undecided:** whether the "minimal argument function" is exactly `()` or some other shape (`:()` etc.) will be nailed down when the `func` grammar is settled (→ undecided item).

### Country / small country

**Country = an explicit scope/arena**: a country is an explicit scope (arena) where information passing and immediate destruction are visible in the grammar. When a country finishes its job, the information is destroyed immediately. There's no hidden control flow and no hidden allocation (principle 3).

A **small country** is an existence that exists only inside a specific country or argument function (context-dependent). It may be a function, may be a variable, may be a Yulist — it can be anything.

- Inside the country of a loop (`while`/`repeat`) there are the `break` and `continue` small countries.
- `continue` is treated as a small country that opens a new country inside the while.

- **Why:** some features (e.g. `break`, `continue`) only have meaning inside a specific context (a loop country). If you make these global functions, they're easy to call in the wrong place and cause errors. A small country guarantees "exists only inside this country" in the grammar.
- **Advantage:** calls that don't fit the context become impossible in the first place (blocked by scope), so mistakes decrease. Also, since they're destroyed together when the country ends, memory is saved too (principle 3).
- **Disadvantage:** even with the same name, whether it exists changes depending on which country you're in, so someone seeing it for the first time has the learning burden of judging "does this work here?" from context.

**Special country**: a special country that handles operators (`rshift`, `or`, `^`, etc.). It's special in two respects — (1) it can use special symbols as names, and (2) unlike small countries it isn't bound by context and **can be used in every argument function**. So: a country is a stage, a small country is a context-dependent function, and a special country is symbol operations used anywhere.

- **Why:** operators (`+`, `^`, `or`, `rshift` …) are used everywhere in code, and making you consider the country context every time would be far too inconvenient. So operators were bundled separately into a special kind of country (special country) meaning "symbol functions used anywhere".
- **Advantage:** operators can be used freely without context constraints while still keeping the principle that "a name does not carry the functionality" (1-B #3) — a special symbol is, in the end, just a registered function (a special country). It also leaves room for the user to add their own operators as special countries.
- **Disadvantage:** since special symbols are allowed as names, there's a risk of symbols colliding with each other (e.g. `//` for comments vs quotient). This has to be managed with 1-A #11 (remove the very room for duplication).

**Country execution order + break**: countries execute in number order — country 1 first, then country 2. If you use `break` in a small country inside a function declaration, you can stop after executing "this country (the current country)" or "only up to here". (This connects to the break = small country + label rule, where the label points at the target country.)

- **Why:** as with `if`→`else`, the later country often depends on the result of the earlier one. Fixing the execution order by number (country 1→country 2) makes the flow of the earlier country finishing first, passing information, and being destroyed hold naturally (matching the lower→higher direction of inter-country communication).
- **Advantage:** the order is predictable so it's easy to read, and since "the earlier country has already finished" is guaranteed, the timing of information destruction is also safely fixed.
- **Disadvantage:** the country order is fixed, so free rearrangement like running a later country first is impossible (but that freedom is mostly unnecessary and only causes confusion).

**Repetition of countries with the same number**: if there are several countries with the same number (e.g. repeated else if), they run in the order written. Inter-country communication is also relayed in that order: country 1 → first country 2 → second country 2 → …. The "skip if it already ran earlier" of the else if chain is defined by this relay (passing taken).

### Full summary of the argument function concept

There are actually few sections like this in this document, but I put this one in specially. This section is purely for understanding.

Here's why this argument function was made. And to understand at once why it has this shape:

First, the argument part of an argument function is the parameter part when calling a function. It's easiest to just understand it that way. And the code body part inside the argument function exists in order to pass a callback. Because in ordinary languages there are very many times you have to pass a callback. But in something like an if statement you just write it. In an ordinary function, though, to actually pass a callback you have to declare a function yourself. This is somewhat inconvenient. It creates a privilege only the system can use. Putting a callback in directly without a function declaration — Headlot unifies all of this into the code part of the argument function.

Also, if you have to put in several callbacks, you use countries. That's why countries exist.

### return / break / continue = small country + label (escape)

- `return`, `break`, and `continue` are all small countries.
- All three point at the destination **label** with the **`to` country**. Used without `to`, the default (the nearest target): `break`/`continue` take the innermost loop country, `return` takes the current function.
- **The label is attached to the target with naming** (the name after the keyword):

```headlot
while outer (i < 3):{            @... outer = the label of this loop country
   while inner (j < 3):{
      break to outer;            @... breaks the outer loop, not the inner one
   };
};

func find result (...):(...):();   @... result = the label of this function
return (foundValue) to result;              @... takes the value out of the result function
```

- **`to` is a country** — it's the destination country inside the `break`/`continue`/`return` small countries, so all three share the same `to` country: `break to label`, `continue to label`, `return (value) to label`. For several values, `return (v1; v2) to label`.
- **The kind of target is checked by kind:** the label of `break`/`continue` must be a loop (LOOP) country, and the label of `return` must be a function that has a return. If they don't match, compile error.

**Why it was changed from level → label:** previously you counted how many countries out with a `level` number, but **if a country was added or removed in between, the number went out of sync** (that downside was real). A label points directly at the destination by name, so it's safe under refactoring and reads better. Since the destination is still visible in the code as a name, "no hidden control flow" (principle 3) still holds — if anything it's clearer than a number. (Precedent: labeled break in Java, Rust, Kotlin.)

- **Advantage:** local (default) and non-local (`to label`) escapes are unified into one small country model (1-A #10), the destination is specified by name (principle 3), and it doesn't break when countries are inserted or removed.
- **Disadvantage:** to use a non-local escape you have to attach one label (naming) to the target — the notation can grow compared to a level number. In exchange, local escape (`break;`) stays concise without a label.

### Types

| Type    | Description                     |
|--------|---------------------------------|
| int    | 64-bit integer                   |
| double | double-precision real            |
| sizeT  | index-related                    |
| regex  | regular expression               |
| naming | used when writing the name of something |
| string | string                           |
| char   | character                        |
| boolean | true / false                   |
| condition | condition                      |
| anyVar    | dynamically typed variable      |
| Yulist   | just any Yulist                  |
| Module   | Module                         |
| nothing   | nothing                       |
| NaN    | not a number, but the number 0.0 / 0.0 |
| never  | no value; there is no value where a value should be |
| byte[T]   | 8-bit T type                   |
| short[T]  | 16-bit T type                  |
| middle[T] | 32-bit T type                  |
| decimal[T] | stores a numeric type in decimal form |
| variable[T] | a variable, static, with type T |
| typeof[T]  | the T type itself             |
| Array[...T] | an array of type ...T        |
| LinkedList[...T] | a linked list of type ...T |
| Dictionary[T, V] | a dictionary with T as the key type and V as the value type. |
| Would[T]   | not of type T right now, but will become type T. |
| any         | anything |

Except for some types, every type consumes 64 bits.

Also, a function is `func[(country1Name(the arguments country 1 takes)(country 1's small country 1(the small country's type), country 1's small country 2(the small country's type) ...), country2Name(the arguments country 2 takes)(country 2's small country 1, country 2's small country 2 ...) ...) => return type]`. Also, the parts you don't have to write here are the small country part and some `()`, which can be omitted if there is only country 1. Like this: `func[]`

> Type names follow camelCase (starting lowercase) as a principle, but `NaN` is an exception. Not a Number is standardly written `NaN` and that notation is far more familiar. (It is kept as the only exception where familiarity beats rule consistency.)
> Data-structure-related types use PascalCase.
> Here Disctionary, Array, Module and so on are data structures, but they are not special data structures other than Yulist — they are simply Yulists all the same. So it doesn't matter if you set the type of a Disctionary to Yulist.


**sizeT**: index-related. In `a[1]`, **the 1 is a sizeT**. For reference, sizeT belongs to int. That is, just as Array[...T] belongs to Yulist, sizeT belongs to int. But **using a sizeT like an int is an error**. However, **using an int like a sizeT is not an error.** Why does it exist? When making something like an array with Yulist you'd have to make the type with key as int and value as any, but then the problem is that with key as int it is understood as a dictionary form of key-value with an int key rather than just an index. But if you make the key's type sizeT, you can define the Yulist like an index.

naming is a peculiar type in that it comes directly without being wrapped in `""`. The namings of an argument function come in the form `...naming`.

There are **falsy and truthy**. But in a conditional expression all falsy things behave the same, and in a conditional expression truthy things behave the same too.

nothing and NaN are both falsy values. A Yulist is truthy whether it's empty inside or not. Because when you make your own data structure with Yulist there may be times when it must always be truthy. If you want to know whether it's empty you have to use the .isEmpty function. If you want to know whether a char or string is empty like '' or "", you just have to use `== ''` or `== ""`.

The downside is that `if (Yulist.isEmpty())` can get longer, but even when empty it is one data structure to begin with and has Interception built in, so it's seen as truthy. The reason 0 is falsy is that 0 is a value too, but calling it falsy is a bit odd. The reason '' or "" is truthy is the same.

For reference, `'a' == 97` is false, because the two have different types. If you want to make `'a' == 97` true, you do `'a' ~= 97`.

**never**: the value itself simply doesn't exist; there's just no value, there's no information either, it just isn't holding information and there's no space to hold information and no information itself. It isn't in memory at all. `():{}` isn't never either. It's more like `var never :: never = ;`. That would actually be a compile error, but if you were to express that never, it feels like that. And since it's a value that must not exist at all, using PascalCase, which means something is equipped (in Headlot, if something is fairly well equipped it uses PascalCase), felt a bit off, so camelCase is used.

**any**: it isn't just turning off type checking. All types simply come out of this any. That's any's internal implementation. And any here is used when anything may come here; it isn't for use when you don't know the exact type of something. As an example there's `typeof[any]`. A value of any type may come. That is, you use it when you take some value and it doesn't matter what type it is.

// TODO: think about how to express Headlot's complicated argument-function-based function system as types.

### Type magic

In Headlot a name does not carry functionality (name magic forbidden, 1-B #3). Instead the type carries the functionality — this is **type magic**.

> An IOP-family feature

**The way a value is evaluated is decided by the type declared in the spec.**

| Declared type | What you receive |
|---|---|
| (default) | the evaluated value — `i < 3` → `true` |
| condition | the structure of the expression — `i < 3` → first = i, operator = Operator.LESS_THAN, second = 3, result = true; .get() tells you the current result of that condition.|
| expression | it's an expression. `1 + 2` is an expression. `1 + 2 > 3` is a condition, and doing type magic with expression on it is an error. |
| naming | the name itself — `VAR` → the name VAR. Even if there's a variable with the same name, the name wins |
| anyVar | a dynamic variable; the current name is `.name`, the value is `.value`, the type is `.type`. Think of it exactly like variable[T]. |
| variable[T] | receives the variable itself; `.name` is the variable name (it's a naming), `.value` is the value, `.type` is the type. |
| typeof[T] | receives some type as a type. That types are first-class citizens, that types are values too, is this. |
| would[T] | a value that isn't in T shape yet but will become T with more work. Running `.complete()` finalizes (seals) it as type T |

**Types are values too.** In Headlot types are first-class values — `typeof[T]` is a value. So there is no separate comptime feature (keyword): compile-time type handling is **done by type magic**. (The 'comptime' expressions left in the document are not Headlot features but merely mentions of external lineages like Zig.)

**would[T] details:**

- **Meaning:** a value that isn't in this shape (T) now but will become T with more work. e.g. a value in the middle of being filled in field by field as a Yulist — it isn't a completed T shape yet.
- **`.complete()`:** a function that appears automatically on would[T]. Running it **finalizes that value as type T**. From this point on it's treated as T.
- **Why:** when setting something up step by step toward a target shape, it shows "not complete yet / complete" in the type. Now that class has been removed, it plays the role of a **creation primitive** for building objects step by step (transition from an incomplete value during creation → a completed T). The type blocks using an incomplete value as if it were a completed T by mistake.
- **Undecided:** handling of `.complete()` failure (shape not satisfied), the boundary of what can and can't be accessed on a would value.

**condition details**:

- The fields are references, not values — re-evaluation is possible. (The `ref(< condition.first = i; condition.second = 3; >);` model)
- For a complicated expression you get a list of sub-expressions with condition.equations (type `(...condition)`).
- **condition vs expression — same expression, different layers.** When looking at an expression like `1 + 1 == 2` that has both an operator (`+`) and a comparison (`==`): if taken as `condition`, the arithmetic part is evaluated and the comparison structure remains → `2 == 2` (first=2, op===, second=2). Taking the same thing as `expression` is **an error** — expression takes only a pure arithmetic expression (calculation and result) and cannot contain a comparison (`==`). That is, **condition = the boolean/comparison layer, expression = the arithmetic layer**. (Why: the two types capture different layers, so when the layers don't match it errors instead of quietly crushing it — principle 3 and cost honesty.)
- Short-circuit: equations are evaluated from the left. and stops at the first false, or stops at the first true. (Preventing division by 0 in `x <> 0 and 10 ~/ x > 1` hangs on this.)
- Performance: in an expand context the structure exists only at compile time, and at runtime only machine code remains. Interpreting the structure at runtime is Smalltalk-style slowdown — this sentence is the performance defense line.
- Escape: a condition contains the variables of its own country — treated the same as a closure. The only path out of the country is send, and when you send, the captured variables migrate along with it. The migration is a snapshot at that moment.
- Honest downside: looking only at the call site (`while {i < 3}`) you can't see whether there's a capture — the spec is the source of that information. In exchange the call site is always clean. (Explicit notation like `while condition (i < 3)` was rejected as more complicated.)

**expression details**:

- **Meaning:** an expression, a formula, that is, a polynomial.
- **Why:** it's used when you have to take a plain polynomial instead of an equation and taking it as a condition won't do.
- **Usage:** first, with .result you can get the result of this polynomial. For `2 + 4 - 2`, .result is 4. And if there are variables in it, as in `I + 3 - X`, .result is the result at the time this expression was first taken. So it stays the same even if the variables' values change. Also, if you use the .get() function it gives you the value you get by computing that value now. Also .struct is like `[2, Operator.PLUS, 4, Operator.MINUS, 2]`. And if there are variables in that polynomial it becomes [variable I as a variable, Operator.PLUS, 3, Operator.MINUS, variable X as a variable]. Also here .struct is the structure at the time it was first put in, and .structNow() gives the current structure. The difference is that instead of the variable as it was when first put in, the variable in its current state comes out.

**variable details**:

- **Meaning:** takes the variable itself; just this variable itself, just the variable itself.
- **Usage:** `.name` is the variable's name, `.type` is the variable's type, `.value` is the variable's value, and if you passed a literal it's an error.
- **Why it exists:** for example when validating whether this variable fits a format, an ordinary language often uses `lambda: variable`, and when it even takes the name it takes the name as `"name"` and can even take the type as `"int"` in that style, so this was made.
- **Downside:** if you put in a literal by mistake it errors, and since you can't see whether there's a capture just by looking, it's easy to error by mistake.

**naming details**:

- **Meaning:** takes a name. When making a variable you don't do `var "x" :: int = 1;` but `var x :: int = 1;`, and the x isn't wrapped in anything. Because **it's a name, a naming.**
- **Usage:** just set the type to naming. When putting in a value, set it with no quotes and nothing else, like `aaaa`.
- **Why it exists:** taking a name as a string is the worst.
- **Downside:** it looks like it's taking a variable, so if it isn't clearly visible that this is type magic with naming, you might not realize by mistake that this is a naming.

For reference, naming also has dot.case. It's used when finding a value inside here, and inside the naming type, in dot.case, both dot and case are namings, so **there's a naming inside a naming.** And why does it exist? Adding it to naming makes it possible to express a bit more. And naming is the name type of a value that has one name, and in a place that doesn't take that naming as a naming type, it just looks for the variable or constant of that naming. But when looking for that, accessing via a naming somewhere — it does make some sense that it can't be found by that naming, but then you actually need something like a workaround: in the part that takes arguments as naming you **simply can't write name.aaa directly and have to put in a lambda that looks up that key and returns it.** So that's why dot.case is possible in naming. And in exchange something like dot["case"] is not allowed. Because that would be a string inside a naming, and that would be strange, it makes no sense, they're entirely different types; something like that would need a workaround, but in fact if it isn't looking up a key by naming, then it isn't really the name of one value being looked up, it can be anything. Because naming makes it impossible to directly put a naming taken as Input into some Input. That is, an ordinary string can be taken directly and used to look something up like `aaa[str]`. But if you take a naming called aaa and write aaa.aaa, it doesn't look it up with the naming value in the aaa variable inside aaa; it just looks up the name aaa inside aaa. This is naming's nature, and because of it, allowing dot["case"] in naming would break the rule, which is why dot["case"] is not allowed.

But there's one problem. The characteristic of naming is that you input that naming directly into the code — that is, it's used only when making names usable in this metaprogramming code, not for things like country names in a game. But if you convert a string to a naming with changeType, you could turn something taken as input into a naming, or turn a number into a naming by attaching a single character in front (like the current OS time). So this naming is similar to never. Like never, type conversion is impossible. Like never, it can't be a value at all. It just exists for things like this function's name that have no meaning in an ordinary programming language. (For reference, in Headlot you can know things like this function's name via IOP, but what's being talked about here is ordinary use.) So type conversion with changeType is impossible and doing type magic on something that is a naming as a condition is also impossible. (You can pass a value for things like making a function that determines whether a function is a yield function, so that a function ending in Async is a yield function, but taking Input from the user as external input isn't possible.) And also, if you want to put a variable of naming type somewhere as the naming value that was put into that variable, you actually have to use the let magic constant. Store the naming value taken through this variable with let, then put it directly into the function that takes this naming type. let has higher priority than naming processing at the AST stage. It looks at a magic constant declared with the naming type, and if that is being put into some function with the same name as that magic constant, that magic constant's naming value is passed. (And since the type comes first, putting an int magic constant declared with let into a place that is a string is not allowed.)

**typeof[T] details**:

- **Meaning:** when taking something as a type, the type for it
- **Usage:** take it as typeof[T]. Then even if there's already a variable called string, putting in string gets you typeof[string]. The most used one is typeof[any]. This is good when you have to specify some type directly.
- **Downside:** same as naming. It's just hard to tell what variable is really being put in.

Why is name magic forbidden while type magic is a principle: a name is an appearance, and a type is declared structure. Type magic keeps "functionality is decided only by explicit structure" (1-B #3) exactly.

> Type magic is not type conversion. Type conversion exists separately. Type magic says "take this value in this way", and that is not type conversion.

(Precedent: in C#, if you assign a lambda to the Expression type, an expression tree is captured instead of code — LINQ stands on top of that. naming capture is in the lineage of C#'s nameof and Lisp's quote. Being decided by the type declaration alone is the Headlot way.)

The way to write a function is

.

If `...` comes before a type it means there are several values of that type.\
Examples: ...any, ...boolean, ...regex

The type notation of Yulist (arrays, linked lists, dictionaries, all of them — → Yulist section) is `Yulist[...]`.

```headlot
Yulist[init = ...]
```

The previous three-way notation of `( )` (array), `[ ]` (linked list), `{ key: value }` (dictionary) is discarded (→ CHANGELOG). Because the type table already has `byte[type]` and `typeof[type]` — the axis of **square brackets = type parameters** already existed, and `Yulist[...]` rides on that axis. If anything, the three-way notation was the exception that deviated from that axis.

This type magic isn't only condition or expression. Whatever you do type magic with, it just gets changed into that. Precisely, if you specify the type as some type, that variable comes to take that type.

Honest cost: the most common type gets longer (`Yulist[...string]` vs the previous `(...string)`). Since the target is power users, consistency wins.



### Literals

- **Integer**: `1 2 3 4 5 ...`
- **Real**: `1.2d`, `1.3d` — the `d` suffix means a double literal. `d` is short for double so it's used only for double — if you need single precision you cast with `middle[double]`. If there's a receiving type, type magic beats the suffix (e.g. `var x :: middle[double] = 0.5d` → 32-bit).
- **String**: `"..."` or `«...»`
- **Character**: `'.'`
- **nothing**: `nothing`
- **NaN**: `NaN`
- **True / false**: `true` / `false`

String formatting: `` `...` `` and to put a value in here it's `` `({...})` ``. Originally, if you used only `{}`, then to use `{}` you'd have to write `{{}}`,\
which is both awkward to look at and becomes escape hell.\
So instead of `{}` it became `({})`. If you want to use `({` or `})` inside,\
`\fl` (format left) gives `({` and `\fr` (format right) gives `})`.

Also, the reason the strange symbols `«...»` exist for strings is not for originality but to prevent escape hell like \sq, \dq. For reference, if there aren't many quotes or double quotes, using escapes is recommended,\
and when `"` or `'` is used a lot in a really long string, using «» is recommended.

Formatting with %f is possible. When is it used? Sometimes when you get some string and have to format it accordingly. So for example there's a function called getPlayerUserName, and this function spits out only one string. You can use it by formatting that directly with %f and formatting inside it.

```headlot
var UserName :: string = getPlayerUserName().format(PlayerName, PlayerId);
```

Like that.

How it works: first put %f in the string, and when you have to format, use the .format function. For example, `"Today I ate %f %f.".format(3, "apples");` becomes "Today I ate 3 apples."

**Binary, octal, hexadecimal numbers**:

```
binary:      0b e.g. 0b100101
octal:       0o e.g. 0o242322
hexadecimal: 0x e.g. 0xffffff
```

In hexadecimal, uppercase like 0xAB or mixed case like 0xAb is also possible.

Exponent: numbereexponent

Escapes:

```
'\n'                                // line break
'\t'                                // tab
'\r'                                // carriage return
'\\'                                // backslash
'\q' (short for quote ')             // single quote
'\qq' (short for quote quote ''      // double quote
that is, the " double quote)
'\uUnicode'                         // unicode
```

Here unicode can also be `'\u{unicode}'`, and the advantage of `'\u{unicode}'` is that the unicode is shown as a number so things like `'\u{0xab}'` are possible.
And binary notation like `'\u{0b1011}'` or `'\u{0o257}'` is also possible. Anything that's a number works. So when there's arithmetic or the like, using `'\u{unicode}'` is recommended.

Multiline:

```
"""
content
"""
```

And you can put `_` inside numbers.

Examples:

1_000_000\
2_321_424

Numbers can be expressed a bit more easily.

Regular expression:

`/[a-zA-Z0-9_]/`

> Except for some literals, camelCase is used.

### nothing

nothing is most similar to ordinary null. But it isn't null or None. It's actually closer to NaN. First, in programming languages null is just absence. The pointer points to nothing.

In ordinary languages null causes bugs and blows up servers. But nothing isn't just "the pointer points to nothing"; it indicates that there is no value currently passed. It was taken from noop, which was made while planning NoopScript.

nothing is contagious, and `1 + nothing` is nothing. The point where this ends is ifNothing.

Also, you'd think you have to keep checking every expression for whether nothing got in there, but actually you don't have to check. Because nothing carries the nature of NaN. NaN is contagious. `1 + NaN` is NaN. But you don't check every time whether there's a NaN. nothing is the same. It makes use of this nature.

Also, nothing is entirely the information that there's no information, the information that it's an exception; if you do changeType("aa", int), instead of an error, the information nothing, meaning an exception, comes. But here the situation of having no information or being an exception can come at any time. So nothing is possible in every type.

// TODO: how nothing works, build the mechanism of nothing

### Pointer

If you want to get the pointer of a variable you do `&<variable>`, and the type is Pointer[T].

Example:

```headlot
var X :: int = 1;
var PointerX :: Pointer[T] = &X;
X = 10;
print(PointerX); @= 10
```

For reference, the difference from ref is that with ref the variable isn't originally a Pointer but can hold a Pointer, while `&<variable>` can hold the pointer itself as a value. That is, ref puts a pointer into a variable, and `&<variable>` is the pointer itself. Also, ref doesn't need the type to be Pointer[T] — it returns that pointer via interception, so the type isn't Pointer[T] but just T, the type — whereas `&<variable>` is the pointer itself, so it forces the type to be Pointer[T].

### Operators

Operators are classified as special countries. (→ see 1-C "Country / small country": they use special symbols as names and can be used in every argument function without being bound by context.)

- **OR, AND, NOT**: or uses `or`, and uses `and`, not uses `not`.
- **Bitwise**: bitwise AND is `bitand`, bitwise OR is `bitor`, bitwise XOR is `bitxor`, bitwise not is `bitnot`

Addition is `+`, subtraction is -, division is `/`, multiplication is `*`. The remainder of a division is %, the quotient of a division is `~/`. Exponentiation uses `^`. In `x ^ y`, x and y just need to be numbers (int or double). (// TODO: rule for the result type of a double exponent) Joining two strings uses `$`. `$` symbolizes joining. It's used like this: `"abc" $ "def"` gives `"abcdef`. The reason `$` is joining is that it just gives that feeling. (It really does give that feeling)

Equal is `==`, and equal including type conversion is `~=`. Not equal is `<>`, and not equal including type conversion is `<~>`. Greater is `>`, less is `<`, greater or equal is `>=`, less or equal is `<=`.

When not-equal was made `<>` you might have this doubt: doesn't `<>` fail to give the sense of "different"? First, there are very many languages that use `<>` to mean different. Representative ones are SQL and Pascal. Also, ! feels like it doesn't give the sense of different. Because ! feels like emphasis and there have been few times I got the sense of "different" from it. Also I think `<>` gives a sense of mismatch, so it gives the sense of different.

Right shift is `rshift`, left shift is `lshift`.

0.0d / 0.0d is NaN, 0.0 / 0.0 is also NaN, and 0 / 0 is an error.

And the ternary operator.

`condition then result when the condition held else result when the condition failed`

That's it.

Example:

```headlot
1 == 1 then
   print(1);
else
   print(2);
```

Something like this is also possible. (Writing it that way is good for readability, and whitespace has no meaning at all in Headlot, so writing it that way is good for readability.)

And also

```headlot
Input == "exit" then
   Line.addLine("exit");
else
   Line.addLine("continue");
```

### Operator precedence

From highest:

1. `( )` parentheses
2. `^` — **right-associative** (math convention: `2 ^ 3 ^ 2` = `2 ^ (3 ^ 2)`. And `-2 ^ 2` = `-(2 ^ 2)` = -4)
3. Unary: `bitnot`, sign `-`
4. Multiplication group: `*` `/` `~/` `%` `lshift` `rshift` `bitand`
5. Addition group: `+` `-` `bitor` `bitxor`
6. Comparison: `==` `~=` `<>` `<~>` `>` `<` `>=` `<=`
7. `not`
8. `and`
9. `or`

Only `^` is right-associative; all the rest are left-associative. A comparison chain (`a < b < c`) is a compile error (it becomes a comparison of a boolean and an int, so the static types naturally catch it — it's just stated explicitly).

Why:

- and is above or — Boolean algebra convention (and = product, or = sum). If they were the same rank, `a or b and c` would read differently only in Headlot and everyone would be surprised.
- Bitwise operations are in the arithmetic groups — the placement C regretted for 40 years (the `x bitand mask == 5` trap) is what Go fixed. Headlot is statically typed so an error occurs instead of a silent bug, but the inconvenience of being forced to use parentheses remains, so they're put in the arithmetic groups.
- bitnot is unary so it's at the top, and not is below comparison like in Python — `not a == b` reading as `not (a == b)` is natural.
- Since and/or are lowest, they become the top decomposition layer of condition.equations — consistent with type magic.

// TODO: extend the operators further.

### Comments

First, comments are `@...` for easy reading. @ gives a sense of emphasis and ... gives a sense of trailing off, and also @ is darker than something like `#...` and so gives much more of a comment feel.\
And // puts your fingers in a somewhat awkward position to type, whereas @ is 2, a very comfortable position. Shift is used a lot too so it won't be inconvenient.\
Also . makes the hand a bit awkward, but once you're used to it it's very comfortable to write. For multi-line comments, to give the feel of a storage box

To just show comment examples:

```headlot
@... TODO: finish this
```

```headlot
@<<
   Things to do today:
   finish some TODOs and
   do some structural design
>>
```

is used.

There's also something called an expected behavior comment.

It's a comment saying "this is probably going to be the result."

`@=` is the expected behavior comment; to just show an example:

```headlot
print(5) @= 5
```

This is an example of the use of the expected behavior comment. Or

```headlot
if (5 == 5):{ @= runs because it's true
   print(5) @= 5
};
```

It can be used like this too.

Also `@TODO` is a TODO comment. That is, a comment where you write a TODO.

```headlot
@TODO make this whole algorithm O(n)
```

Like that.

And `@~~` is a file comment. It explains what this file does.

```headlot
@~~ this file is the terrain generation module
@~~ handles the core features
```

Like that.

> For reference, @ doesn't mean comment; it means it has no effect at compile time.

### Variables, constants, dynamic variables, magic constants

`var`, `anything`, `const`, `let` are valesto. You can see valesto in detail in the **Valesto** section.

First, here's how to make a variable.

```headlot
var x :: int = 1;
var p :: string = "Hello, World";
```

The places where the variable names are are all aligned and the types are aligned too, so it's comfortable to look at.

```java
int x = 1;
string p = "Hello, World"
```

In other languages it's like this, where the position of the variable name is uneven, so it's hard to look at.

And if you want dynamic

```headlot
anything x = 1 :: int; @= int is the current type, not "this is the type forever".
anything p = "Hello, World" :: string; @... same for this one.
```

is the structure

By making the character count differ from var, it gives a different feel from an ordinary variable (a static variable).

```headlot
var x::int = 1;
```

is also possible; for readability the

```headlot
var x :: int = 1;
```

form is recommended.

Making constants is simple too.

```headlot
const x :: int = 1;
@... for readability the form `const x :: int = 1;` is recommended
const y::int = 2;
```

Same for this one, and by making the character count differ from var and anything it gives a different feel.
const requires a type. And any is also possible as the type.

And anything, var, and const are all first-class citizens. I wrote this down in case someone misunderstands them as second-class citizens because they're special function Keywords.

And here's how to change an anything or a var.

```headlot
var x :: int = 1;
x = 2;
```

Like this, var can change its value simply. And for an anything dynamic variable

```headlot
anything x = "string" :: string;
x = 2 :: int; @... when changing an anything dynamic variable, if the type changes too you have to write down what type it is.
```

Also, a variable whose type is any and an anything are strictly different.

First, a variable whose type is any doesn't need you to write what type you're changing it to,\
while anything requires you to write what type you're changing the value to.

And the decisive difference is that the compiler sees a variable whose type is any as simply a static variable whose type is any,\
and sees anything as just a dynamic variable.

Also there are no operators like += or -=. Because with += the intent of "add this much" isn't very visible.

And a magic constant is a constant that exists purely for type magic. To be precise, one that's also fast in performance

First, here's how to declare it.

```headlot
let NUM :: int = 1;
print(NUM);
```

But there's a difference from a constant. After compiling it becomes

```headlot
print(1);
```

Precisely, in the AST node all those NUM parts get changed into the value 1.

When is it used? When you've done type magic and the type is any so you can't put in something like a naming directly.

```headlot
Line.addLine(want to print a naming);
```

But at this point

```headlot
Line.addLine(aaa);
```

this looks for a variable called aaa instead of the naming aaa, and errors if there's no variable. But here Headlot doesn't have a separate Line.addLine(naming(aaa)); you put in the value declared as a magic constant directly. Like this.

```headlot
let NAME :: naming = aaa;
Line.addLine(NAME);
```

Then aaa in the naming type is converted into an AST node, that let declaration part disappears, and in the Line.addLine(name) part, name changes into the value aaa of naming type.

And though its use differs from a constant, when storing a magic number

```headlot
let MAX :: int = 10;
...
```

it's used for that too, so its use is almost the same as constants in other languages. So this magic constant is **sometimes just called a constant.** In fact it's **included in the constant family.**

And the naming convention is SNAKE_SCREAMING_CASE. Because when declaring a constant that stores a magic number, other languages almost always use SNAKE_SCREAMING_CASE too.


#### Variable (static)
> var [variable name] :: [variable type] = [variable value];

#### Dynamic variable
> anything [dynamic variable name] = [dynamic variable value] :: [current type];

#### Constant
> const [constant name] :: [constant type] = [constant value];

#### Magic constant
> let [magic constant name] :: [magic constant type] = [magic constant value];

Naming conventions:

#### Variable (static)
> PascalCase

#### Dynamic variable
> camelCase

#### Constant
> camelCase

#### Magic constant
> SCREAMING_SNKAE_CASE

And in Headlot, "variable" means a static variable, and a dynamic variable is called a dynamic variable separately.\
Static variables give a strict feel so PascalCase, with an uppercase letter from the start, was chosen

Dynamic variables give a slightly loose feel so camelCase, with no uppercase at the start, was chosen

For constants, SCREAMING_SNAKE_CASE by constant convention, or camelCase to make it easy to distinguish from the most commonly used ordinary variables, static variables, was chosen.

### Dynamic variables

Dynamic variables are a concept that exists only in this language so you'll wonder why they exist; they exist because **the type of a value that came in from outside isn't clear**. Even with type inference, something that was "N/S" as a string may turn out to have been an int, so dynamic variables exist.

**Type inference whatType**

The base form is this.

```headlot
anything project = https.access("https://github.com/discunderbar/headlot-lang") :: whatType(); @... the reason https.access takes its argument as a string is that taking it as a naming would error because of the special characters.
```

Here the whatType function is a small country, that is a function, that only this anything, that is the dynamic variable, has, and it infers what the type is. The value currently put in here

And it's fine if it sees "N/S" and infers the type as string. It's fine even if the type changes entirely. Because it's a dynamic variable so the type can keep changing.

```headlot
anything project = https.access("https://github.com/discunderbar/headlot-lang") :: whatType();
project = https.access("https://github.com/DiscUnderbar/variable-number-binary") :: wahtType();
```

Like this, whatType is used when using type inference in a dynamic variable or in a dynamic variable reassignment.

**Type freezing**

You can finalize the type of a dynamic variable. For example you can use it when you're not going to change data brought in from outside any more, or when something that was an int has to be converted to a string after all the work is done.

```headlot
anything project = https.access("https://github.com/discunderbar/headlot-lang") :: whatType();
@... did various things with the project function and now the type won't change any more, but it'll keep being used
project.typeFreeze :: whatType();
```

That's how you do it.

> Precisely, it converts an anyVar, that is a dynamic variable, into a static variable and finalizes the type.

### Built-in functions

#### if

The function most used as an example of the use of countries and the use of argument functions. It's the if statement of an ordinary language.

Let's start with the grammar.

```headlot
if (condition):{
   what to run
} else if (condition):{
   what to run if the condition fails but this condition holds
} else {
   what to run when the condition fails and even the else if condition fails
} ifNothing {
   what to run if the result of the condition is nothing
};
```

It's an if statement of ordinary structure, and in else, the if is taken as a naming. Also the condition is taken with `condition` type magic — the structure of `{i > 3}` (first/op/second) comes as it is.

#### Loops (while / repeat)

```headlot
while (i < 3):{
   ...
   break;        @... a small country of FuncKind.LOOP. continue is also a small country of this loop country.
};
```

`while` takes a `condition` and runs the body while it's true. `break`/`continue` are small countries that exist only inside this loop country (→ return/break/continue = small country + label). For a fixed count, `repeat (n):{ ... };`.

**There is no `for`.** What for does is practically the same as while, so it hits #10 (no duplicate similar features). Traversing data structures will later be handled by **Yulist traversal functions** of the `forEach` family — traversal is the data structure's job, not a loop's.

#### switch (value branching)

```headlot
switch ("Luau"):{
   case "Luau" ( ...; break; );
   case "Python" ( ...; break; );
   ifNothing ( ... );   @... when no case matches
};
```

> There are no events (emit/when/give) — they overlap with 1-D actor messaging (`send`/`ask`/`on`/`receive`) and request-response, so they hit #10 (no duplication); signals and request-response go through messaging alone. (→ CHANGELOG)

#### Other built-in functions

Output is `print` / `Line.addLine` (→ output section). The rest (input, Yulist methods like `.isEmpty`, type queries) mostly go into the standard library, and **only what absolutely needs the compiler floor** stays built in (minimizing the built-in list — 1-B direction). The final list is undecided.

There's loop. `loop {}` means the same as `while (true):{}`. It's just put in for readability.

### Functions

**The two uses of a function (terminology).** The same argument function is called two things depending on how it's used. **These aren't different mechanisms, just a distinction of use.**

- **Three-mechanism function** — a simple function that uses only the three slots of parameters, body, and return. (func always uses the return slot, so even when it's nothing it's three slots → always exactly three, so "three" fits perfectly.) e.g. `greet(name)`.
- **Multi-mechanism function** — a systematic function that additionally takes and handles mechanisms like countries, small countries, and values. e.g. `if`, `while`, `switch`, `special`.

And the way a **three-mechanism function** is defined must never become complicated because of the way Headlot's complicated **multi-mechanism functions** are defined. If it did, Headlot would end up being a language that makes even unnecessary things complicated.

In Headlot functions are really complicated. Almost at the level of a dialect. So to prevent that we use something called FuncKind. FuncKind is the kind of the function. A function that gets something is FuncKind.GET, a function that does something is FuncKind.DO, a function that does something and returns is FuncKind.DO_RETURN. And DO_RETURN can be used on every function. Also a declaration statement is FuncKind.MANIFESTO. Also something that sets something is FuncKind.SET.

**Why FuncKind exists**: if there were just functions it would naturally look like a dialect and become like Lisp. So to solve this we made FuncKind. First, FuncKind is the kind of the function.\
If there were no FuncKind, when you see this function you'd have to **Jump** all the way to where this function was first declared just to know how to use it. To solve this, FuncKind makes functions of the same FuncKind use the same form.

For example **FuncKind.MANIFESTO**, being a declaration statement, uses this form.

```headlot
<function name> <name of the thing being declared> argumentFunction;
```

That's the form.

Also the loop **FuncKind.CONTROL.LOOP** uses this form.

```headlot
<function name> argumentFunction;
```

Also the argument function is taken in form 3.

And the conditional **FuncKind.CONTROL.CONDITIONAL** uses this form.

```headlot
<function name> argumentFunction;
```

Also the argument function is taken in form 3.

And the control statement **FuncKind.CONTROL** uses this form.

```headlot
<function name> argumentFunction;
```

And the argument part of the argument function does type magic as condition. Also the argument function is taken in form 3.

Like this, a FuncKind uses a specific form. Precisely, it does a specific behavior. The user just looks at this function's FuncKind, thinks about what that FuncKind does, and writes according to that form.

But actually the usage is almost all similar. Still, the person writing distinguishes it.

And here's **how to declare a function.**

First, use func. You can make a function using func.

```headlot
@>> what this function does (in the IDE this comment part is automatically shown when using the function.)
@>> a function that lets you create functions in the new form
func functionName (arg :: type, second arg :: type ...):(
   setFuncKind (FuncKind.CONTROL.CONDITIONAL); @... if absent, automatically DO_RETURN

   what the function does (country 1)
   ...
   
   [CONDITION<type: <condition>>]:[
      CODE<<condition.get() == true> -> run>
   ]self;
   
   @... what self is: it's the argument function that came into this current country 1. In if ():{};, if if is country 1, then ():{} comes in as a mapping real func.
   @... for reference, the done function here ends this function. Like done();

   routing(the values to pass from this country 1 to country 2 via inter-country communication);

   country countryName (which number country):{
      the things done if this country exists (for reference, here done ends this country immediately)
      if (namings[1] == if):{ @= namings, that is, which namings came after this country. Here the first one (namings[0] is this country's name, so if the country is else, namings[0] is else)
         [CONDITION<type: <condition>>]:[
            CODE<<condition.get() == true> -> run>
         ]self; @... here too, self is the mapping real func that mapped what came in as the argument function.
      };
   };
):(return type);
```

And here's an example function declaration.

```headlot
using hl;

@~~ example three-mechanism function declaration

#main
module SmallMath();

@>> a function that adds two numbers
#SmallMath.add func add (X :: int, Y :: int):(
   setFuncKind (FuncKind.GET);
   return X + Y;
):(int);

func sumSquareDigits (Num :: int):(
   var Sum :: int = 0;

   while (Num > 0):{
      var Digit :: int = Num % 10;
      Sum = Sum + (Digit ^ 2);
      Num = Num ~/ 10;
    };

    return Sum;
):(int);

@>> a function that tells whether a number is a happy number
#SmallMath.isHappyNumber func isHappyNum (Num :: int):(
   while (Num <> 1 and Num <> 4):{
      Num = sumSquareDigits(Num);
   };

   if (Num == 1):{
      return true;
   } else {
      return false;
   };
):(boolean);
```

And here's a multi-mechanism function declaration.

```headlot
using hl;


```

// TODO: write out the full example code for that multi-mechanism function declaration

Also, if a function is completely empty

```headlot
func void ():():();
```

then everywhere that uses the function, the use of the function disappears.

```headlot
func void ():():();

void(); @= disappears during compilation
```

For reference, when compiling, expand is all compiled first, and then the removal of these empty functions happens.

And on the side that uses this empty function, erasing the function-call code entirely at compile time if the function is empty is called **empty function killing**. Also, if this function is an empty function but you don't want it to get empty-function-killed, you do this.

```headlot
func void ():(
   --void;
):();
```

And why is it special syntax instead of a function like void? Because if the void function is empty, the void function itself ends up getting empty-function-killed too, and then this function dies as well, so it was changed to the special syntax `--void;`.

And also, why does this --void exist? For when you want to keep this function — that is, maybe this function was made on purpose, that is, maybe this empty function was made on purpose. What that means is that this empty function might be needed at some point, like when you pass these functions as arguments and want to easily make a function that returns nothing, so it was made for that.

// TODO: finish everything

/*

// TODO: change the function call method so the speed is really fast

*/

### lambda, mu

lambda makes a function in the manner of turning that expression into an expand, like Zig's comptime, and mu isn't like Zig's comptime but is a real abbreviation of a function.

// TODO: finish

### Valesto

Valesto is a value declaration statement, that is, the thing that holds a value = the thing you declare like this. What's different from a Manifesto function is that it's used when declaring something like a storage that holds a value, like var and const, and the name Valesto came from Value + Manifesto, which became Valesto.

As an example, here's how Valesto is declared.

I'll show code that uses Valesto to make a type-inference-based variable declaration statement called let.

It goes like this.

```headlot
let x = 1;
let y: int = 1; @... type inference is also possible; for reference this uses : and it's type inference and it goes in by gentleman's agreement.
```

I'll make something like this.

// TODO: finish this Valesto. Put in the concept completely, and this Valesto probably has to recognize : as well. It has to recognize :: too, but the reason :: is the type notation in Headlot was that : gives a dynamic feel and seems like it would have type inference. Since in this Valesto there will also be dynamic things that declare while inferring, make : possible too

### Why Yulist exists

Headlot has no class. Just as Luau expresses objects with **table + metatable** without classes, Headlot expresses them with **Yulist + Interception (hooks)**.

The reason class was removed is that class and Yulist are both "structural types that bundle fields + behavior", so it hits #10 (no duplicate similar features). Yulist already has hooks (Interception), representation, and performance (expand), so if objects are built on top of it too, there's only one thing to learn and no duplication. (If you keep data structures and objects separate, you have to learn both.)

- And the things that appear as one of the built-in data structures, the things that appear as data structures, are all **made with Yulist**. They're not some other special data structures; since it would be hard to make a List Yulist and a Dict Yulist yourself in every project, those frequently used patterns are all just implemented using Yulist.

**Mapping (Luau → Headlot):**

| Luau | Headlot |
|---|---|
| table | Yulist (data + slots) |
| metatable (`__index` etc.) | Interception hook |
| method | a **function-value** held in a Yulist slot (functions are first-class, principle 0) — `moveTo` is a function-value inside the Yulist |
| constructor | create hook + `would[T]` — an instance starts as `would[Point]`, fills in fields, and is sealed into `Point` with `.complete()` |
| type hint | **a named Yulist = a type** — `var userPos :: Point = ...` (like py's `user_Pos: Point`) |

**What was thrown away (honesty):** the `class` / `new` / `extends` / `self :: would[T]` syntax. These now have to be rebuilt with Yulist.

**Composition instead of inheritance — decided.** Yulist has no inheritance (extends). Instead, behavior shared by several objects is pulled out as a **component (unit)**, and each Yulist takes and uses that component.

Example: if `Point2D` and `Point3D` use `reset` in exactly the same way, make `reset` a component and put it in both `Point2D` and `Point3D`. Without a parent-child relationship, **only what's shared is pulled out and each one includes it.** (Since functions are first-class (principle 0), putting a component in a Yulist slot is natural.)

- **Why:** inheritance has the **advantage of a clear structure** (what inherits what is visible in a single tree). But inheritance sometimes makes code more complicated instead (the hierarchy gets deep and the branches tangle). Since Headlot's purpose is to lower implementation complexity, composition is chosen instead of inheritance, which risks getting complicated. Luau's metatable `__index` chain (imitating inheritance) is also rejected — no imitating, going straight to composition.
- **Giving up (honesty):** the "structure visible at a glance" benefit of inheritance is put down — with composition you have to trace which component some behavior came from, so it isn't as immediate as an inheritance tree.
- **Undecided:** the exact syntax and semantics of putting a component into a Yulist (inclusion? delegation?).

**Team — the unit that shares the same components.** A unit that shares the same components is called a **team**. Some team shares these components, another team shares different ones. (Why: to **make the relationships between data structures clear** — with composition, components scatter easily, and bundling them into a team reveals what belongs with what.) A component shared everywhere gets **`#public`** attached when it's made.

// TODO: team declaration syntax

**Still unresolved (replacement syntax undecided → // TODO 5, 6):**

- **self binding** — how a method (function-value) points at its own Yulist. Undecided.
- **Yulist definition syntax / instance creation syntax** — what will replace `new Point(...)`. Undecided.
// TODO: resolve all of these undecided items

If you move Point to a Yulist, roughly this is the picture (**conceptual sketch — syntax undecided**):

```headlot
@... defining a Yulist type called Point: fields x,y + function-value moveTo + create hook
@...   (definition syntax undecided — // TODO 6)
@... instance creation:
@...   start with would[Point] → fill x,y → .complete() → seal as Point
@...   (creation syntax undecided — // TODO 5)
@... method call: p.moveTo(...) — moveTo is just a function-value in a Yulist slot
```

> Note: in Headlot **types are values too** (`typeof[T]` is a value). So "a type = a named Yulist" is natural — types aren't treated as something special but handled as values.

### next, prev

Generally, languages like JavaScript or C++ say `i++` for "add 1 to the variable i". But this isn't good for readability, so a readability-focused language like Python has you write `i += 1`. But this is also a bit uncomfortable to look at.\
So the next and prev functions exist. First, next adds 1 to some variable. It also returns the added value.

Example:

```headlot
var i :: int = 1;

Line.addLine(next i); @... 1 + 1 makes i 2, and prints 2
```

And similarly prev is the opposite of next; it subtracts 1 and returns that value.

```headlot
var i :: int = 2;

Line.addLine(prev i); @... 2 - 1 is 1, and it prints 1, so it prints 1
```

### Output

Output is two functions: `Line.addLine` (general purpose) and `print` (numbers only).

print is exactly what the name says — pr + int — it prints only numbers. It started as wordplay but the reason it was kept is serious: the overlap between the two output functions was removed by differentiating their functionality (1-A #11 — remove the room where duplication appeared), and keeping zevra's name preserves the designer's signature.

Honest record: there are still two paths for numeric output — it's a recorded exception to #10 (reason: zevra compatibility + character).

zevra compatibility is partial: zevra's `print("text")` is an error in Headlot.

// TODO: print's numeric range (int only? double included?), whether it adds a newline.
(The history of the mix-up that produced two functions is in data.md.)

### job

A job can decide what this function, variable, Yulist, or section does, using the opening symbol `(<` and the closing symbol `>)`.\
If you want to point at only one variable, one function, or one Yulist, you use `#`.

For example, if you always want this variable to be referenced

```headlot
var x :: int = 1;

ref(<

var y :: int = x;
var z :: int = y;


@... variable declarations in this section are references

>);
var a :: int = x;
var b :: int = y; @... just a value copy

x = 5;

Line.addLine(x); @= 5
Line.addLine(y); @= 5
Line.addLine(z); @= 5
Line.addLine(a); @= 1
Line.addLine(b); @= 1
```

As an example a job called ref was shown, but there are many other jobs.

And here's how to use #

```headlot
var x :: int = 1;

#ref
var y :: int = x

x = 2;

Line.addLine(y); @... 2
```

For reference, by Headlot's `if /\s/ then continue` principle,

```headlot
var x :: int = 1;

# ref

var y :: int = x;

x = 2;

Line.addLine(y); @... 2
```

becomes the same thing.

Also, the things inside some job are not that job. What does that mean?

```headlot
#main
func main ():(
   var x :: int = 1; @... #main must not apply this far.
):();
```

So

```headlot
main(<
func main ():(
   var x :: int = 1;
):();
>);
```

even like this, main's influence goes only as far as the inside of main itself and does not apply to x.

Instead, a job that indicates a section does apply all the way inside, and this is when the kind is JobKind.Interval when the job is declared with its kind indicated.

The boundary between job and argument function: **a job does not create a country, a scope, or a lifetime. If it does, that's an argument function.** A job isn't a simple label but a marker that can change meaning (like a Python decorator — ref changes the behavior of `=` in that section).

// TODO: create the job declaration syntax

### Modules

A module is simply something that lets you get the Yulists, functions, and variables of another file.

#### How to make a module — id + #main

What a module hands out is **what `#main` points at**. This is why it was said that main can be a function, a variable, or a Yulist, anything — that is the representative of that file (what it exports).

**The id is decided by making a naming dynamic variable called id as a global variable** (the ID is taken as a naming):

```headlot
using hl;

global id :: naming = MainPos;

var X :: int = 0;
var Y :: int = 0;

#main
func getPos ():(
   return X, Y;
):();
```

In another file:

```headlot
take MainPos as getMainPos;

var X, Y :: ...int = getMainPos();   @= 0, 0
```

- **The global id variable** — the id of this file (module). If absent, the file name (excluding the extension) becomes the id.
- What you bring in with `take` is that module's `#main`. In the example above, `getMainPos` is the `getPos` function itself.
- **If the FuncKind of the function `#main` points at is `FuncKind.MANIFESTO` (a declaration statement)**, then when you take it, you get not the function itself but **what that declaration statement returns**. (A path for assembling module contents with a declaration statement and exporting them.)

#### Module — data structure

`Module` is one of the **built-in data structures** Headlot supports (alongside Array, LinkedList, and Dictionary). Creation:

```headlot
module moduleName();
```

If there's no id global variable, that file must put **a `Module` type as its `#main`**, and the name of that module becomes the id.

```headlot
using hl;

#main
module Pointer();

#module.Pointer
func newPoint (...):(       @... becomes a function belonging to the Pointer module
   ...
):(...);
```

- If you attach the **`#module.moduleName`** job, that function comes to live inside that module → from outside you call it as `Pointer.newPoint();`.
- That a module is a data structure means a module is handled like any other value (1-A #9 — don't separate user and system).

And main is the entry point, so if this module is a function it gets run automatically, without this code being called from anywhere else, so if this is a main used only as a module rather than as an entry point, you use main.pass instead of the main job. For example

```headlot
using hl;

global id :: naming = newPoint;

#main.pass
func newPoint (...):(
   ...
):(...);
```

#### How to load a module

```headlot
take moduleId as nameToUse;      @... brings in the module's #main
```

- If you omit `as`, that module's id becomes the name you use as-is.

**The standard library (the automatically supported library) doesn't need `take`.** You can always just use it (like `print`/`Line.addLine`). `take` is used only when bringing in someone else's modules or libraries.

- **Why:** forcing take makes it like Python — while writing code, to use something you have to **break the flow and go up to the very top line** to add an import. That's really annoying. Headlot hates jumps (the same reason "marking it at the top in advance" was rejected in information baking).

// TODO: make a job that marks the part of the code that runs automatically when this module is taken.
- **`import` is a feature that brings in one object inside a Module** — it's used when picking a specific function or value inside it rather than the whole module.

```headlot
take Pointer;                       @... the whole module (used as Pointer.newPoint())
take Pointer import newPoint;       @... only newPoint inside the module
```

There's also something called `using`, which is roughly used when setting up hl; for details see main just below.

### main

main is a job that says this is the main function, variable, Yulist, or the like.

That is, main is Headlot's entry point.

Originally the whole Headlot code should look like this.

```headlot
using hl;

#main
func helloWorld ():(
   Line.addLine("Hello, World");
):();
```

And using is there for readability.

If you start right away at the beginning

```headlot
#main
func helloWorld ():(
   Line.addLine("Hello, World!");
):();
```

it starts without taking a pause, so it's complicated from the start and somewhat uncomfortable to look at.

But if you start with `using hl;` at the beginning and take a pause

```headlot
using hl;

#main
func helloWorld ():(
   Line.addLine("Hello, World!");
):();
```

And if this `#main` bothers you a bit, you can also do this.

```headlot
using hl;

#main func helloWorld ():(
   Line.addLine("Hello, World!");
):();
```

This gives a slight feel of Java's static, final keywords. If you think using it like a Python decorator looks better, go with `\n` after #main; if you like things laid out like Java's static, final, going with `#main func` is recommended.\
For reference, Headlot skips all `/\s/` except in comments anyway, so the compiler interprets both the same.

If it isn't complicated from the start and there's a simple declaration statement at the beginning, you can immediately see "ah, the body is here", so it reads a bit better. ~~or not, whatever~~

For reference, precisely, using is a compiler option. But it exists for readability. And since some people may find this using inconvenient, if you don't use using, `using hl;` is automatically added to the top line at the compile stage. (The compiler that compiles using is called the setup compiler.)

> For reference, Headlot code in this document that doesn't start with `#main func ...` isn't code where you can skip it — it's just that writing it all out would get too long, so it wasn't written.

### Yulist

All of Headlot's data structures are unified into **Yulist** alone. Arrays, linked lists, and dictionaries are not special data other than Yulist; they are **Yulists with a few settings already applied** (presets). The user can make new data structures out of the same material too (1-A #9 — don't separate user and system).

Yulist is a representation-oriented feature. Rather than an option like `mode = list` (twenty questions), it **represents what to do when finding a value, what to do when modifying, what to do when created.**

**Its identity**: apart from one special search syntax `Yulist[?]`, Yulist is not a new core mechanism but **a big library built on top of Interception and expand** (1-A #10 — there's only one hook mechanism, Interception).

**Performance — the representation is fixed at expand time**: representation = the shape actually laid out in memory (contiguous array / scattered nodes / hash buckets). expand reads at compile time what configuration (presets + hooks) this Yulist is, and bakes machine code with the real layout matching each configuration. After expansion the array preset is just contiguous array indexing machine code — not a single line of code asking "what kind is this?" remains at runtime. (Lua's table is effectively a hash inside no matter what you put in it, so the cache advantage of arrays dies — this sentence is what avoids that trap.) Only Yulists whose configuration changes during execution pay the indirection cost, and that cost is paid by the person who chose it (cost honesty).

**Creation**: normally, where you declare with a manifesto function, it's `<function name> <name of the thing to be newly created>`. But if you don't want to make it with a manifesto function and want to make it directly with the new function, you can do this.\
Use the new function. It goes like this: `new(Yulist type) deliver (the things to pass to that Yulist's constructor)`. Also, deliver is a country of the new function, and the argument of the new function is of type typeof[Yulist].

A Yulist is always a reference. If you want to use a plain copy you have to hold the result of the .clone() function.

Division of roles: **the compiler's part = the representation** (what shape to bake it into), **the user's part = the placement** (where in SM to gather those shapes — preventing values from scattering is the user's job).

**Citizenship**: if you put a value into a Yulist, that value migrates to the Yulist's citizenship (consistent with the container escape rule — → memory management).

**Search**: `Yulist[?]` — if you declare the index position with the condition type, queries like `bricks[name == "door" and color == "red"]` hold (absorbing M.G.S 2.0's where without adding syntax — → type magic).

**Member-style access**: not only `Yulist[?]` but also dot access in the form `Yulist.key` works (`bricks.door`). It reads better when the key is a name. However, how to allow and distinguish `.` access when the key is a **number** is undecided (something like `Yulist.0` is ambiguous — → UNKNOWN).

**The name**: it just has no meaning.

**Pronunciation**: pronounced You + List. In phonetic symbols /juːlɪst/.

// TODO: the preset list (array / linkedList / dictionary / set …) and the hook configuration spec of each preset, fixing the `?` notation of `Yulist[?]`, the registry pattern and the weak reference problem (→ UNKNOWN.md).

### Type conversion

Use the changeType function.

It goes like this: `changeType(value, type);`. value is any and type is typeof[any]. It converts value into type. If it doesn't fit the format, nothing is returned.

### Array, Dict, LinkedList

> For reference, these aren't new data structures other than Yulist; they're Yulists all the same. As a standard library.

**First, Array.**

Array is an array. The array we all know well

It's created with the new function.

Here's actual use.

```headlot
var ScoreList :: Array = new(Array); @... creates an empty array
var AskInput :: AskInputModule = Line.askInput();

loop {
   var NewScore :: middle[double] = changeType(AskInput.reask("new score"), middle[double]);
   ScoreList.append(NewScore); @... same as table.insert(self) in Luau. Likewise, if you put an index after NewScore the value is added at that index, and if you don't it's added at the very end.
};
```

Besides that, you can erase the whole array with the .delete function, delete the value at an index with the .remove(index) function, and erase a value inside that array with .removeThisValue(value). Also, with .find(value) you can find that value in the list and get its index.

**And then Dict.**

// TODO: do Dict, LinkedList

### Memory management

**Goal (positioning)**: in C and C++ leak prevention is the user's job, and Rust is safe but hard. In Headlot **the compiler bears leak prevention and safety.** In exchange, some patterns that store and return references are forbidden — that's the price paid for easiness. (Note: blocking even structural leaks is something Rust can't do either — in Rust, Rc cycles and mem::forget are 'safe' code. However, no language can block a logical leak where a live registry keeps holding an object — → UNKNOWN.md.)

// BEFORE: there used to be "end with free", freeing at the moment a country ends so leaks are blocked at every ending point, but this had some problems so a new method is being devised.
// TODO: new memory management method
// It's roughly this: all memory, if dynamic, must have code that frees it, and if there's no such free, error; and also make a data structure implemented as a Yulist called a storage where the Yulists live, and there you specify directly that this part is the creation function and this is the deletion function, and if there's no code freeing or newing inside it, error

**SM (Substitution Memories)** — in Headlot you can also write code at a low level. Precisely, it's storing a value at an address and getting the value at that address, on top of a substitution memory called SM.

- **The substitution principle**: Headlot doesn't forbid dangerous things — it substitutes them. Just as VMware gives you a fake CPU, SM gives you fake memory. Only the substitute is provided to the user, and the real memory is touched only by the language.
- SM isn't a small playground; it's **the substitution memory space of the whole program** — both var and Yulist live entirely on SM. Layers: SM (the whole) ⊃ country arenas (sections) ⊃ values.
- `SM.store(address, value)` — put this value at some memory address / `SM.load(address)` — get the value at some memory address. (Same terminology as LLVM and hardware. Argument order is // TODO.)
- **Ordinary var access has 0 range checks** — the compiler laid out the address so it can't be wrong. Checks are attached only to SM.store / SM.load, where the user makes the address by hand.
- Two-stage range checking: if it can be decided at compile time (literals etc.), compile error. The rest use guard pages — out-of-range access is caught by hardware as a trap (0 check code, the WASM runtime approach). Embedded and 32-bit fallback use if checks — // TODO.
- **Giving up (recorded)**: kernel- and driver-level direct control of real memory is not Headlot's domain. In exchange you get a language without unsafe. C FFI is the SM ↔ real memory copy layer (marshalling) — see the `C FFI` section below.

// TODO: explicit copy syntax, reference/borrow rules (together with func and queue syntax), the minimal code for each escape + the error wording.

### Citizenship table

| Name   | Rank                            |
|--------|---------------------------------|
| function    | first-class            |

// TODO: organize

### C FFI

Headlot values live on the country arenas of SM (substitution memory), and real memory pointers are not exposed to the user. C works with real memory, raw pointers, and manual malloc/free. So C FFI is the **boundary** between the two worlds, and Headlot handles this boundary differently from other languages because of its own model (SM, countries, the cooperative scheduler, expand).

**1. The boundary is explicit — the safety guarantee ends here.** Headlot's value proposition is "the compiler bears safety and leaks". C is inherently unsafe. So a place that calls C is possible only inside a **marked boundary** (an FFI block/job — syntax undecided), and "from here on, outside the compiler's guarantee" is visible in the code. It isn't hidden (principle 3, honesty).

- **Why:** the same spirit as Rust's `unsafe`/`extern "C"`, but the reason comes not from philosophy but from a **constraint** (C really is unsafe, so the guarantee can't be continued). If you don't draw the boundary, unsafe becomes contagious and the very value of "a language without unsafe" collapses.

**2. Data crosses by marshalling (copying) — expand bakes it at compile time.** Headlot doesn't pass country arena pointers to C (if it did, end-with-free and send migration safety would break). Instead it **copies (marshals)** values into C ABI layout and hands them over. expand reads the Yulist representation (the fixed memory layout) at compile time and **bakes** this conversion code in place — 0 runtime reflection cost, and only code that crosses the boundary pays the marshalling cost (cost honesty).

- **Why:** copying isn't a preference but a **constraint** — SM safety forbids exposing arena pointers, so copying is forced. (If zero-copy for a large buffer is needed, an exception with an explicitly pinned buffer — undecided.)

**3. Memory allocated by C is not freed automatically by Headlot — an honest concession.** end-with-free manages only SM country arenas. Headlot knows nothing about C's malloc memory. So C-owned memory is held as an **opaque handle**, and freeing is done by the user directly (calling that C library's free).

- **Why (concession):** the moment you cross C FFI, the no-leak guarantee is **the user's job**, not the compiler's. It's the same for Rust in FFI — no language can bear lifetimes beyond the C boundary on your behalf. It isn't papered over with a workaround; it's admitted. (This is where the boundary that Headlot's safety guarantee holds only "inside SM" is made clear.)

**4. Long or blocking C calls are promoted to workers.** Headlot uses cooperative scheduling so the compiler plants yield checks at loop back edges and call boundaries, but **it can't plant them inside a C function.** So a long C call freezes the entire Stack (starvation). Solution: blocking and long C calls are put on a separate thread with the already existing **free worker promotion** (1-D) so they don't block the cooperative scheduler. Short C calls are treated as an atomic section without yielding, like `atomic{}`.

- **Why:** it's a constraint that came from the domain (the cooperative scheduler), and it **reuses an existing mechanism (worker promotion)** — no new machinery is made (#10). (The judgment of the short/long boundary and the default are undecided.)

**Undecided (→ // TODO):**

- extern C function declaration syntax + the FFI boundary block/job notation.
- The type mapping table (int↔int32/64, Yulist↔C array/struct, string↔char\*, boolean, pointer↔opaque handle).
- C→Headlot callbacks (function pointer marshalling — Headlot functions carry naming and information so they differ from raw pointers, → a point of conflict with information orientation).
- Matching struct ABI alignment and padding, zero-copy pinned buffers, propagating C errors (errno/return codes), the type notation for C-owned handles (`opaque[T]`? `Cptr`?).

### Py FFI

Using Python libraries in Headlot.

First let's look at how it works. Python code is translated into Headlot code. Here class just turns into a new Yulist definition, for turns into while or forEach, and for now this still has to be built out more.

// TODO fix this precisely

## expand

expand is a special function (a function the user can't make, like var and const).

expand X means "run X as far as you know it at compile time, and expand it in place as far as you don't."

- If everything is known → only the value remains (constant computation — not a separate comptime feature but one result of expand)
- If nothing is known → the body is attached in place as a whole (inlining)
- If it's a function that manipulates notation → substitution

Three results from one semantics — a realization of 1-A #10 (no duplication). (This approach is called partial evaluation. Zig's comptime is the same lineage.)

Expansion doesn't fail — what isn't known is not an error but code that remains. The only error is exceeding the expansion limit. Because with recursion of unknown depth, the copy-pasting never ends (no compile-time system can avoid this — Zig blocks it with a quota too). The limit is taken by expand as an argument and the default is 2000.

Multi-mechanism functions (if, while …) are defined with expand. That's why control structures have 0 call cost.

The first line of the external explanation: expand works on units of meaning, not text. It is not a C-style text macro.

Precisely, it goes like this.

```headlot
func a ():(
   print(0);
   expand {
      print(1)
   };
):();
```

Then at compile time the expand inside the a declaration disappears entirely. But the part that calls a, `a()`, changes like this: `a(); print(1);` — what was expanded gets attached entirely at the part that calls a.

But then there's a problem. If, like Zig's comptime, you want to expand a value that adds two things and the function name is addExpand, then `var X :: int = addExpand(1, 2);` causes a problem. After compiling it becomes `var X :: int = addExpand(1, 2), 3`. Then the expand inside addExpand(1, 2) is empty, but inside it there'd be something like `var Sum :: int = X + Y`, and then this function won't get empty-function-killed, and then another problem is that addExpand(1, 2) doesn't return but only expands, so the result is nothing and x becomes nothing.

// TODO: solve this

// TODO: the unit of the expansion limit (1 expansion = what is counted), the notation of definition-expand vs call-expand — when the func syntax is settled.

## None-Native (interpreter mode)

The default is native (LLVM → machine code). But if you use **`using hl-none-native;`** instead of `using hl`, it doesn't compile to native machine code and an **interpreter** reads and executes it one unit at a time.

```headlot
using hl-none-native;

#main
func helloWorld ():(
   Line.addLine("Hello, World!");
):();
```

**Why (domain, not philosophy):** the optimum differs per workload — sometimes **starting fast** (iterative development, small scripts, REPL/eval, DSL embedding) is better than waiting for LLVM optimization + linking, and sometimes **running fast** (long-running heavy programs) is better. So you pick between the two by purpose. (Precedent: Luau also makes native optional and turns it on with `--!native`. Headlot's identity is "honest native performance", so **the opposite: native is the default and none-native is the opt-out.**)

**Architecture — why it doesn't split:** there is one source of semantics. The frontend (lex → parse → **expand**) is **completely shared** by both modes, and the only thing that splits is the final backend.

```
lex → parse → expand → core IR ┬─▶ LLVM → native      (fast execution, default)
                                └─▶ interpreter        (fast startup, hl-none-native)
```

- **expand runs in both modes.** The meaning of control structures and type magic is decided in expand, so the interpreter also runs expand and then interprets **the result (core IR)**. That's why native and none-native produce the same result for the same program — the same discipline as Luau keeping one bytecode as the source so native doesn't split.
- What none-native saves is the **LLVM optimization + linking** stage (expand runs either way). That part is the big chunk of compilation, so startup really does get faster.

**Honest cost (no workaround):** the interpreter is slow to execute — it traded fast startup for fast execution, so when something "has to start immediately but also has a lot of work", native is still better. And since there are two backends, the semantics have to be kept in sync. (Though this is also a gain — the reference interpreter becomes a **semantics oracle** that validates the native backend: differential testing.)

**Undecided:** the notation of the core IR the interpreter interprets, what differs under none-native (what happens to C FFI and worker promotion in the interpreter — automatic yielding is compiler-inserted in native but reduction counting (the zevring prototype) is more natural for an interpreter; consistency to be checked), whether partial native is allowed, raising only hot functions to native.

### Interception

Interception is Headlot's **only hook mechanism** (1-A #10) and the floor of Yulist and of the class replacement (metatable). It feels like TS's proxy/getter/setter, but it intercepts **only exactly the situations you declared** (it doesn't catch everything like a proxy).

**Model:** an operation on a value (creation, `=`, `+`, indexing …) **emits** a situation, and interception's `when` receives that situation and handles it **on its behalf**. This emit/when is the system's internal behavior model (it isn't user-facing event syntax — that went to actor messaging). Positionally it's exactly the same as **Luau's metatable** (`__index`/`__add` …).

**Declaration — independently, without a target:**

```headlot
interception Bag (
   when get (key):{ return ...; };      @... when reading  (bag.key / bag[key])
   when set (key; value):{ ... };        @... when writing with =
   when add (other):{ return ...; };     @... on the + operation
   when create (...):{ ... };            @... when created
);
```

- `interception NAME ( ... )` — `interception` (function name) + NAME (naming) + `( hooks )` (body). Exactly principle 0.
- `when situation (whatToTake):{ whatToDo }` — one hook. `when` (function name) + situation (naming) + `(args):{body}` (handler). This is principle 0 too (an argument function inside a label, like case and prototype methods).
- **The situation is not a fixed list.** The operation that emits that situation decides what it passes (e.g. `+` emits `add` together with the other operand), and interception `when`s **only the situations it wants to handle**. Situations not handled just pass through — **representation orientation and cost honesty** (only what you represented, only that cost).
- Hooks that have to produce a value (get/add …) return it with `return`.

**Attaching — inserted with a job:**

```headlot
#Bag
var inventory :: Yulist = ( ... );   @... inserts the Bag interception into this variable
```

- The **main way** to insert an interception into a variable or Yulist **is a job** (`#name`, or `(< name ... >)` for a section). Consistent with the existing job model — a job changes the operation behavior of that section like a Python decorator (e.g. the same grain as the `ref` job changing `=` into a reference).
- **Yulist works the same way** — presets like array and dictionary are in the end a fixed bundle of interception hooks. So "choosing a data structure = inserting that interception".

And why is there no such thing as target? Because the way it works is attaching the interception to the target, not deciding the target when declaring the interception, and the reason is that it lets you implement more things later.

And global is a valesto, and the reason there's something like global.all is that an interception is applied. Because inside global there's code like `when key (key):{ if (key == "all"):{...} else {...}; };`.

**Undecided:** the contract of the argument shape each situation passes (which operation emits which situation with what arguments) — if this isn't fixed, errors get ambiguous when hook arguments mismatch (→ UNKNOWN, connected to the Deep Module error problem). Whether `set` is always `{key; value}` or a scalar `{value}` version exists too. The order when several interceptions are inserted on top of each other.

### kind

First, kind is an enum, but with more of a "sort" feel?

First, kind isn't like an enum with enum.A = 1, enum.B = 2; kind.A is simply an object called kind.A and kind.B is an object called kind.B. As for how it's implemented,

kind.A is originally 0, kind.B is 1. But the type is that kind

```headlot
kind Keyword (
   VAR; CONST; LET
);
```

Here Keyword.VAR stores the value 0. But the type is Keyword. And at this point, if you compare 0 and Keyword.VAR with `~=`, the comparison that also does type conversion, an interesting thing happens.\
`~=` first pulls out the data of Keyword.VAR. It doesn't pull out the type, and the data of Keyword.VAR is 0; and it doesn't pull out int, the type of 0, either, only the value 0. Then it becomes 0 == 0. The result is true.

As you'll have seen above, the kind declaration statement is

```headlot
kind kindName (
   sortName1; sortName2; ...
);
```

like that. For example

```headlot
kind Keyword (
   VAR; CONST; LET
);
```

you can use kind like this when making a language with Headlot.

You can also add new things to an existing kind.

```headlot
kind FuncKind (
   DO_RETURN; LOOP; IF; INLINE @... // TODO: consider renaming INLINE to EXPAND (unify with the expand decision)
);
```

Here, for the user to add a new value

```headlot
FuncKind.add(newSortName, index);
```

First, newSortName here is what name of sort to add, and index is what value comes out when this is type-converted to int, with the default being the last sort's index + 1.

For example

```headlot
FuncKind.add(FUNC); @... right now the last index is 3, so index is automatically 4
```

For reference, when do you put in the index parameter? You use it when you want two sorts in this kind to be represented as the same thing. So when you want, say, LOOP and MY_LOOP in FuncKind to be the same, you use index.\
Actually it's almost never needed, so not using it is recommended, and using it only when needed, when it's really absolutely needed, is recommended.

For reference, you might wonder why FuncKind suddenly appears — the kind function declares the FuncKind type with expand and adds methods inside it, and so on.

And then ChildKind. Child sorts.

```headlot
kind FuncKind (
   CONTROLOR (
      IF;
      LOOP;
   );
   MANIFESTO (
      MODULE (
         MAIN;
      );
   );
);
```

If it's like this

FuncKind.CONTROLOR is also the same as FuncKind.CONTROLOR.IF

So that's it. A child kind is also the same as its parent kind or its ancestor kind.

Also access goes like FuncKind.CONTROLOR.IF, and the type is all the same, FuncKind.

Adding a child kind goes like this.

FuncKind.CONTROLOR.add(IF);
FuncKind.CONTROLOR.add(LOOP);

(The FuncKind code above differs from the real FuncKind.)

The rules of kind:

- A kind's index starts from 0.
- Use `==` for kind comparison. (The `~=` example is for understanding. Note: even for different kinds, if the index is the same `~=` is true — it's a consistent consequence of `~=`, so watch out for the trap.)
- add runs at expand time (compile time). Adding in user source is free (e.g. `FuncKind.add(COUNTRY_FUNC)` classifying functions like tax calculation and rebellion probability in a nation management game). Adding during program execution is impossible — because the label rule of break/continue reads the kind (of the country the label points at).
- Adding the same name is a compile error (1-A #11).
- No default rules are attached to a new kind — the side that reads that kind gives it meaning.
- **The same FuncKind keeps the same form.** FuncKind is like a **part of speech** in natural language (→ data.md #11), so within the same part of speech the inflection form has to be the same. Just as in English you use the same form `to` when attaching something to a noun, functions of the same FuncKind use **the same slot shape** (what is taken where). e.g. `while` and `repeat`, both `FuncKind.LOOP`, are both of the form `(condition/count):{body}`, and their escapes share the same `to` country.
  - **Why:** if the form varies within the same part of speech, the user has to memorize the form anew for every function. Tying the form to the part of speech means **learn one and you can read that entire part of speech** — it's why others can read a custom control structure (principle 0) even when you make one, and why a dialect becomes new vocabulary rather than a new language (#9, #10).
  - Form consistency is enforced by the side that reads the kind (the compiler and the small country rules) — mismatch is a compile error. (Judgment details when the func syntax is settled.)
- **FuncKind-specific small countries are attached by explicit mapping, not automatic insertion.** For example, in `FuncKind.REPEAT`, `break` doesn't appear automatically as if by magic; you register **"in this kind, break is this function"** like `break = MyBreakFunction`. (Why: where a small country came from and which function it is becomes visible in the code — the spirit of no name magic and principle 3. Since which kind gives which small country is explicit, there's no hidden injection.)

### Naming conventions

First the basic rule. If something has information, has formality, and is equipped with something (it has a type, it has a value, that sort of thing), use PascalCase; and if there is something and you are declaring something proper, but it has no formality and isn't equipped (anything, a variable whose type is never), use camelCase. Also, for special syntax — using is a compiler option, but using itself gets compiled, and at that point choosing the compiler for that with using is a contradiction, so using is special syntax, and to emphasize special syntax, the compiler name (precisely, an abbreviation of the name of the language that compiler compiles) is written in kebob-case.

And snake_case is used only for .hl files. Like test_debug.hl. Why snake_case? Because file names don't especially need to be easy to read, and it's good if you learn them like a picture and instantly recall what this file does. And in snake_case the _ is a bit cumbersome, but here that actually becomes an advantage — snake_case looks like a picture, so it's easy to learn what this does. So file names use snake_case. And the .tpro file is this project's connector file. It's the main file of the project that connects everything into one. It's just the single file that organizes each of the tasks that do all the work of this project. So it uses PascalCase. Like LookLanguage.tpro — this way it definitely feels different from the ordinary snake_case files, like the uppercase is the biggest thing. So it uses PascalCase.

// TODO: decide and unify all the naming conventions

## 1-D. Execution model — Stack / Sub-stack / Queue (concurrency)

Headlot's concurrency and execution model is a **hierarchical actor system based on cooperative scheduling**. It uses **message passing**, not shared memory, as the default. (Only the execution model was taken from the designer's browser zevring runtime — the browser and rendering parts were left out.) This model ties in with Headlot's honest cost exposure, freedom, and native performance. Below, the details are written out so that reading only this document tells you the whole execution model. (**The exact notation for the queue/stack declaration syntax and the message API is defined in the queue/stack part of the 1-C grammar** — here only the execution model and concepts are written.)

### Three units — director / coach / player

- **Stack** — the top-level scheduler. **Exactly one** per execution unit (program). A thin loop that picks and directs the execution of the queues (it doesn't do heavy computation). (Analogy: the brain / the director)
- **Sub-stack** — a delegated scheduler. It's like a queue in that it takes the Stack's orders, but unlike an ordinary queue it (1) **can run on its own** and (2) **controls other queues**. (In the lineage of the Erlang/OTP supervision tree. Analogy: the coach)
- **Queue** — an execution unit (actor) that moves under the direction of a Stack/Sub-stack. Each has its own FIFO mailbox and communicates **only through messages**. (Analogy: the hands and feet / the players)

- **Why:** if one scheduler directly controls every queue, it becomes a bottleneck and a management burden as the scale grows. Delegating control through a director–coach–player hierarchy keeps the director thin.
- **Advantage:** strong at scaling, and the proven pattern where a supervisor restarts a failed unit (supervision).
- **Disadvantage:** with three units there are more concepts to learn, and the queue ownership (tree) rules have to be clearly defined (→ TODO).

### Queue state machine

| State | Meaning |
|------|------|
| `waiting` | waiting for CPU. it's in the ready queue and the scheduler **can pick** it as the next thing to run |
| `running` | currently running. **only one queue at a time** is in this state |
| `blocked` | waiting for a specific event (a message reply, completion, etc.). the scheduler **doesn't pick** it to run |
| `complete` | body execution finished. live memory freed + compressed storage (hibernation) |
| `kill` | forcibly stopped |
| `failed` | stopped by an error. a **separate state distinguished** from a forced stop (`kill`) |

```
(queue created) ─▶ waiting ──(picked)──▶ running ──┬─(yield)─────────▶ waiting
                     ▲                             ├─(message/wait)──▶ blocked ──(reply arrives)──▶ waiting
                     │                             ├─(body ends)─────▶ complete
                 (revival)                         ├─(unhandled error)─▶ failed
                     │                             └─(forced stop)────▶ kill
                     └──── a message arriving at a complete queue revives it (complete → waiting)
```

- **Why `waiting` (ready) and `blocked` must be distinguished:** if you don't distinguish them, the scheduler keeps picking a queue whose reply hasn't come yet, wasting CPU on a queue that can't do anything even when run. A blocked queue returns to waiting — and becomes selectable — only when the reply it was waiting for arrives.
- **Why `failed` is separated from `kill`:** a forced stop (external will) and an error stop (internal accident) have different causes, so the supervisor's response has to differ too; distinguishing them by state is what makes a decision possible.

### Scheduler execution loop

```
Scheduler.run():
   while (ready has queues):
      q = ready.shift()               // in its own order
      q.state = running; current = q
      run q "until the next yield / blocked / complete"
      - reached a yield point & another ready exists → park q as waiting
      - waiting for a message/reply → set q to blocked
      - body ended → set q to complete
```

**Important — it's interleaving, not parallelism.** "A runs, then B's request comes so B runs" works by A yielding and the scheduler picking B, which has become ready. It looks parallel but is actually one flow crossing over — interleaving — with no data races and simple reasoning and debugging (the intended default). Real parallelism is a separate path via worker promotion (below).

### Automatic yield safety net (starvation prevention)

Pure cooperative scheduling lets one queue that doesn't yield stop the whole thing (starvation). So the safety net is laid down doubly.

- **Explicit `tick`** — for cooperation. the queue yields voluntarily.
- **Automatic yield** — **the compiler inserts a yield check (decrement a counter, force a yield at 0) at loop back edges and function call boundaries.** (zevring counts reductions in the interpreter, but Headlot is native AOT with no interpreter, so **the compiler plants the check instructions** for the same guarantee — in the family of Go's cooperative preemption.)

- **Why the insertion points are limited:** the hidden contract of cooperative scheduling is the atomicity of "no one cuts in before a yield". Inserting at arbitrary points breaks this (read-modify-write sections, etc.). So insertion is **limited to loop back edges and call boundaries only**, and a section that must never be cut is suppressed from automatic yielding with **`atomic { ... }`**. (The same spirit as principle 3, no hidden control flow.)
- **Warning policy:** a loop with no yield point is not an error but a **lint warning** (there's a safety net, so it's not a bug but "code whose latency can't be predicted"). But warn **only when a statically unbounded loop has no yield point** — warning on every tick-less loop would become noise and bury the real warnings.

### Sub-stack — delegated scheduler (the coach)

The burden of one Stack directly controlling every queue is split by layers. The Stack (director) gives only the big orders to the Sub-stacks (coaches), and control of individual queues is handled by the responsible Sub-stack.

| Sub-stack state | Meaning |
|------|------|
| `running` | running its own body code |
| `waiting` | waiting |
| `stacker` | doing part of the main Stack's work (controlling the queues it's responsible for, etc.) — a **Sub-stack-specific state** |
| `kill` | terminated by the main Stack. **But unlike an ordinary queue, restartable (rebirth)** |
| `complete` | complete |
| `failed` | errored |

- **The `stacker` state:** separating its own body execution (`running`) from coach duties (controlling its queues) into distinct states lets you observe "time spent doing its own work" separately from "time spent on control duties" in profiling and debugging.
- **The `kill` difference (key):** an ordinary queue's `kill` is **not restartable**. A Sub-stack's `kill` is **restartable via rebirth**.
- **Relation to worker promotion:** a Sub-stack + its group of responsible queues is a natural candidate unit for worker promotion. Putting the whole group on a thread keeps reference passing inside the group and serializes only the messages that cross the group boundary.

### Messaging (actor communication)

**Direct delivery, guaranteed delivery.** It is **not** a global event/broadcast — it delivers directly to a specific queue.
- *Reason global/broadcast was rejected:* the receiver is unclear and delivery can't be guaranteed. The principle that "a message is **never dropped**" holds only for direct delivery to a specified receiver.

**Mailbox.** Each queue has a **FIFO mailbox**. Messages that come via `send`/`ask` pile up and aren't dropped. For memory's sake bounded is recommended; on overflow, **backpressure** (slow the sender) or an error.

**Receiving — two styles.**

| Method | Character |
|------|------|
| **on** (declarative handler) | auto-dispatched when a message arrives |
| **receive** (imperative) | goes `blocked`, waiting until the next message comes. for sequential protocols |

**Sending — two styles.**

| Method | Character |
|------|------|
| **send** | fire-and-forget. doesn't wait for a reply |
| **ask** | request-response. returns a Promise that completes with the reply value |

- **Performance:** it's **in-memory reference passing** so it's fast with no serialization. Serialization is only for queues promoted to workers.
- **Deadlock prevention:** (1) `ask` has a default timeout (changeable by option, can be infinite), and rejects on exceeding it. (2) Every time a queue goes `blocked`, a **wait-graph cycle detection** runs — if there's a cycle it immediately rejects with `DeadlockError` ("an immediate, clear error" instead of "a silent stop"). (3) A sender blocked by sending to a full mailbox is registered in the same graph too → even send-send deadlocks are detected together. Since it's a single-scheduler in-memory setup, the check cost ≈ 0.

### Hibernation (complete = compressed storage)

When a queue goes `complete` it no longer runs, so it **frees and compresses** its live environment (variables, closures) (for memory and performance). If it's needed again it is **revived** (e.g. a `send` arriving at a complete queue auto-revives it → the no-loss principle is maintained even during hibernation).

- **Revival 1 — one-shot:** keeps only the queue's function and its arguments (props) and discards the environment. On revival that function is re-called with the arguments. **No serialization needed, the cheapest.**
- **Revival 2 — stateful snapshot:** serializes and compresses the state (a snapshot) and discards the environment. On revival it's unpacked and **continues** running. Safe even with a DB or randomness. **Constraint:** functions and closures can't be serialized, so a hibernatable queue's state must be composed of **data only**.
- **❌ Replay (event sourcing) rejected:** the approach of replaying from the start with a message log is not used. Revival cost is O(history) so a queue gets slower the longer it lives, and using a DB, randomness, or time makes replay non-deterministic (dangerous). A pure-actor-only option.
- **The `data` queue contract (two birds, one stone):** the snapshot-hibernation condition ("state is data only") **exactly matches** the serialization condition for worker promotion. So at queue declaration one flag bundles (a) snapshot hibernation possible + (b) worker promotion possible + (c) putting a function/closure in the state errors at snapshot time — into **one contract**. In development mode it periodically checks serializability (preventing "tried to hibernate but can't" after deployment). A queue that needs a closure just doesn't declare the contract (uses one-shot) — **a contract of choice, not force**.

### Worker promotion (real parallelism)

A CPU-heavy queue is put on a **real OS thread** to get multicore parallelism.

- **The "free upgrade" argument:** actors, from the start, share no memory and only exchange messages, so moving a queue to a thread doesn't break the code. Had it been shared-memory, separating data between threads would have been impossible (the fundamental reason shared-memory concurrency was rejected). → writing it as actors now makes parallelization a **free upgrade with no code changes**.
- **Cost and policy:** workers don't share memory, so messages are sent **serialized**. So the default keeps in-memory (reference), and only CPU-heavy queues are promoted. (Full workerization rejected: most queues are light, and it would impose serialization cost on every message.) Promotion eligibility is judged by the `data` queue contract above.

### Deep recursion & first-class continuations (runtime core)

Deep recursion overflows the OS call stack and blows up. And **queues/threads can't solve it** — a thread has the same stack limit, and deep recursion is **one unbroken chain** where call N depends on the result of N+1, so it can't be split across several queues. The fundamental fix is turning recursion into iteration + an explicit stack (trampoline / CPS).

- The Headlot runtime puts a queue's execution stack and continuation **explicitly on the heap** (stackless / growable stack). Effects:
  - **(a) preemption is free** — it can stop at any point in the execution loop, so the automatic yield above becomes "one line that checks a counter".
  - **(b) deep recursion and suspend aren't trapped on the OS stack** — a queue goes `blocked`↔`waiting` cheaply.
  - **(c) continuations are first-class data** — the path opens for generators/async and "a mid-execution snapshot".
- **Two birds, one stone:** queue suspend/resume and the control layer's `yield` (a small country) stand on the **same first-class continuation**. Concurrency and control share one floor rather than being separate machinery (→ the floor of data.md #7).

> Undecided items (the queue ownership tree rules, the `failed` supervision protocol, the `data` queue contract notation, the `atomic`/`tick` syntax, the yield-check insertion points and the counter's initial value, etc.) — see TODO.md.

## 1-E. bash

### Execution

First, how to run a Headlot file.

```bash
headlot <file name>
```

That's it. If you want to leave a build artifact

```bash
headlot <file name> -o <executable name>
```

you can leave a build artifact this way.

For example, if you want to run a game file called WorldWar.hl

```bash
headlot WorldWar.hl
```

you do that, and if you want to run one at a specific path

```bash
headlot "C:\WorldWar\START.hl"
```

you do this.

Also if you type hl alone

```bash
headlot
```

then the help about using the hl terminal is printed.

## Standard library

For the standard library: since in Python it's annoying to keep importing and breaking the flow, you can use the standard library without `take`, just as Luau doesn't have to do `const math = require(game:GetService("MathService"))` to use math.

### SubStackTurner

SubStackTurner is a standard library that makes several queues advance one step at a time on the same beat.

The core mechanism: when a queue finishes its own work it puts itself into blocked and waits for the event until the turn ends, then releases everyone at once when they've all arrived, or releases them all at once at a specific interval. The domain: FPS, game turns, world simulation ticks. And there's fixed time (a turn goes around at a specific interval; even if everyone finishes their work it waits until the specific time) and free time (once all queues finish all their work it goes around again; it starts the turn as fast as possible).

One line: actors normally each run on their own, but sometimes everyone has to take one step together.

Headlot's execution model (1-D) is a hierarchical actor based on cooperative scheduling. The queues each look at their own mailbox and run on their own. This is **correct as the default** — they don't wait for each other so there's no bottleneck, one slow queue doesn't tie up the whole thing, and it even goes to real parallelism with worker promotion.

But in real programs there's inevitably a **section that needs "one step, all together"**.

- The screen has to be **drawn entirely** in one frame. If the terrain is a new frame and the UI is the previous frame, the screen tears.
- One turn of a game has to have **everyone on the same turn**. If just one country is on the next turn, it's not a game.
- To save the world state you need **a moment when no one is moving**. If you dump it mid-motion you get a save file that doesn't line up.

The actor model doesn't give this requirement by default. So you need a technique that makes it.

Why the language doesn't give this by default: it can be implemented as a library, so it wasn't made into a feature.

How a Turn goes around:

```
┌─ turn start
│
│  the Turner emits an End-Turn release to all its member queues
│      ↓
│  all → waiting; the scheduler picks them one by one → running
│      ↓
│  each queue: run mappingRealFunc(the doing block)
│      ↓
│  on return → the Turner marks that queue done → blocked
│      (waiting for the End-Turn event)
│      ↓
│  everyone has reached blocked
│      ↓
│  ── turn boundary ──  (the only moment when no one is running)
│      · admit the new queues from the waiting room
│      · snapshot / aggregate / save
│      · (fixed mode) wait out the remaining time
│      ↓
└─ next turn  (loops back to the top)
```

At this point the queue is not forcibly stopped

Also **the Turner does not put the queues to sleep from outside**. When a queue finishes its own work it goes into `blocked` **on its own**, and what it waits for is the `End-Turn` event the Turner will issue.

There's a safety net you get for free. **Deadlock detection.**

The execution model runs a **wait-graph cycle detection** every time a queue goes `blocked`. The Turner's wait is a real event wait too, so it goes right into this graph.

Result: **if the Turner buggily never issues `End-Turn`, a `DeadlockError` occurs immediately.** It doesn't stop silently; it errors. This is given by Headlot's default safety net. That's where the benefit is.

---

Why sub-stack was chosen

A Turner bundles only the group of queues it supervises. Here the authority is above a queue, but since the Stack doesn't do big work, it uses a sub-stack. That's how the name sub stack turner came to be.

```
Stack
├─ Render-Turner (Sub-stack)     ← only this group has the frame barrier
│    ├─ terrain render queue
│    ├─ UI render queue
│    └─ position calc queue
├─ World-Turner (Sub-stack)      ← only this group has the 1-second barrier
│    └─ ...
└─ network queue                 ← belongs to no Turner. keeps flowing
```

**Why not use a global barrier:**
- **A global barrier always ties the whole thing to the slowest queue.** One heavy queue makes all the rest wait. Even if you parallelize with worker promotion, they meet again at the barrier so the benefit disappears.
- Real programs have multiple beats. Rendering is 16ms, the world sim is 1 second, the network has no beat at all. Bundling them into one makes everything match the slowest beat.
- **Side effect:** while one Turner is tied to its barrier, the queues of other Sub-stacks run normally. That is, **there's no idle CPU time.**

**Trade-off:** with several Turners, consistency between Turners isn't guaranteed. The moment the Render-Turner is at a turn boundary, the World-Turner may be mid-turn. If rendering reads world state it may see a torn state. → This is a problem the user has to solve by design, not the library (e.g. rendering only reads snapshots the world published at a turn boundary).

---

There are two modes. Fixed time and free time

Fixed time — startTurnWithPinnedTime

The turn goes around at exactly fixed intervals. If the queues finish early they **wait for the remaining time.**

**Where to use it:** world simulation ticks, game physics, server ticks

**Why it's needed:** sometimes you use it directly for things like resetting the world every 10 minutes. In that case, if the turn moves to the next one the instant the queues finish their work, it might reset the world at 3 minutes instead of 10. Or you have to sync time with other SubStackTurners. That's when you use fixed time.

**Trade-off:** if the queues can't finish within the interval, the turn is pushed back. Whether to **catch up by the pushed-back amount or just skip** is a policy decision (→ chapter 8, undecided).

Free time — startTurnWithFreeTime

Starts the next turn the moment all the queues finish. No waiting.

**Where to use it:** when you just want to go fast and don't need to sync any turn, or anything, with something else.

**Example domain:** somewhere you keep computing, doing physics computations directly, and everyone doesn't need the Turn to go around at a regular interval. Just finish as fast as possible and compute again. That's when you use it.

---

#### API

##### Creation

```headlot
var WorldEnconomy :: SubStackTurner.Turner = SubStackTurner.create();
```

`create` makes one Sub-stack and returns a `Turner` wrapping it.

For reference, since it's a data structure it uses PascalCase. (in the type)

##### Deletion

If you now want to end this turn, you do this.

```headlot
var WorldEnconomy :: SubStackTurner.Turner = SubStackTurner.create();
WorldEnconomy.delete(); @= all the Queues of that SubStack are killed and the SubStack goes into the complete state.
```

And if you want to end it a different way

```headlot
var WorldEnconomy :: SubStackTurner.Turner = SubStackTurner.create();
WorldEnconomy.delete {
   self.waiting(); @... self is the queue currently being ended, a small country of delete. so this puts all these queues into waiting
};
```

you do it like this.

Also, to delete a specific queue from this Turner

```headlot
var WorldEnconomy :: SubStackTurner.Turner = SubStackTurner.create();
WorldEnconomy.addQueue queueName ()...

worldEnconomy.deleteQueue(queueName);
```

you do this.

Example:

```headlot
var WorldEnconomy :: SubStackTurner.Turner = SubStackTurner.create();
WorldEnconomy.addQueue 3DModelRender ()...

worldEnconomy.deleteQueue(3DModelRender);
```

##### Attaching a queue

```headlot
World.addQueue {
   @... creates a queue. returns the queue with return.
} doing {
   @... the code that runs every turn. self is this current queue.
};
```

For reference, here addQueue is country 1 and doing is country 2.

- **addQueue**: makes a queue and returns it with return. (self is the currently created queue; you complete the queue directly and return it with return.)
- **doing**: the body called every turn.

Also, to mark completion in doing, you use the self.done() function.

##### 6-5. Start

```headlot
World.startTurnWithPinnedTime(time);     @... fixed interval (time is written in milliseconds and it keeps running at each interval. even when the time comes, if a queue hasn't finished its work, it makes a leftover-processing queue directly and finishes the unfinished work there.)
World.startTurnWithFreeTime();   @... free (as fast as possible)
```

---

At a turn boundary, **all member queues are `blocked` and no one is running.** This moment is that group's **consistent snapshot.**

Things you get for free here:

**Save / load:** since no intermediate state exists, you just dump it |
**Global aggregation:** since the state of every queue is fixed, there are no race conditions. In the actor model a "computation that sweeps the whole" is originally hard, but the turn boundary gives that spot |
**Hibernation (snapshot):** a natural place for 1-D's snapshot hibernation to hook in |
**Admitting new queues:** gathered in a waiting room and inserted here |
**Worker promotion / demotion:** since it's a moment when queues aren't running, moving is safe |

**Why you can't insert a new queue mid-turn:** bugs can happen. If you insert one mid-turn, it's easy for something to accidentally make this turn take longer in the free time, and so on. Also, the turn boundary is where all the unfinished processing of the turn gets done, and one of the most important reasons the turn boundary exists is to insert new queues here.

---

**Failure handling:**

**A queue in the `failed` state is counted as "this turn complete."**

Because a `failed` queue never goes into `blocked`. If it isn't counted as complete, **when one queue dies the whole group stops forever.**

**The response is not decided by the Turner.** Whether to restart the dead queue, remove it from the group, or halt the whole group is a user policy.

**Why the library doesn't decide the policy:** here the behavior you want may have to be decided by the user directly, and if you let the user decide it with interception, you can write far more flexible code.

---

#### Undecided

11. **Dynamic removal** — the way to remove a queue from a Turner. It seems it should only be possible at a turn boundary.

### Math

> A math-related library

It supports various math functions and constants.


#### max, min

Gets the maximum and minimum values.

Example:

```headlot
print(math.max(1, 2, 3)); @= 3
print(math.min(1, 4, 2)); @= 1
@... reals work too.
print(math.max(1.2, 1.43, 2.5)); @= 2.5
print(math.max(1.4d, 2.4d, 1.2d)); @= 2.4d
print(math.min(1.3d, 1.3d, 1.1d)); @= 1.1d
@... if all the numbers are equal it just returns the one written first.
print(math.max(1, 1, 1)); @= 1
@... if the types are all different it errors.
print(math.max(1, 2.3, 4.1d)); @= errors
print(math.min(1, 3.4, 0.1d)); @= errors
```

Also, if you want to return, say, the longest string

```headlot
var String1 :: string = "Hello, World!";
var String2 :: string = "Byte, World!";
var Longer :: variable[string] | variable[string] = math.max (String1, String2):{ @... String1 is longer, so String1 is returned as a variable.
   return self.len(); @... return is a small country of math.max, and self is also a small country of math.max. math.max, for example, when it substitutes String1 into that expression, self becomes String1, and so on.
};

Line.addLine(Longer); @= String1
```

You do it like this. It returns whichever value returned with return is larger.

#### abs

Returns the absolute value.

```headlot
var x :: int = math.abs(-2); @... returns the absolute value
print(x); @= 2
var y :: double = math.abs(-4.32d); @... double works too.
print(y); @= 4.32
var z :: byte[double] = math.abs(4.2); @... other precisions of double work too.
print(z); @= 4.2
```

#### sum

Returns the sum of all these numbers.

```headlot
var x :: int = 1;
var y :: int = 3;
var z :: int = 5;
print(x, y, z); @= 9
```

For reference, like max and min, mixing different types errors.

### Line

#### addLine

Prints all types like string, int, float, double.

```headlot
using hl;

#main
func main ():(
   Line.addLine("Hello, World!");
):();
```

#### addLineColor

Prints in a specific color.

```headlot
using hl;

#main
func main ():(
   Line.addLineColor("Hello, World!", FFFFFF); @... the color is taken as a color code, as a naming.
):();
```

#### askInput

Takes input. Similar to Python's input. It isn't a yield function; it creates a new queue and takes the question there. So the code flow doesn't stop, and to get that input value you have to use the module that input returned, because askInput asks but doesn't receive the result.\
The type AskInputModule means the module this function returns. As the second argument it takes a color code for what color to use. It's optional and taken as a naming. doing is where you write what to do after taking the question. The self small country means the input content the sibling received.\
With the .reask function on AskInputModule you can ask again. Precisely, the return value of .getInputAsync() is what comes out as the result of .reask, and it also yields until it gets an answer. Also if you pass no argument to reask, it uses the same question and doing as the first ask.\
Also if there are no arguments at all, it just creates an AskInputModule.

```headlot
using hl;

#main
func main ():(
   var Prefix :: AskInputModule = Line.askInput("Hello, World prefix: ", FF0000) doing {
      if (self == "exit"):{
         return nothing;
      } else {
         Line.addLine(`Hello, World prefix is ({self}));
      };
   };
   var Surfix :: AskInputModule = Line.askInput("Hello, World surfix: ", 0000FF) doing {
      if (self == "exit"):{
         return nothing;
      } else {
         Line.addLine(`Hello, World surfix is ({self}));
      };
   };

   loop {
      var PrefixString :: string = Prefix.getInputAsync(); @... gets the prefix result
      var SurfixString :: string = Surfix.getInputAsync(); @... gets the surfix result

      Line.addLine(`({PrefixString}), World({SurfixString})`);
      Line.addLine(`time to answer prefix: ({Prefix.timeOccupined})`); @... the time it took to answer prefix
      Line.addLine(`time to answer surfix: ({Surfix.timeOccupined})`); @... the time it took to answer surfix

      Prefix.reask();
      Surfix.reask();
   };
):();
```

If askInput forces you to work around things, use inputAsync. This askInput sometimes forces workarounds because of its structure, which is why inputAsync exists.

Also the execution method is exactly one queue per one question. And if there are two questions at the same time, you answer the two separately, in that manner.

```
Hello, World prefix: 
Hello, World surfix: 
```

These two come out at the same time, and if you move the pointer up to the one above you can type into it directly, and if you type into the one below you can type into the one below, and so on.\

It'll be incredibly, incredibly hard to implement, but I'm going to try it anyway.

#### inputAsync

Asks directly in this queue. It's a yield function and the same as Python's input.

The usage is this.

```headlot
using hl;

#main
func main ():(
   var Prefix :: string = Line.inputAsync("Hello, World prefix");
   var Surfix :: string = Line.inputAsync("Hello, World sufix");

   Line.addLine(`({Prefix}), World{Surfix}`);
):();
```

For things that are hard to implement with inputAsync alone and force workarounds, use askInput

### time

### asyncTime

Waits some seconds. It's similar to Luau's wait, and it stops this queue or sub-stack. The method is just to block it and set it back to running when the time passes.

```headlot
using hl;

#main
func main ():(
   time.asyncTime(1d); @... waits 1 second and
   Line.addLine("Hello, World!"); @... prints
):();
```

Also, this currently returns exactly how many seconds it waited.

The reason the name is like this is that it looks damn cool.

### untilAsync

Waits until this condition holds.

```headlot
using hl;

#main
func main ():(
   var x = 1;
   var y = 1;
   time.untilAsync(1 == 1, 10d, 0.05d) @... condition, callback, at what interval to keep checking; if there's no callback it waits infinitely, and if there's no check interval it just checks as fast as possible.
):();
```

#### timer

It's a timer. Returns the time in seconds as a double. To make it, since it's a Yulist and not a manifesto — that is, not a declaration statement — it goes `new(timer)`.

Here's the usage.

```headlot
using hl;

@~~ typing game

#main
func main ():(
   @... start with a value larger than 10 seconds at first.
   var ShortestTime :: double = 11d;
   var LongestTime :: double = 0d;
   var InputSentence :: AskInputModule = askInput();
   var MainTimer :: Timer = new(timer) deliver (0d);
   var Round :: int = 0;

   const CONDITION_TIME :: double = 10d;
   const SENTENCE :: string = "O say can you see by the dawn's early light what so proudly we hailed at the twilight's last gleaming";

   MainTimer.start();

   while (ShortestTime > CONDITION_TIME):{
      var ThisTurnTimer :: Timer = new(timer) deliver (0d);

      Round = Round + 1;
      ThisTurnTimer.start();

      InputSentence.reask(`type ({SENTENCE}) within 10 seconds`);
      var Answer :: string = InputSentence.getInputAsync();

      ThisTurnTimer.end();
      var ThisTime :: double = ThisTurnTimer.getTime();

      if (Answer != SENTENCE):{
         Line.addLine(`attempt ({Round}) is incorrect.`);
         continue;
      };

      @... only correct inputs are reflected in the records.
      if (ThisTime < ShortestTime):{
         ShortestTime = ThisTime;
         Line.addLine(`new shortest record: ({ShortestTime}) seconds`);
      };

      if (ThisTime > LongestTime):{
         LongestTime = ThisTime;
      };

      Line.addLine(`this record: ({ThisTime}) seconds`);
      Line.addLine(`current shortest record: ({ShortestTime}) seconds`);
      Line.addLine(`current longest record: ({LongestTime}) seconds`);
   };

   MainTimer.end();

   Line.addLineColor(
      `success! succeeded in ({Round}) tries, shortest time ({ShortestTime}) seconds, longest time ({LongestTime}) seconds`,
      0000FF
   );
):();
```

// TODO: add functions like this — a .repeat so the timer can keep going x -> y, x -> y, and a country called whenRepeatEnd where you can put in new things to do when y resets to x again. And it uses SubStackTurner for that. And also something like which repetition it is (the first repetition being 0).

### global

global lets you make global variables. It lets you make a global variable in this file so that other places can directly use the global variable made in this file. When is it used? For things like making a module, or when a variable in this file has to be manipulated from another file too (like the money currently left in a game).

The basic variable declaration is

```headlot
global id :: naming = add;
```

That's it. Then in another file you do `global.addUsingVar(variable name, globalId)`, and here the way to decide globalId is `global id :: naming = globalID`.

And here's an example.

File A:

```headlot
using hl;

global id :: naming = score;
global score :: int = 0;
```

File B:

```headlot
using hl;

#main func scoreGame ():(
   global.addUsingVar(score, score);
   next score;
   print(score);
   next score;
   print(score);
   next score;
   print(score);
   Line.addLine(`final score: ({score}) points`);
):();
```

You can make it like this.

And here there's a project global variable. It's just a global variable in the project itself. So it's shared across the whole project without file distinction — you store something shared across the whole thing, like the year in a whole game, and its creator is the project itself. So it's easiest to understand as a global variable used in the tpro.

Example:

File A (tpro):

```headlot
using hl;

global.all Year :: int = -2000; @= global.all is the valesto that declares a project global variable.

#main func updateYear ():(
   loop {
      time.asyncTime(30.5d);
      Year = Year + 1;
   };
):();
```

File B (hl):

```headlot
using hl;

global.addUsingGlobalVariable(Year); @= registers the Year global variable into the global variables currently in use

#main
module yearModule();

#yearModule.nextYear func nextYear (time :: int):(
   Year = Year + time;
):();
```

You can implement the year in a game directly like this.

And the basic operating principle of both the global variable and the tpro global variable in this global is the same.

First, when you use the global module in this project, it first makes a queue called global in this project module. If there's already a queue named global and that queue's creator is the global module, it keeps using that queue, and if the creator of the queue named global isn't global, it errors.

So this global queue stores everything in the global queue whenever another file manipulates year directly, or declares a global variable or a tpro global variable. Then, when changing the value of that variable or getting it, each function asks this global queue directly with ask. Then the global queue responds, and that's how this global variable is implemented. But an ordinary global variable remembers the file that made this variable directly, so you have to write even the file's name to find what's in that file, while a tpro global variable is just stored in the project itself. That's the difference.

For reference, the naming convention here is camelCase for an ordinary global variable and PascalCase for a tpro global variable. For the detailed reason see the naming conventions section in the grammar.

### https

Sends an https request.

Sends an https request. With the .access function you can get the request result directly as a string. Example:

```headlot
var MyProject :: string = https.access("https://github.com/discunderbar/headlot-lang");
Line.addLine(MyProject); @... <!DOCTYPE html><head>...</head><body>...</body>
```

If you request an http URL it errors.
.access is something dangerous, so the function name was made to look dangerous.

It's just made for now and the details are undecided.

// TODO: in detail

### http

Sends an http request. With the .access function you can get the request result directly as a string. Example:

```headlot
var MyProject :: string = http.access("http://github.com/DiscUnderbar/Headlot-lang");
Line.addLine(MyProject); @... <!DOCTYPE html><head>...</head><body>...</body>
```

If you request https it errors.
.access is something dangerous, so the name was made to look dangerous.

It's just made for now and the details are undecided.

// TODO: in detail

### allHttpReqeust

Lets http and https requests go.

The difference from https, the difference from http, is that it can send both https and http requests.

// TODO: in detail

### python

Uses Python's execution method. Py FFI is made with this.

Maybe

// TODO: how do I implement this... ugh.

### html

Reads html code and converts it into a Yulist of the html form.

// TOOD: rough out the usage

### Json

A Yulist for data formats coming from outside

// TODO: Json coming from outside is this data structure called Json. Also, if you convert this current Yulist to Json, when exporting the information about this Yulist you might want to do it a bit differently — like including even the interception information about the Yulist — and there'd be a country for one more thing to do when parsing directly, and such

## 2. Compile pipeline

```
source code
   │
   ▼
[Lexer]    string → token stream
   │
   ▼
[Parser]   tokens → abstract syntax tree (AST)
   │
   ▼
[CodeGen]  AST → LLVM IR
   │
   ▼
LLVM       optimization + machine code generation + executable
```

Only the front end (Lexer, Parser, CodeGen) is implemented directly, and the hardest part — optimization and machine code generation — is handled by LLVM.

## 3. Design principle: Deep Module

Each compile stage is made a deep module of "narrow interface, deep implementation". Complexity is confined inside the module so it doesn't leak into other parts.

| Module  | Public interface            | What it hides inside               |
|---------|-----------------------------|-------------------------------------|
| Lexer   | `tokenize(source) → tokens` | character handling, whitespace skipping, number/string parsing |
| Parser  | `parse(tokens) → AST`       | grammar rules, operator precedence, error recovery |
| CodeGen | `generate(ast) → LLVM IR`   | IRBuilder manipulation, type mapping |

Since the interface is stable, even if you later change the internal implementation (e.g. the parsing algorithm, the IR generation strategy), the other modules aren't affected.

**Honest Deep Module**: keep the narrow interface and deep implementation, but **even if you hide algorithmic complexity (the complexity of the internal implementation), don't hide the cost**. Whether an allocation happens, whether it can error, where control is transferred (allocation, error, control transfer) — these are exposed in the interface. Hiding cost means the user can't predict performance, which conflicts with principle 1-A #1 (performance first). That is, "hide the complexity, but don't hide the expensiveness".

## 4. Implementation architecture (C++)

- **Token / Lexer:** `enum class TokenType`, `struct Token`
- **AST:** a node class hierarchy + the Visitor pattern
- **CodeGen:** assembling IR with the LLVM `IRBuilder` (e.g. `2 + 3` → `Builder.CreateAdd(...)`)
- **Build system:** CMake, linking the LLVM development libraries, C++17 or later

Note: LLVM's official "Kaleidoscope" tutorial covers this path (a simple language → LLVM native compilation) step by step, so use it as a skeleton reference.

-- *hl*