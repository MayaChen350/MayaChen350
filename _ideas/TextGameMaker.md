# Text Game Maker

## Why?

That probably exists, but maybe making my own could be fun, maybe.

## Description

I had forgotten about it when I wrote this Text Game Maker idea in class, but about almost a year before, I wrote a kind of "dialog DSL" (documented in another file) which has a different syntax than the one thought for this one.

However, this one is for making entire games.

While I am a Linux user, Batch actually makes it pretty simple to write textual games if you run them through Wine, and works on Windows obviously.

But it's still weird to write things in Batch also the number of `echo` everywhere is kinda awful... So how about another dsl?

### Specs

(I wrote about those in class, those are small notes I wrote down after a lot of thinking, it might be flawed still as I was trying to listen to my philosophy class in the same time)

The game is written in C.

The text files are written in an assembly file with absolutely minimal things inside, it's mostly to write `.incbin` inside.

The project is to be cloned and made through the makefile, there's already C handling the game.

There are two versions for this thing:

#### Interpreted

The files are included as is, and they are read line by line to know what to do.  
Probably not visibly slower, but takes more space.

Good when testing.

### Compiled

This version I overthought it a lot to make it very optimized, even if almost useless since it's just terminal based but it's still nice to have things as more lightweight as possible (for me)

In this version:

- The compilation is slower
- The size is smaller
- Good for releases or sharing
- A python script makes necessary files
- The text are recreated to spare spaces
- The text is included in a file all text beside eachother
- A file is created containing all the offset for every lines to know where each strings end

The special file just mentioned is special because it is indexed for every lines, meaning if you go up by 4 bytes, you'll get the offset in the text file of the next string.  

However, this is not always the case.

Each offset can only stores until 31 bits. The first bit define if the next lines are dialogue choices, and in the dialog choices, the line offset with the first bit set defines the last dialog choices.  
After those, there are indexed for each choices, a value for the line offset in that very line offset array to jump to.  

Note that this is fine because, normally, the dialog choices should always jump to somewhere. If it continues further, it will have the index of the next line, therefore, it works fine because the program will never accidentally consider the line offset index values like actual line offset values.

In this version, when the program is initialized for fast access because micro-optimization is cool, a `struct` is created in the stack, containing necessary values to for the game to work:

Like:

- The story counter (void* to the current address in that ""Indexed"" line offset array, defined in global, from an `extern` label (because it's defined with `.incbin` in asm)
- ...etc

Note that those also be defined as global:

- void* line offset array (extern, defined in ASM (`.incbin`) in its own section preferably (like .raw_data or smth))
- char*/(preferably a char[size_of_that_file/array]) optimized text chunk (extern defined in ASM again)

## Tools to use probably

- C
- LLVM maybe for optimizing further
- gcc

## When possible?

Whenever I feel like it, can be started anytime.
