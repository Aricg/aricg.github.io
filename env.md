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
-->
<header class="major">
  <h1>Workstation Configuration</h1>
</header>

## LLM Helper

{% highlight shell %}

git clone https://github.com/Aricg/openai-gpt-api.git

{% endhighlight %}

{% highlight shell %}
vim ~/.openai_config
[DEFAULT]
api_key = sk-YOUR-API-KEY
model = gpt-3.5-turbo-16k
temperature = 0.5
{% endhighlight %}

{% highlight shell %}
sudo ln -s ~/Github/openai-gpt-api/gpt /usr/bin/gpt
{% endhighlight %}

{% highlight shell %}
usage: gpt [-h] [--file FILE [FILE ...] | --command-output {git_commit}]
           [--model MODEL] [--temperature TEMPERATURE] [--list-saved]

options:
  -h, --help            show this help message and exit
  --file FILE [FILE ...]
                        Provide one or multiple filenames to use as input
  --command-output {git_commit}
                        Choose a command to run and use its output
  --model MODEL         model to use for the chat completion
  --temperature TEMPERATURE
                        temperature to use for the chat completion
  --list-saved          List all saved input-output files and exit

{% endhighlight %}

 <p>zsh/tmux with NeoVim + plugins</p>

 ## Neovim:
```

#######################################################################


Do you want to send this message? [y/n/edit]: y
feat: add LLM Helper to env.md

Add instructions for setting up the LLM Helper, a command-line tool for OpenAI's GPT-3 API. This includes installation instructions and usage options.


{% endhighlight %}

<p>I use zsh/tmux and NeoVim with all the fixings</p>

## Neovim:

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

{% highlight json %}
{
  "coc.preferences.formatOnSaveFiletypes": ["py", "yaml", "json", "sh", "go",],
  "languageserver": {
    "go": {
      "command": "gopls",
      "rootPatterns": ["go.mod"],
      "trace.server": "verbose",
      "filetypes": ["go"]
    }
  },
  "diagnostic-languageserver.filetypes": {
    "vim": "vint",
    "markdown": [ "markdownlint", "mdl"],
    "sh": "shellcheck",
    "yaml": [ "yamllint" ],
    "cmake": [ "cmake-lint", "cmakelint" ],
    "py": "flake8",
  },
  "diagnostic-languageserver.formatFiletypes": {
    "python": ["black", "isort"],
    "sh": "shfmt",
    "cmake": "cmake-format",
  },
  "markdownlint.config": {
    "default": true,
    "line_length": false
  },
  "python.linting.flake8Enabled": true,
  "python.formatting.provider": "black",
  "snippets.userSnippetsDirectory": "~/.config/nvim/snippets/"
}
{% endhighlight %}

~/.config/nvim/init.vim

{% highlight None %}

"trim trailing whitespace
match ErrorMsg '\s\+$'
function! TrimWhiteSpace()
    %s/\s\+$//e
endfunction
autocmd BufWritePre \* :call TrimWhiteSpace()

if empty(glob('~/.config/nvim/autoload/plug.vim'))
silent !curl -fLo ~/.config/nvim/autoload/plug.vim \
 --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
autocmd VimEnter \* PlugInstall
endif

call plug#begin('~/.config/nvim/plugged')
Plug 'arcticicestudio/nord-vim'
Plug 'tpope/vim-fugitive'
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'SidOfc/mkdx'
Plug 'Shougo/ddc.vim'
Plug 'junegunn/vim-easy-align'
Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install' }
Plug 'ctrlpvim/ctrlp.vim'
Plug 'preservim/nerdcommenter'
Plug 'tmhedberg/matchit'
Plug 'scrooloose/nerdtree'
Plug 'arcticicestudio/nord-vim'
Plug 'sheerun/vim-polyglot'
"Plug 'jiangmiao/auto-pairs'
call plug#end()

" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list.
nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

set cc=120 " set an 80 column border for good coding style
set autoindent " indent a new line the same amount as the line just typed
set mouse=a " enable mouse click
set clipboard=unnamedplus " using system clipboard
colorscheme nord
{% endhighlight %}

~/.config/nvim/snippets<br>

{% highlight shell %}
~/.config/nvim/snippets/
markdown.snippets python.snippets sh.snippets
{% endhighlight %}

## Zsh/tmux:

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

#Plugins list #https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins

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
