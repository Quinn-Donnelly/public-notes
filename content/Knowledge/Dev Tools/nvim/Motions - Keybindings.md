---
tags: []
---
parent domain:: [[vim]]
similar:: [[Typing]] #devtool 

Going to work on practicing some more advanced motion usage. Though to do this there are some holes in my current motion usage I need to shore up. 

`v` for visual mode which is something I almost never use. highlights then `y` to `yank` `p` in normal mode also will paste. *note: deleting will overrite the same register as yank*
normally i delete to paste so I should be fine with that

Going to work on rust whilst working on motions so that I can have some practical examples to work on movement with.

Helpful thing to know with some of my searches and hotkeys they will open the quickfix window which you can open with `ccopen` close with `ccl` or `cclose`

`C-p` is my go to previous selection 
`C-n` is my go to next selection
These both work in pop up windows and in my cmp completions

`^` beginning of line non white space
`$` end of line non white space

`nmap` shows normal mode mappings. Very useful I assume the other modes mappings follow a similar pattern.

`C-w` in vim will allow you to then use the movement home row to move panes in vim. Useful for the toggle windows like undo tree