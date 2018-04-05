# i3-vim-nav
Seamlessly change focus between i3 windows and Vim splits using the same hotkey.

NOTE: This is a fork of
[https://github.com/termhn/i3-vim-nav](https://github.com/termhn/i3-vim-nav)
because I had some issues with the original:
* Sending the Escape through xdotool does not work for me. So I just added
  another set of vim bindings for insert mode.
* The regex in the go binary did not always match my neovim window. I simplified
  it (but now it only works with neovim).

# Installation

## Dependencies

This depends on you having a couple packages installed. Most notably, `xdotool/libxdo`, the second of which should be installed as a dependency of the first. If you want to build the binary from source and you're on Fedora, you'll also need the `libxdo-devel` package. We also currently require you to be using a version of vim with either python or python3 support.

## Vim plugin

First, install the Vim plugin.
 
### Using vim-plug
In your .config/nvim/init.vim (neovim):

```vim
Plug 'termhn/i3-vim-nav'
	
" i3 integration
nnoremap <silent> <c-l> :call Focus('right', 'l')<CR>
nnoremap <silent> <c-h> :call Focus('left', 'h')<CR>
nnoremap <silent> <c-k> :call Focus('up', 'k')<CR>
nnoremap <silent> <c-j> :call Focus('down', 'j')<CR>
inoremap <silent> <c-l> <Esc>:call Focus('right', 'l')<CR>
inoremap <silent> <c-h> <Esc>:call Focus('left', 'h')<CR>
inoremap <silent> <c-k> <Esc>:call Focus('up', 'k')<CR>
inoremap <silent> <c-j> <Esc>:call Focus('down', 'j')<CR>
```
	
### Using Pathogen
1. cd ~/.vim/bundle
2. git clone https://github.com/termhn/i3-vim-nav
3. add the following to your .vimrc

```vim
" i3 integration
nnoremap <silent> <c-l> :call Focus('right', 'l')<CR>
nnoremap <silent> <c-h> :call Focus('left', 'h')<CR>
nnoremap <silent> <c-k> :call Focus('up', 'k')<CR>
nnoremap <silent> <c-j> :call Focus('down', 'j')<CR>
inoremap <silent> <c-l> <Esc>:call Focus('right', 'l')<CR>
inoremap <silent> <c-h> <Esc>:call Focus('left', 'h')<CR>
inoremap <silent> <c-k> <Esc>:call Focus('up', 'k')<CR>
inoremap <silent> <c-j> <Esc>:call Focus('down', 'j')<CR>
```
	
## i3 config

Then, in your i3 config (adjust the path to the executable as necessary if you installed it differently). Feel free to change the key bind as you please.

```
bindsym --release $mod+h exec --no-startup-id "~/.config/nvim/bundle/i3-vim-nav/i3-vim-nav h"
bindsym --release $mod+j exec --no-startup-id "~/.config/nvim/bundle/i3-vim-nav/i3-vim-nav j"
bindsym --release $mod+k exec --no-startup-id "~/.config/nvim/bundle/i3-vim-nav/i3-vim-nav k"
bindsym --release $mod+l exec --no-startup-id "~/.config/nvim/bundle/i3-vim-nav/i3-vim-nav l"
```

Note: I've gotten a bug where in some installations of i3, it seems to not respect user $PATH additions, even though it seems to recognize them in the variable. If it doesn't work when placed in a user $PATH directory, try hard-coding the path to the binary in the exec commands.
