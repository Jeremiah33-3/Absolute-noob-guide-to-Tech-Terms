# vim and LaTex for note-taking

## Table of content
- [Getting started](#Getting-started)
- [quick links](#quick-links)
- [command lines stuffs](#command-lines-stuffs)

## Getting started
1. Install LaTex
  - On Linux: `sudo apt install texlive-full` (Ubuntu/Debian) or equivalent (texlive, texlive-latex-extra).
  - On macOS: install MacTeX
  - On Windows: install TeX Live or MikTeX (search for their differences)
  - check on Terminal if it works: `pdflatex test.tex`
2. Manage vim plug-ins via [vim-plug](https://github.com/junegunn/vim-plug)
3. PDF Viewer Integration that syncs well with Vim
  - Linux: zathura (best integration with vimtex).
  - macOS: Skim (with inverse search configured).
  - Windows: SumatraPDF.
  - Setting up the Viewer:
```vim
let g:vimtex_view_method = 'general'
let g:vimtex_view_general_viewer = 'C:/path/to/SumatraPDF.exe'
let g:vimtex_view_general_options = '-reuse-instance -forward-search @tex @line @pdf'
```
4. Install Plugins to support workflow
  - [vimtex](https://github.com/lervag/vimtex) → full LaTeX IDE inside Vim
  - Snippets: [UltiSnips](https://github.com/SirVer/ultisnips) + [vim-snippets](https://github.com/honza/vim-snippets) → LaTeX snippet expansions (e.g. typing eq + <Tab> → inserts equation environment).
  - LSP (Language Server Protocol) support (autocompletion, linting): coc.nvim or nvim-lspconfig with [texlab](https://texlab.netlify.app/)
5. configure .vimrc file to support plugins
6. Save .vimrc file and install all plugins/viewer via this command: `vim +PlugInstall +qall`
7. Write your own snippets in a file under a diectory with path looking sth like this: `~/.vim/UltiSnips/tex.snippets`
8. Defining a main file for the latex to let VimTex know which file to compile
  - put in the main file as well as subfiles: `%! TEX root = main.tex`


## quick links
- [vim cheatsheet](https://scthornton.github.io/cheatsheets/vim_cheatsheet/)
- [latex cheatsheet in general](https://wch.github.io/latexsheet/)
- [more comprehensive latex with math](https://quickref.me/latex.html)

## command lines stuffs
Fun fact: in CMD of Windows, we can run `curl`

Powerful Windows terminal trick
- remove all files except certain files: `Get-ChildItem -Recurse -File | Where-Object { $_.Extension -ne ".pdf" } | Remove-Item`
