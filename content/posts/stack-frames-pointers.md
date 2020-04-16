---
title: Stack Frames & Pointers
subtitle: A compiler's dream...
category:
  - Binary Exploitation
author: Cameron Wickes
date: 2020-04-15T20:57:07.206Z
featureImage: /uploads/bufferoverflowstackframes.jpg
---
*Now that we’ve covered the basics of the stack, addressed in [Callers, Callees, Functions and Registers](https://www.cameronwickes.com/callers-callees-and-stack-frames), we can start to move onto more complex low-level operations and how the stack is made up. For the sake of simplicity, I will illustrate x86 calling convention in this article, but do be aware that in 64-bit binaries, the arguments may not appear on the stack. Read more [here](https://www.cameronwickes.com/calling-conventions-x86-x64).*

**Important Registers** 

We should now know that there are eight main general-purpose registers in 32-bit systems:

```
EAX, EBX, ECX, EDX, ESI, EDI, EBP, and ESP
```

We should also know that 64-bit systems extend those eight core registers to 8 bytes, and add eight extra registers: 

```
RAX, RBX, RCX, RDX, RDI, RBP, RSP, R8, R9, R10, R11, R12, R13, R14, R15
```

We also have a very important special purpose register called the EIP / RIP (x86 and x86-64 respectively).

The three main registers of interest are shown below, with a description of what they do:

* ESP – The Extended Stack Pointer – Points to the top value of the stack
* EIP – The Extended Instruction Pointer – Points to the current instruction being executed
* EBP – The Extended Base Pointer – Points to the top of the current stack frame (more on that in a bit)

**The Stack** 

The stack is space in memory, that is used during runtime to:

* Hold local variables
* Hold arguments to be passed to the function (if using x86-64)
* Keep track of which functions were called before the current function

To keep data organised, and so that the program can know what data is where, we use stack frames to keep track of where we are and what we are holding. 

**Stack Frames** 

Each time a new function is called, there needs to be a new stack frame created to organise the data involved with executing the function and resuming previous operation. A diagram of the stack, as well as caller and callee stack frames are shown below to help you understand what they are and how they are made up:

![](/uploads/stackframescropped.jpg)

The stack frame is constructed like shown:

1. Old Base Pointer (EBP) is pushed onto the stack
2. Stack Pointer (ESP) is moved into the Base Pointer Register (EBP) to become the current stack frames’ base pointer
3. Register values we want to save, as well as any local variables are pushed onto the stack
4. If the function calls another function at any point, it will push the arguments in reverse order (cdecl) and then push the return address onto the stack Once inside the function, we can access our arguments from the EBP like shown: 

   `mov ecx, [%ebp + 8]`

   `Moves the value at %ebp + 8, to ecx for easier access. (+8 ignores the return address)`

When the function finishes executing, we apply the opposite operation, and deconstruct the stack:

1. Any local variables are popped off the stack, and any saved registers get restored
2. Base Pointer (EBP) is moved into the Stack Pointer Register (ESP)
3. The old base pointer previously pushed is then popped off the stack and stored in (EBP), to become the new function base pointer, since previous execution will be resumed, and we need to move down a stack frame
4. The return address is popped off the stack and stored in EIP, which resumes previous execution Since we are using x86 calling convention, it is the callers job to clean up the function parameters still laying on the stack.

**Buffer Overflows** 

Now that we have a basic knowledge about stack frames, we can look at how a typical buffer overflow would work.

![](/uploads/bufferoverflowstackframes.jpg)

You can see the basic concept of a buffer overflow illustrated above. We provide an amount of data larger than the program is expecting, and we actually start to overwrite the stack. If we can overwrite the return address of the previous function, we can control the flow of the program and achieve arbitrary code execution.