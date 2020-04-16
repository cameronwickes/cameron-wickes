---
title: Callers, Callees and Stack Frames
subtitle: An introduction to functions...
category:
  - Binary Exploitation
author: Cameron Wickes
date: 2020-04-11T22:14:02.953Z
featureImage: /uploads/pankaj-patel-yeaofwsdzgm-unsplash.jpg
---
*This article is the first in a series of many, addressing binaries (programs) on 32 and 64-bit machines and how they operate.  It does require some basic knowledge of programming, and it helps if you have a background in C.* 

**Callers and Callees** 

In a programming language, we have functions/subroutines. They are blocks or chunks of code that perform a specific task. We can pass things into a function using ‘parameters’ and produce things from a function using ‘return values’.  Take a look at an example below:

![](/uploads/caller.png)

The function sum calculates the sum of two numbers, x and y, which get passed into the function. The function uses a return value to provide the sum back to the computer. \
Fun is separate function which doesn’t have any parameters, nor does it return a value. Inside it declares two local variables, which can only be accessed inside function. These can then be passed into functions or manipulated further but get forgotten once the function is finished. In this case, we call the sum function with the two local variables and store the return value in a new variable called sumAB. 

We describe fun as the ‘caller’ function and sum as the ‘callee’ function. This terminology can also apply to multiple functions, like below:

![](/uploads/callee.png)

In this example, *Alpha* is a caller and *Beta* is a callee. However, *Beta* calls *Gamma*. *Beta* is therefore also a caller, and *Gamma* is a callee. \
*Alpha* is a caller, *Beta* is both a caller and a callee, and *Gamma* is a callee. 

**The Stack** 

At run-time, we need to allocate space to store all these local variables, along with other useful information about where we are in the program. 

Introducing the stack. A data structure managed by the compiler that holds all sorts of useful information during runtime. It grows down, from higher to lower address, and it operates using LIFO (Last In, First Out). This means that the most recent data item pushed on is the first to come off.  N.B. You may see illustrations of the stack growing upwards. This is just to help users understand the workings of the stack in a visual way but is not how it works during runtime. 

There are a couple of operations of note regarding the stack:

* Push – This operation adds a supplied data item to the top of the stack
* Pop – This operations removes a data item from the top of the stack and returns it

**32 and 64-bit Registers** 

There are also important registers to be aware of when looking at how programs operate, many of which are detailed below. We will talk in depth about them in further articles. 32-bit systems have eight core general purpose registers (each of 32 bits/4 bytes):

```
EAX, EBX, ECX, EDX, ESI, EDI, EBP, and ESP
```

64-bit systems extend the eight core 32-bit registers to make them 64 bits/8 bytes long, and also add eight extra registers, R8-R15.

```
RAX, RBX, RCX, RDX, RDI, RBP, RSP, R8, R9, R10, R11, R12, R13, R14, R15
```

Note: On 64-bit systems, we can access the lower 32 bits of 64-bit registers using the E-- notation, instead of the R-- notation, and R-d instead of R- notation.  Example: RAX is a 64-bit register. EAX would access the lower 32 bits of the register.  Example: R10 is a 64-bit register. R10d would access the lower 32 bits of this register.