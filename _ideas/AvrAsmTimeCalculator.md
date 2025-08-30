# Time calculator in AVR ASM

## Why?

Date are more easily fitting within one single byte than regular numbers, and so that could be a great opportunity eventually to try AVR assembly.  
Programs in AVR assembly obviously run on AVR architecture, but with `qemu-avr`, that could actually make me do a calculator of the size of a few bytes!  

Maybe later, I could even put this code into some real calculator I could make with an arduino.

## Description

This calculator calculates time and dates. Basically, I want it to support date equal or less than 7 years, 11 months, 31 days, 59 minutes and 59 seconds.  
However, I don't know what I could do to calculate months as they all varies, and I don't want to use floating point numbers.

But then, how would I calculate say, 300 days (above 255)?  
Well I can do some bytes magic:

Let's say, I have 300 days, that's about... Okay writing this down right now and trying to calcute things... Maybe I should use two registers... I have like 32 in AVR anyway.

But you know what is going to compensate for that one extra byte?  
Well, I can put the months and the years in the same byte.  

Like, 12 fits pretty much in 4 bits. So I can use the 4 bits before for the number of years, if that reveals itself like a good idea in anyway, so I'm noting it down in case.  

I also want it to supports **additions**, **substractions**, **multiplications**, and if possible, divisions.  
Things are going to be like enums for now as I will seperate the implementation code from the rest, so it's easily rewritable for a physical device.  
But I can have things like:

```
0: 0
1: 1
2: 2
3: 3
4: 4
5: 5
6: 6
7: 7
8: 8
9: 9
10: +
11: -
12: *
13: = 
```

And everytime this is gonna be decoded with branches (a kind of switch case) to know what to do.  

The rest is pretty much obvious I hope.

## Tools to use probably

- AVR ASM
- AVR ASM toolchain (assembler, linker, compiler, objdump, etc)
- qemu-system-avr
- an arduino board (eventually)

## When possible?

When I'll have learned enough AVR assembly, then surely I'll be able to try this project out.
