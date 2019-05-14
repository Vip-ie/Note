# VIM

### Homebrew常用命令

```
brew list                 # 查看已经安装的包
brew update               # 更新Homebrew自身
brew doctor               # 诊断关于Homebrew的问题(Homebrew 有问题时请用它)
brew cleanup              # 清理老版本软件包或者无用的文件
brew show ${formula}      # 查看包信息
brew search ${formula}    # 按名称搜索
brew upgrade ${formula}   # 升级软件包
brew install ${formula}   # 按名称安装
brew uninstall ${formula} # 按名称卸载
brew pin/unpin ${formula} # 锁定或者解锁软件包版本，防止误升级
```

### zsh，好用的shell

Shell程序就是Linux/UNIX系统中的一层外壳，几乎所有的应用程序都可以运行在Shell环境 下，常用的有bash, csh, zcsh等。在

`/etc/shells`文件中可以查看系统中的各种shell。

```
cat /etc/shells

# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

而zsh是OSX系统原生的shell之一，其功能强大，语法相对于bash更加友好和强大，所以推荐 使用zsh作为默认的shell

```
# 切换zsh为默认shell
chsh -s $(which zsh)
```

如果你想使用最新的zsh，你可以使用Homebrew，此方法也会保留原生的zsh，防止你在某个 时刻需要它。

```
# 查看最新zsh信息
brew info zsh

# 安装zsh
brew install --disable-etcdir zsh

# 添加shell路径至/etc/shells文件中
# 将 /usr/local/bin/zsh 添加到下面文件中
sudo vim /etc/shells

# 更换默认shell
chsh -s /usr/local/bin/zsh
```

下面贴上我的zsh配置以供参考

```
# modify the prompt to contain git branch name if applicable
git_prompt_info() {
  ref=$(git symbolic-ref HEAD 2> /dev/null)
  if [[ -n $ref ]]; then
    echo " %{$fg_bold[green]%}${ref#refs/heads/}%{$reset_color%}"
  fi
}
setopt promptsubst
export PS1='${SSH_CONNECTION+"%{$fg_bold[green]%}%n@%m:"}%{$fg_bold[blue]%}%c%{$reset_color%}$(git_prompt_info) %# '

# load our own completion functions
fpath=(~/.zsh/completion $fpath)

# completion
autoload -U compinit
compinit

# load custom executable functions
for function in ~/.zsh/functions/*; do
  source $function
done

# makes color constants available
autoload -U colors
colors

# enable colored output from ls, etc
export CLICOLOR=1

# history settings
setopt hist_ignore_all_dups inc_append_history
HISTFILE=~/.zhistory
HISTSIZE=4096
SAVEHIST=4096

# awesome cd movements from zshkit
setopt autocd autopushd pushdminus pushdsilent pushdtohome cdablevars
DIRSTACKSIZE=5

# Enable extended globbing
setopt extendedglob

# Allow [ or ] whereever you want
unsetopt nomatch

# vi mode
bindkey -v
bindkey "^F" vi-cmd-mode
bindkey jj vi-cmd-mode

# handy keybindings
bindkey "^A" beginning-of-line
bindkey "^E" end-of-line
bindkey "^R" history-incremental-search-backward
bindkey "^P" history-search-backward
bindkey "^Y" accept-and-hold
bindkey "^N" insert-last-word
bindkey -s "^T" "^[Isudo ^[A" # "t" for "toughguy"

# use vim as the visual editor
export VISUAL=vim
export EDITOR=$VISUAL

# load rbenv if available
if which rbenv &>/dev/null ; then
  eval "$(rbenv init - --no-rehash)"
fi

# load thoughtbot/dotfiles scripts
export PATH="$HOME/.bin:$PATH"

# mkdir .git/safe in the root of repositories you trust
export PATH=".git/safe/../../bin:$PATH"

# aliases
[[ -f ~/.aliases ]] && source ~/.aliases

# Local config
[[ -f ~/.zshrc.local ]] && source ~/.zshrc.local
```



