---
title: Calling Conventions (x86 & x64)
subtitle: What are they and why is it relevant?
category:
  - Binary Exploitation
author: Cameron Wickes
date: 2020-04-10T11:26:53.700Z
featureImage: /uploads/markus-spiske-1llh8k2_yfk-unsplash.jpg
---
Transitioning from 32-bit to 64-bit binary exploitation is a bit of a challenge, especially if you haven’t got your head around the differences in registers and calling conventions. In this article, I aim to address these variations, so you can understand what you need to do differently when dealing with the respective architectures.

If some of the terminology in this is a bit frightening, make sure to have a read of [Callers, Callees and Stack Frames](https://www.cameronwickes.com/callers-callees-and-stack-frames), a previous article which goes in depth on functions and what happens when they are called.

### **Calling convention**

Calling convention is essentially a contract between the caller and callee, which defines how parameters are passed into functions, what registers can be utilised inside the function, how return values are stored and who cleans up the stack after the function is complete.

**Arguments and Parameters** 

In 32-bit machines, arguments are pushed onto the stack before the call. These arguments should be pushed in reverse order, with the first parameter at the lowest address, and the last parameter at the highest address. Example: Say we had a function called funcA(int a, int b, int c). If we wanted to call this function, we would have to push our arguments onto the stack in the order C,B,A. This means that the function pops them off the stack in the right order (they will be popped to become A,B,C).

However, in 64-bit machines, arguments are not placed on the stack. Instead, the program uses it’s general purpose registers to store and pass these arguments to functions. 

The parameters of the required function fill the registers in the following order:

```
RDI, RSI, RDX, RCX, R8, R9
```

If we have floating point numbers, we don’t fill the aforementioned registers, but instead utilise the SSE registers designed by intel to handle floating point numbers.  \
They fill sequentially in the order XMM0 – XMM7.

Any further parameters that don’t fit into these registers get pushed onto the stack, lower to higher address, and the caller makes sure that all of the parameters on the stack are ‘8-byte-aligned’. If there is a variable number of arguments passed to the function, the number of arguments is pushed into the RAX register so the computer knows how many it is expecting.

**Execution of the Function**

Whilst executing a function, the machines can utilise any register for a particular purpose. However, there are some strict instructions for restoring them before the return call on both 32 and 64-bit systems. The following registers must be restored:

```
32-bit: EBX, ESI, EDI, EBP
64-bit: RBX, RSI, RDI, RBP, R12-15 (also XMM6-XMM15 in some cases)
```

There may also be some others registers that need to be restored, which is down to specific implementations and cases. Restoring the registers makes sure that everything is as it was before we entered the function, so we can correctly resume previous execution.

**Return Values**

The return value of the function (for both x86 and x86-64 calling conventions) is stored in the EAX and RAX registers respectively.  Notice that there are no other registers used for storing return values. This is because C code can only return one value from a function and doesn’t support multiple return values.

**Cleaning up the stack**

32-bit machines are compiled in a way that means the caller is responsible for ‘cleaning up the stack’ after the function has returned. When we called the function, we pushed the arguments, as well as the return address onto the stack. When the function returns, previous execution is resumed at the caller, but the arguments we pushed onto the stack earlier are still present. In 32-bit machines, the caller is responsible for cleaning up the stack, and removing anything that needs to be in there.

On the contrary, 64-bit machines are compiled such that the callee is responsible for ‘cleaning up the stack’ before returning, meaning the stack will be in order when the execution is resumed. 



### Putting all of this together

So how does this all fit together?

When we are exploiting a binary, there are plenty of ways this will fit in. Perhaps you have to call a win function with an argument of 1 to print a flag. This will require you to understand the calling convention, and how we pass arguments to functions. Should you push the argument onto the stack, or load into RDI with a handy gadget? Now you should know.