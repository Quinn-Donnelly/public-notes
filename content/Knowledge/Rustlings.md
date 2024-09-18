---
tags:
  - tutorial
---
parent domain:: [[Rust]]
Going to walk through rustlings project to get feet wet with `rust`
[Rustlings](https://github.com/rust-lang/rustlings)

For rust learning and explanations using these [docs](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)

# Variables

## Showdowing
You can redefine var with same name this will create new var under the hood and allows you to remain mutation less even when you need to change types.
## Const
Good to note that types must be annotated with types 

# Functions
Rust like that `snake_case` style functions back to my olden days of C world

Order of definitions for functions doesn't matter

implicit returns are the last expression in the function. Note that rust cares about the difference between statements and expressions. It's the usual computer science definition in that expressions return values and statements don't

# Control Flow
noticed my auto completion and language features weren't all there going to get those working first.

# Move
In rust the heap variables will be "moved" when they are passed to a function. This results in them going out of scope in their source function.

This occurs based on data type of the variable. If it has the `Drop` Trait if so then when passed to a function the variable will be moved. If the variable's data type has the Trait `Copy` then when passed to a function it will be copied thus keeping the original reference in scope and valid. These traits are mutually exclusive.

You can force a deep copy of a `Drop` data type by calling `Clone` (if the data type implements that trait)