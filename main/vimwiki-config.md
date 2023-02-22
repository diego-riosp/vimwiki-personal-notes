---
title: "VimWiki commands"

---

[Back](index.md)

## Pre-requisites:
Install the following dependences:

  ```bash
  sudo pacman -S vim neovim pandoc sed
  ```

## Configuration
In order to install vimwiki plugin and configure it in your neovim environment, you must perform the following procedure.

1. Create `init.vim` following these steps:

  ```bash
  cd ~/.config/nvim/
  mv init.lua lua/config.lua
  touch init.vim
  mkdir autoload
  ```

  Into `autoload` directory, you must charge the file `plug.vim` from this repository.

2. Now, edit the file `init.vm` exactly like this:

  ```bash
  let mapleader=" "
  lua require('config')
  set nocompatible
  filetype plugin on
  syntax on
  
  call plug#begin()
  Plug 'vimwiki/vimwiki'
  call plug#end()

  let g:vimwiki_list = [{'path': '~/path/to/wiki',
    \ 'path_html': '~/path/to/wiki/wiki_html',
    \ 'syntax': 'markdown',
    \ 'ext': '.md',
    \ 'custom_wiki2html': '~/path/to/wiki/wiki2html.sh'}]
  ```

  In `~/path/to/wiki` you must write the path where you expect create your wiki, as well as `~/path/to/wiki/wiki_html` is the path where you will store your wiki as `html` format (notice that this folder is into wiki proper folder).
  
  Now, get out from neovim with `:wq` and re-enter in order to reload the configuration. Being inside neovim again, type `<space>+ww`, and `:PlugInstall`. Wait for installation. When it finishes type `:q`, and afer `:wq`.

3. Create the bash script to convert `markdown` wikis in `html` files. Do:

  ```bash
  touch ~/path/to/wiki/wiki2html.sh
  ```

  Put into this file the following code:

  ```bash
  #!/bin/bash

  FORCE="$1"
  SYNTAX="$2"
  EXTENSION="$3"
  OUTPUTDIR="$4"
  INPUT="$5"
  CSSFILE="$6"

  FILE=$(basename "$INPUT")
  FILENAME=$(basename "$INPUT" .$EXTENSION)
  FILEPATH=${INPUT%$FILE}
  OUTDIR=${OUTPUTDIR%$FILEPATH*}
  OUTPUT="$OUTDIR"/$FILENAME
  CSSFILENAME=$(basename "$6")

  HAS_MATH=$(grep -o "\$\$.\+\$\$" "$INPUT")
  if [ ! -z "$HAS_MATH" ]; then
      MATH="--mathjax=https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  else
      MATH=""
  fi

  # >&2 echo "MATH: $MATH"

  sed -r 's/(\[.+\])\(([^#)]+)\)/\1(\2.html)/g' <"$INPUT" | pandoc $MATH -s -f $SYNTAX -t html --template=github.html5 -c $CSSFILENAME | sed -r 's/<li>(.*)\[ \]/<li class="todo done0">\1/g; s/<li>(.*)\[X\]/<li class="todo done4">\1/g' >"$OUTPUT.html"
  ```
4. Create the file `github.html5` following the instruction:
  
  ```bash
  touch /usr/share/haskell-pandoc/data/templates/github.html5
  ```
  
  and copy all the content from [here](https://github.com/jgm/pandoc-templates/blob/master/default.html5) to that file.
  
Now, you are able to convert `markdown` wikis into `html` files using the instruction `:VimwikiAll2HTML` within 
vimwiki.

---
[Back](index.md)
