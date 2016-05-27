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

However, there is only one truly low-level language - Assembly. Assembly is almost 1:1 to the actual instructions that will be executed by the processor. All that said, there are a few differences - 
 - Instructions are represented by a small string of letters (`add`) rather than their numeric form (`4C`).
 - Extra, non-existent instructions are there to make certain common tasks more convenient (for example, `li r3, 5` is translated into `add r3, 0, 5`).
 - Numbers can be written as decimal (base-10, `27`), hexidecimal (base-16, `1B`) or binary (base-2, `11011`) whereas computers can only read binary (or hexadecimal, which is pretty much interchangable with binary)
 - There's a huge number of differences that make Assembly code more human-readable: Naming functions and marking where they start and finish, for example.
 
For all these reasons, Assembly code still needs to be translated into what we call "machine code" (the sequence of ones and zeroes that a processor can actually interpret) before it can be executed.
This job is done by an "assembler" - a program that's in charge of swapping out all the human-readable stuff (`add` and `func_writeFilesToSDCard`) into computer-readable stuff (`4C` and `080D43C0`). You might be able to think of it as the "compiler" for Assembly.
Even with all these additions, Assembly is still incredibly close to the real instructions. For this reason, it's very easy to change between Assembly and machine code.

There is another thing to consider when learning Assembly - the processor you want to learn. Simply put, there are many different "architectures" (or types) of processors - 80x86 (often shortened to x86 or 32-Bit), amd64 (64-Bit), ARM (often used in mobile devices), PowerPC (already mentioned) and many more...
Each of these machines have their own uniqe setups and have different sets of instructions. For this reason, there are several different varieties of Assembly, one for each architecture.
This tutorial will cover PowerPC Assembly. Another thing worth noting is the different syntaxes of Assembly - that is, there are several different ways of notating Assembly. This is a matter of preference.

For example, all of the following lines of Assembly are exactly the same; they are simply written in different syntaxes.
```asm
addi r3, r4, 3 #Intel Syntax (my favourite)
addi %r3, %r4, 3 #AT&T/GAS Syntax (Used by the GNU Assembler)
addi 3, 4, 3 #"Raw" Assembly (how the computer sees it)
```
See how the different syntaxes change how the code is notated? In most cases you'll be using Intel or AT&T syntax, but it's worth knowing about the third syntax.
You may be wondering what these "r#" things are. We'll cover them in just a bit.

## Bits, bytes and bobs
As you might know, computers read, think and breathe binary. Since we're working with a language that's so close to the metal we'll need to have at least a basic understanding of binary and its sister system, hexadecimal.

### Binary
When you count "normal" numbers (1 up to 10) you are counting in what we call the decimal system. You could think of this as having 10 different states of your (single-digit) number - It could be 0, 1, 2, 3 etc. 
Computers, however, don't have 10 states of a number. This is because they need to transport numbers around internally with electricity, which only has two states - on or off.
For this reason, computers don't count in the decimal system - they count in binary. Binary is like any other number system.

#### Place Value
When you count in decimal (or base-10), each digit represents how many of its place value there is. For example, the number 235 translates to 2 hundreds, 3 tens and 5 ones. For this next bit you'll need to think of 1 as 10<sup>0</sup>, 10 as 10<sup>1</sup> and 100 as 10<sup>2</sup> and so on.
In binary, instead of thinking in powers of 10 (like decimal) we think in powers of two. This is best expressed with a table - 

**Decimal**
|Number|10<sup>4</sup>|10<sup>3</sup>|10<sup>2</sup>|10<sup>1</sup>|10<sup>0</sup>|
| ---- |:------------ |:------------ |:------------ |:------------ |:------------ |
|96325 |9             |6             |3             |2             |5             |
|10420 |1             |0             |4             |2             |0             |