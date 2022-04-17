---
layout: post
title: ~/
description: Workstation
image: assets/images/pic88.png
nav-menu: true
---

<!-- Main
<div id="main" class="alt">
<section id="one">
	<div class="inner">
		<header class="major">
			<h1>My ThinkPad</h1>
		</header>
<p>I use zsh/tmux and NeoVim with all the fixings</p>
-->
<header class="major">
  <h1>Workstation Configuration</h1>
</header>


Neovim:
------

vim-plug:

{% highlight shell %}
:PlugStatus
Finished. 0 error(s).
[============]

- vim-polyglot: OK
- matchit: OK
- vim-fugitive: OK
- vim-easy-align: OK
- mkdx: OK
- ddc.vim: OK
- markdown-preview.nvim: OK
- nerdtree: OK
- nord-vim: OK
- ctrlp.vim: OK
- coc.nvim: OK
- nerdcommenter: OK
{% endhighlight %}



nvim conqueror of completion:
{% highlight shell %}
Update finished

- ✓ coc-docker Current version 0.5.0 is up to date.
- ✓ coc-git Current version 2.4.9 is up to date.
- ✓ coc-json Current version 1.4.1 is up to date.
- ✓ coc-markdownlint Current version 1.12.4 is up to date.
- ✓ coc-prettier Current version 9.2.3 is up to date.
- ✓ coc-pyright Updated to v1.1.235
- ✓ coc-sh Current version 0.6.1 is up to date.
- ✓ coc-snippets Current version 3.0.8 is up to date.
- ✓ coc-spell-checker Current version 1.2.0 is up to date.
- ✓ coc-tsserver Updated to v1.10.0
- ✓ coc-yaml Current version 1.7.5 is up to date.
{% endhighlight %}

~/.config/nvim/coc-settings.json<br>

{% highlight shell %}
{
  "coc.preferences.formatOnSaveFiletypes": ["py", "yaml", "json"],
  "python.linting.flake8Enabled": true,
  "python.formatting.provider": "black",
  "snippets.userSnippetsDirectory": "~/.config/nvim/snippets/"
}
{% endhighlight %}

~/.config/nvim/init.vim

{% highlight None %}

"MARKDOWN MACROS
let g:mkdx#settings     = { 'highlight': { 'enable': 1 },
                        \ 'enter': { 'shift': 1 },
                        \ 'links': { 'external': { 'enable': 1 } },
                        \ 'toc': { 'text': 'Table of Contents', 'update_on_write': 1 },
                        \ 'fold': { 'enable': 1 } }
let g:polyglot_disabled = ['markdown'] " for vim-polyglot users, it loads Plasticboy's markdown
                                       " plugin which unfortunately interferes with mkdx list indentation.
                                       "
                                       "
" trailing whitespace
match ErrorMsg '\s\+$'
function! TrimWhiteSpace()
    %s/\s\+$//e
endfunction
autocmd BufWritePre * :call TrimWhiteSpace()

if empty(glob('~/.config/nvim/autoload/plug.vim'))
  silent !curl -fLo ~/.config/nvim/autoload/plug.vim \
  --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall
endif

call plug#begin('~/.config/nvim/plugged')
Plug 'arcticicestudio/nord-vim'
Plug 'tpope/vim-fugitive'
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'SidOfc/mkdx'
Plug 'Shougo/ddc.vim'
Plug 'junegunn/vim-easy-align'
Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install'  }
Plug 'ctrlpvim/ctrlp.vim'
Plug 'preservim/nerdcommenter'
Plug 'tmhedberg/matchit'
Plug 'scrooloose/nerdtree'
Plug 'arcticicestudio/nord-vim'
Plug 'sheerun/vim-polyglot'
"Plug 'jiangmiao/auto-pairs'

call plug#end()

" Give more space for displaying messages.
set cmdheight=2
" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=300
" Don't pass messages to |ins-completion-menu|.
set shortmess+=c
inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"
function! s:check_back_space() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion.
if has('nvim')
  inoremap <silent><expr> <c-space> coc#refresh()
else
  inoremap <silent><expr> <c-@> coc#refresh()
endif

" Make <CR> auto-select the first completion item and notify coc.nvim to
" format on enter, <cr> could be remapped by other vim plugin
inoremap <silent><expr> <cr> pumvisible() ? coc#_select_confirm()

" Use `[g` and `]g` to navigate diagnostics
" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list.
nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window.
nnoremap <silent> K :call <SID>show_documentation()<CR>

function! s:show_documentation()
  if (index(['vim','help'], &filetype) >= 0)
    execute 'h '.expand('<cword>')
  elseif (coc#rpc#ready())
    call CocActionAsync('doHover')
  else
    execute '!' . &keywordprg . " " . expand('<cword>')
  endif
endfunction

set cc=120                  " set an 80 column border for good coding style
set autoindent              " indent a new line the same amount as the line just typed
set mouse=a                 " enable mouse click
set clipboard=unnamedplus   " using system clipboard

colorscheme nord
{% endhighlight %}

~/.config/nvim/snippets<br>

{% highlight shell %}
~/.config/nvim/snippets/
markdown.snippets  python.snippets    sh.snippets
{% endhighlight %}

Zsh/tmux:
------

~/.zshrc
{% highlight shell %}

# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

export ZSH="$HOME/.oh-my-zsh"
alias vim=nvim
export TERM=xterm-256color
DEFAULT_USER=agardner

export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH"
bindkey -v
set -o vi

# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="agnoster"

plugins=(
    git
    docker
    docker-compose
    kubectl
    colored-man-pages
    git-flow
    tmux
    colored-man-pages
)

#Plugins list
#https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins


ZSH_TMUX_AUTOSTART=true
source $ZSH/oh-my-zsh.sh
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
{% endhighlight %}


~/.tmux.conf
{% highlight shell %}

set -g default-shell /usr/bin/zsh
set -g default-command /usr/bin/zsh
setw -g mode-keys vi
set -g prefix C-d
unbind C-b
bind C-d send-prefix
unbind ^A
bind ^A select-pane -t :.+
set-window-option -g mode-keys vi
bind-key -T copy-mode-vi 'y' send -X copy-pipe-and-cancel "xsel --clipboard -i"
bind-key y set-window-option synchronize-panes
set -g mouse on
{% endhighlight %}

<!--
</code></pre>
</div>
-->
