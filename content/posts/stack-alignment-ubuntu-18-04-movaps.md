---
title: Stack Alignment, Ubuntu 18.04 & MOVAPS
subtitle: The three horsemen of the apocalypse...
category:
  - Binary Exploitation
  - ROP
author: Cameron Wickes
date: 2020-04-22T06:30:14.878Z
featureImage: /uploads/movaps.jpg
---
*Whilst on my quest to discover the difference in x86 and x86-64 binaries, I came across a ROP challenge which required the stack to be aligned properly for the exploit to complete. Having not come across a problem like this before, I had a look online to see if I could understand the problem further, but there seemed to be no concise explanation of how and why these issues fit together.  I’ve therefore compiled a short series of explanations about the MOVAPS issue, stack alignment and how a ROP chain may violate the rules set by certain instructions.*



**Stack Alignment** 

Let’s first take a look into stack alignment, an important aspect of compiler behaviour, which controls how the stack is laid out. The stack is ‘aligned’ when variables on the stack start at certain addresses depending on their size in memory. The ‘alignment’ pads the variable to a certain number of bytes, so they can be operated on in a single fetch. Looking at memory maps reveal the need for stack alignment quite clearly, where each address holds a single byte that can be accessed independently: 

![](/uploads/stackalignment.jpg)

You can see an example of non-stack aligned memory in Figure 2. We store a byte of data in the 0000 address and store a word of data in the address 0001, overlapping into 0002 (word = 2 bytes).  If we wanted to read the word at address 0001 & 0002, we would have to do two separate read operations. One would get 0000 & 0001, then the second would get 0002 & 0003. A separate combination operation would be required to combine the relevant bits of data between the two. In Figure 3, stack alignment is used to store the data, with the byte being padded/aligned and the word being stored in 0002 & 0003. Although not optimal for memory space, stack alignment boasts low computational complexity and higher access speeds.

**The SSE instruction set** 

The Streaming SIMD Extensions Instruction Set (SSE) is an extension instruction set to the x86 architecture, designed for signal processing and graphics processing by Intel.  The Instruction Set has four main categories:

1. SIMD Single-Precision Floating-Point Instructions \
   *These instructions operate on the XMM registers and memory to read/write, perform arithmetic, compare operands and convert values.*
2. MXSCR State Management Instructions \
   *These instructions save and restore the control of the XMM, MXCSR and status registers.*
3. SIMD Integer Instructions \
   *These instructions perform operations on the XMM registers.*
4. Caching Functionality & Ordering Instructions \
   *These instructions store, prefetch and serialise operations.*

\- *[Oracle](https://docs.oracle.com/cd/E26502_01/html/E28388/eojde.html)*

**Ubuntu 18.04 & MOVAPS**

Ubuntu 18.04’s version of GLIBC uses the SSE Instruction Set’s MOVAPS instruction to push data onto the stack in specific functions, such as printf.  The MOVAPS instruction, “moves a double quadword containing four packed single-precision floating-point numbers from the source operand (second operand) to the destination operand (first operand). When the source or destination operand is a memory operand, the operand must be aligned on a 16-byte boundary or a general-protection exception (#GP) will be generated.”

\- *[Carnegie Mellon University](http://qcd.phys.cmu.edu/QCDcluster/intel/vtune/reference/vc181.htm)*

The MOVAPS instruction does cause compatibility issues with a misaligned ROP chain, triggering the General Protection Exception when it tries to operate on non-16-byte-aligned data. So, if your ROP chain is generating a SEGFAULT and the faulting instruction is a MOVAPS, it will most likely be a dodgy stack alignment. 

The issue is shown below, with the failing instruction being the MOVAPS:

![](/uploads/movaps.jpg)

Let’s examine that MOVAPS instruction to see what’s going on under the hood: 

`movaps XMMWORD PTR [rsp+0x40], xmm0`

The MOVAPS instruction tries to move the four packed single precision floating-point numbers in the xmm0 register to the address of rsp+0x40.  Notice that we are using XMMWORD PTR, and \[ ] . This implies the destination operand is a memory operand, and the rules of 16-byte aligned data therefore apply. If our memory address is not 16-byte aligned, and our address (rsp + 0x40) is not a multiple of 16, the General Protection Exception will trigger, and a SEGFAULT will occur.

**Fixing Stack Alignment Issues** 

We could try and find a `sub rsp, 8` or an `add rsp, 8` gadget and add it to the start of our ROP chain to realign the stack, but there may not be any of these gadgets freely available within the program. A simpler solution would be to utilise our knowledge of the stack pointer (rbp) and how it functions.\

We should know that: 

*In x86 (32 bit) machines*

* Pushing something onto the stack results in the stack pointer (esp) decreasing by 4
* Popping something off the stack results in the stack pointer (esp) increasing by 4

*Whilst in x86-64 (64 bit) machines*

* Pushing something onto the stack results in the stack pointer (rsp) decreasing by 8
* Popping something off the stack results in the stack pointer (rsp) increasing by 8

Since our stack pointer can only be multiples of 8, and the SEGFAULT is caused because it’s not a multiple of 16, it must be because the stack pointer is aligned to an 8 and not a 16. \

If we push another gadget onto the stack (a simple ret will do), it will increment the stack pointer, making it a multiple of 16 to satisfy the MOVAPS instruction and make the 64-bit pain go away!