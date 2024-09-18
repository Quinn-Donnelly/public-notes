---
tags: []
---
supports:: [[neovim]]
parent domain:: [[Language Server Protocol]]

Presentation done at uk GopherCon [link](https://github.com/a-h/understanding-lsp.git)

The protocol will typically operate over standard in and standard out. Since requests can be interwoven the requests will have an `id` which the response will also send so that they can be matched up correctly.

Notifications are server driven and don't have an id as they are messages from the server that the client won't respond to. Looks like notifications can also come from the client as well?

This will require the use of a Mux since the messages will be racing to write to standard out to respond and if they interweave the message will corupt. 

[cooklang-go-lsp](https://github.com/aquilax/cooklang-go) will take a look at setting up a working example then will customize. This acutally ended up being a parser not and lsp

first will need to build the lsp and make sure the binary is on path. Following that we can configure it in our editor such as the following for neovim with a command line that will run an isolated neovim install with only the configs we point it to. 

```lua
vim.api.nvim_create_autocmd('FileType', {
  pattern = 'cook',
  callback = function()
    vim.lsp.start({
      name = "examplelsp",
      cmd = { "examplelsp" },
      root_dir = vim.fs.dirname(vim.fs.find({ ".examplelsp" }, { upward = true })[1]),
    })
  end,
})
```
```sh
nvim --clean -u ./neovim-config/init.lua pizza.cook
```

[go types for lsp protocol](https://github.com/sourcegraph/go-lsp)

[lsp example used](https://github.com/a-h/examplelsp)

got it set up and played around with it. the hard part isn't the actual lsp programming but the parser that you need to do. It's a shoutout back to the compiler building days keeping track of ranges and things it very important so that you can put your errors and feedback in the right places