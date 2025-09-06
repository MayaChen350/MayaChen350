# Dialog files/DSL

## Why?

When I was making a game on Godot, I thought making a library for Dialogs could be nice and useful for people.

## Description

I have two ideas for this:  

1. A specific file like `someone.dialog` with gdscript files to parse it.

2. A Clojure CLR DSL.

My initial idea was a file I'll be parsing, but considering Clojure can compile into CLR bytecode, maybe it could technically be C#. Maybe there's even some Lisp Dialect for GDScript.

If I make a Clojure CLR DSL, maybe I could even make it work with Unity that'd be fun.

### Specs

`#` defines an ID, it helps with jumping.

Dialogs are like trees, where you have multiple choices of dialogs that can make you go to other choices of dialogs.  

`->` switches between answers and normal dialogs.
`;` seperates dialogs.  
`;;` is for comments.  
`$` ignore a reserved character and make you able to use it in a dialog. (`$#`, `$>`, `$;` and `$$`) 
When the dialog is not jumping anywhere or isn't followed by anything, the dialog ends there.

Indentation should be used for branches clarity.

### Examples

#### Dialog File
```
#mainId Hello -> ;; this is the npc speaking "hello"
  Hi -> ;; this is an answer you can answer
    Dialog; ;; now the npc starts speaking again
    Dialog2; ;; and here
    Dialog3 -> ;; now it switches back to you answering
      No -> #mainId ;; this returns to #mainId
  Hello -> ;; another answer you can answer
    Thank you. ;; the dialogs ends here since it doesnt jump or continue after
#secondaryId Hey I know you!
```

#### Clojure DSL (or pseudo-that)
```clj
(dialog
  (:mainId "Hello" -> 
   (("Hi" ->
     ((Dialog)
     (Dialog2)
     (Dialog3 -> 
       (("No" -> :mainId)))
    ("Hello" -> "Thank you"))
  (:secondaryId -> "Hey I know you!"))
```

## Tools to use probably

- GDScript or a lisp dialect
- Godot or Unity to test things

## When possible?

Whenever I have time and know how Clojure DSL work.
