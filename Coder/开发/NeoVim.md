### GoToPreview 
```shell
nnoremap gpd <cmd>lua require('goto-preview').goto_preview_definition()<CR>
nnoremap gpt <cmd>lua require('goto-preview').goto_preview_type_definition()<CR>
nnoremap gpi <cmd>lua require('goto-preview').goto_preview_implementation()<CR>
nnoremap gpD <cmd>lua require('goto-preview').goto_preview_declaration()<CR>
nnoremap gP <cmd>lua require('goto-preview').close_all_win()<CR>
nnoremap gpr <cmd>lua require('goto-preview').goto_preview_references()<CR>
```

### Printer
```shell
gp
```
### SymbolsOutline
#### 1.KeyMaps

|Key|Action|
|---|---|
|Escape|Close outline|
|Enter|Go to symbol location in code|
|o|Go to symbol location in code without losing focus|
|Ctrl+Space|Hover current symbol|
|K|Toggles the current symbol preview|
|r|Rename symbol|
|a|Code actions|
|h|fold symbol|
|l|Unfold symbol|
|W|Fold all symbols|
|E|Unfold all symbols|
|R|Reset all folding|
|?|Show help message|
#### 2.Commands
| Command                                                    | Description            |
| ---------------------------------------------------------- | ---------------------- |
| `:SymbolsOutline`                                          | Toggle symbols outline |
| `:SymbolsOutlineOpen`                                      | Open symbols outline   |
| ![[Pasted image 20240318101548.png]]`:SymbolsOutlineClose` | Close symbols outline  |