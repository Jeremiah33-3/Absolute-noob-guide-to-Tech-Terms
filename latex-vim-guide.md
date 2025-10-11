# vim and LaTex for note-taking

## Table of content
- [Getting started](#Getting-started)
- [quick links](#quick-links)
- [vim hacks](#vim-hacks)
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
  - some more guide: [workflow](https://www.bing.com/ck/a?!&&p=34b0af5202c2cf0883e45f161ac52a9a6d30a9702b4aed033c2ec7712660ac80JmltdHM9MTc1OTE5MDQwMA&ptn=3&ver=2&hsh=4&fclid=233d489c-9cda-61f4-28be-59689d9f601d&psq=how+to+see+ultisnips+latex+snippets&u=a1aHR0cHM6Ly9lam1hc3RuYWsuY29tL3R1dG9yaWFscy92aW0tbGF0ZXgvdWx0aXNuaXBzLw)
  - a [product](https://github.com/ckunte/latex-snippets-vim) developed for LaTex snippets
8. Defining a main file for the latex to let VimTex know which file to compile
  - put in the main file as well as subfiles: `%! TEX root = main.tex`


## quick links
- [vim cheatsheet](https://scthornton.github.io/cheatsheets/vim_cheatsheet/)
- [latex cheatsheet in general](https://wch.github.io/latexsheet/)
- [more comprehensive latex with math](https://quickref.me/latex.html)

## vim hacks

🖱️`Select` mode:
- enter `VISUAL` mode then press Ctrl G

🔍Find and Replace/ Select:
- [using the :s command](https://linuxize.com/post/vim-find-replace/)
  - `:%s/<pattern>/<replacement>/g`: find and replace all occurences of the specific pattern
- `:set hlsearch`: highlight all occurences of a word under the cursor
- `ggVG`: selecting the entire text like Ctrl + A 

## command lines stuffs
Fun fact: in CMD of Windows, we can run `curl`

Powerful Windows terminal trick
- remove all files except certain files: `Get-ChildItem -Recurse -File | Where-Object { $_.Extension -ne ".pdf" } | Remove-Item`

**More details of PowerShell Scripting**:
- PowerShell (scripting framework): a task automation and configuration management framework developed by Microsoft.
  - It uses a command-line shell and a scripting language built on the .NET framework (enabling the creation of complex scripts for automating administrative tasks).
  - PowerShell is especially powerful for system administration, file management, automation, and working with Windows environments, though it's also cross-platform now (Windows, macOS, Linux).
  - Key features:
    1. Uses cmdlets (like Get-ChildItem, Remove-Item) which are built-in commands. (object-based pipelines: Unlike traditional shells that process text streams, PowerShell's pipeline passes objects between commands (called cmdlets), allowing for more powerful and precise manipulation of data.)
    2. Supports object-oriented pipelines (unlike traditional shells that pass plain text).
    3. Can interact with the file system, registry, processes, services, and even APIs.
- A `.ps1` file is a PowerShell script file.
  - It contains a sequence of PowerShell commands and logic.
  - You can run it to automate tasks like file cleanup, backups, system checks, etc.
Example execution of a file:

```Powershell
# Remove all files except PDFs and a specific file
$filesToDelete = Get-ChildItem -Recurse -File | Where-Object {
    $_.Extension -ne ".pdf" -and $_.Name -ne "keep_this_file.txt"
}

# Preview what will be deleted
$filesToDelete | Select-Object FullName

# Optional: Confirm before deletion
$confirmation = Read-Host "Do you want to delete these files? (Y/N)"
if ($confirmation -eq "Y") {
    $filesToDelete | Remove-Item
    Write-Host "Files deleted."
} else {
    Write-Host "Deletion cancelled."
}
```
✅ Steps to run it:

1. Save the script as cleanup.ps1.
2. Open PowerShell.
3. Navigate to the folder where the script is saved.
4. Run the script: `.\cleanup.ps1`
5. Note: might need to adjust *execution poliy* to enable script running: `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`

**learning points**:
- object properties example:`Select-Object` is used to choose specific _properties_ from objects in the pipeline -- `FullName` is a property of a file object that gives the complete path to the file.
- `|`: also pipes the output from the previous command into the next command. (just like Linux, except, Linux shells pass text between commands.PowerShell passes objects, which makes it more flexible for scripting and automation.)
