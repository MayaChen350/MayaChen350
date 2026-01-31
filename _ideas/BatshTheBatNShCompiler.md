# Batsh, the batch and SHell compiler

## Why?

Sounds fun! 

Also, it's annoying to be writting a script twice, especially when you don't even have the ways to test it sometimes.

## Description

Batsh is for agnostic shell scripting. It compiles to either batch, for windows use, or a POSIX `sh`.

Batsh has its own unified syntax. It makes you write a script once that can be compiled fast for both windows and unix system, in its respective shell scripting language with its own quirks.

Exemples: 

- `mdir` will be converted to `mkdir` on sh and `md` on batch.
- `/` will be `\` on windows.
- Some apps in PATH will be either `app` or `app.exe`

### Features (or ideas)

- Unified, agnostic syntax
    - Syntax for sections for specific shell
- Extensible compiler with extensions (acting as dependencies) for additional apps syntax

- Built-in interpreter (if atp it's not already better to make the interpreter the main project and the compiler an extra app sharing code)

#### Extensions

Since it's impossible to make something completely agnostic and bundle it all in an app in an efficient way, due to the numerous amount of different apps possibly having different syntax/extensions, Batsh can be extended with *extensions*. Those extensions add extra agnostic syntax.

A general one for development should likely be made officially.

Those extensions should be stored with the app data or somewhere else on windows maybe.

## Tools to use probably

- Whatever programming language working well
- Access to both windows and an UNIX(-like) os able of using `sh`

## References

When I wrote that idea down, someone traveled back in time to do it (source: trust)  

Keeping it as reference:  
https://github.com/batsh-dev-team/Batsh

## When possible?

When I'll have a lot of time to waste
