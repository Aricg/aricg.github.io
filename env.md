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
