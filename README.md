# PowerPC 101
A from-scratch PowerPC Assembly tutorial, focusing on reverse-engineering (reading code, not writing it). Very WIP.
This is aimed towards REing Wii U stuff, so keep that in mind.

## So, what's a PowerPC?
PowerPC (PPC for short) is a type of processor. It was introduced in 1994 and was used in Apple computers up until 2006. Today you can find PowerPC processors in video game consoles, modern Amiga computers, and other specialised situations.
The term "PowerPC" can also apply to the Assembly language used to program the processor, depending on the context.

## What's Assembly?
There's a bit of explaining needed for this one, so please bear with me.
A basic processor will take in an "instruction" and some data, operate on the data based on the instruction, then move on to the next instruction.
For example, the instruction could be `add` and the data `2` and `3`. In this case, the processor would look at the instruction `add` and knowing that it needs to add the data together, it will, resulting in 5.
It's worth noting that the processor won't read the instruction as "add" - computers don't understand words, only numbers. For this reason the instruction will likely be represented as "4C" or something similar.
Anyway, once the processor has executed an instruction it will then move on to the next one. You may be wondering where our answer (5) goes - this will be covered later! First we need to talk about how we program these instructions into our processor.
As you may know, there are many programming languages out there, each unique and allowing a programmer to write code in a different way.

A characteristic of different programming languages is whether they are considered "low-level" or "high-level". High-level languages are heavily abstracted - that is, they are fairly far away from what the processor is actually doing.
Examples of high-level languages include Python, Lua and Java (which is so abstracted it technically doesn't run on the processor at all!)
Low-level languages are much "closer to the metal" - that is, they are very similar to the instructions that the processor will end up running. Low-level languages include C, Pascal and Fortran.

However, there is only one truly low-level language - Assembly. Assembly is almost 1:1 to the actual instructions that will be executed by the processor. There are a few differences, however - 
