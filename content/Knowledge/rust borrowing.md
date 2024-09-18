---
---
parent:: [[Rust]]

# Summary
If you pass by reference you are "borrowing" and if you don't then you take ownership.

# Notes
So far as I have learned you deal with pointers and modification separately so for one you need to worry about whether you will take the var and whether you will be modifying the contents. Should it be a pointer this means modifying what it is pointing at and for value it means byte content
