# My Mac Setup

This is a list of applications and tools I use on my mac machine.

## Homebrew

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

## iTerm2

    brew cask install iterm2

Here you can find color [themes](https://iterm2colorschemes.com/)

### Enable natural text selection

To use Option + → or ← to jump words you have to enable it:
(iTerm → Preferences → Profiles → Keys → Load Preset... → Natural Text Editing)

## ZSH

    brew install zsh
    brew install zsh-completions

### Zsh-Syntax-Highlighting

    brew install zsh-syntax-highlighting

Then add to the `~/.zshrc` file

    source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

## Oh My Zsh

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

More info [here](https://github.com/robbyrussell/oh-my-zsh)

## Powerlevel9k / Powerlevel10k

    git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k

Then edit your `~/.zshrc` and set `ZSH_THEME="powerlevel10k/powerlevel10k"` and `POWERLEVEL9K_MODE="awesome-patched"`

More info [here](https://github.com/Powerlevel9k/powerlevel9k)

### Install patched fonts

[Here you can find powerline fonts](https://github.com/powerline/fonts)

Click on the downloaded font and install it.
Set the font in the terminal, e.g. for iTerm2 (iTerm → Preferences → Profiles → Text → Change Font)

## Fortune

    brew install fortune

Then I can add it to `~/.zshrc` file to show a fortune-cookie text on a new shell sessioin, e.g.

```
echo "
|| DATE: $(date)
||
|| $(fortune)
"
```

I have to then add this to my `~/.zshrc` file to supress warning from Powerlevel when echoing something:

    typeset -g POWERLEVEL9K_INSTANT_PROMPT=quiet

## Fira Code Font

    brew tap homebrew/cask-fonts
    brew cask install font-fira-code

## My ~/.zshrc file

```zsh
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="/Users/bartoszbialecki/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="powerlevel10k/powerlevel10k"

# Which plugins would you like to load?
# Standard plugins can be found in ~/.oh-my-zsh/plugins/*
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
    git
    dotenv
    osx
    docker
    gitignore
    virtualenv
    sudo
)

source $ZSH/oh-my-zsh.sh

# User configuration

alias zshconfig="code -n ~/.zshrc"
alias updatezsh="source ~/.zshrc"
alias diskusage="du -h -d1"

# Preferred editor for local and remote sessions
if [[ -n $SSH_CONNECTION ]]; then
   export EDITOR='vim'
else
   export EDITOR='code -w'
fi

# to hide user@hostname info
prompt_context(){}

DEFAULT_USER=$(whoami)

POWERLEVEL9K_MODE="awesome-patched"

echo "
|| DATE: $(date)
||
|| $(fortune)
"

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

typeset -g POWERLEVEL9K_INSTANT_PROMPT=quiet

source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi

eval "$(pyenv virtualenv-init -)"

export JAVA_HOME="`/usr/libexec/java_home`"

# Configuration for virtualenv
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
source /usr/local/bin/virtualenvwrapper.sh
```

## Visual Studio Code

    brew cask install visual-studio-code

### Settings

```json
{
  "workbench.startupEditor": "newUntitledFile",
  "terminal.integrated.fontFamily": "MesloLGS NF",
  "terminal.external.osxExec": "iTerm.app",
  "terminal.integrated.shell.osx": "zsh",
  "terminal.integrated.fontSize": 14,
  "editor.formatOnSave": true,
  "editor.rulers": [80, 120],
  "editor.cursorStyle": "block",
  "editor.fontSize": 14,
  "editor.renderIndentGuides": true,
  "files.trimFinalNewlines": true
}
```

### Plugins

- Prettier
- YAML
- Python
- GitLens
- Docker
- Bracket Pair Colorizer
- Markdown All in One
- Material Icon Theme
- Gi
- shell-format
- Vscode Google Translate
- Debugger for Chrome
- ESLint
- Path Intellisense
- Auto Rename Tag
- Auto Close Tag
- ES7 React/Redux/GraphQL/React-Native snippets
- npm Intellisense
- Dash
- Draw.io Integration

## Vim

My `~/.vimrc` file

```vim
" Comments in Vimscript start with a `"`.

" If you open this file in Vim, it'll be syntax highlighted for you.

" Vim is based on Vi. Setting `nocompatible` switches from the default
" Vi-compatibility mode and enables useful Vim functionality. This
" configuration option turns out not to be necessary for the file named
" '~/.vimrc', because Vim automatically enters nocompatible mode if that file
" is present. But we're including it here just in case this config file is
" loaded some other way (e.g. saved as `foo`, and then Vim started with
" `vim -u foo`).
set nocompatible

" Turn on syntax highlighting.
syntax on

" Disable the default Vim startup message.
set shortmess+=I

" Show line numbers.
set number

" This enables relative line numbering mode. With both number and
" relativenumber enabled, the current line shows the true line number, while
" all other lines (above and below) are numbered relative to the current line.
" This is useful because you can tell, at a glance, what count is needed to
" jump up or down to a particular line, by {count}k to go up or {count}j to go
" down.
set relativenumber

" Always show the status line at the bottom, even if you only have one window open.
set laststatus=2

" The backspace key has slightly unintuitive behavior by default. For example,
" by default, you can't backspace before the insertion point set with 'i'.
" This configuration makes backspace behave more reasonably, in that you can
" backspace over anything.
set backspace=indent,eol,start

" By default, Vim doesn't let you hide a buffer (i.e. have a buffer that isn't
" shown in any window) that has unsaved changes. This is to prevent you from "
" forgetting about unsaved changes and then quitting e.g. via `:qa!`. We find
" hidden buffers helpful enough to disable this protection. See `:help hidden`
" for more information on this.
set hidden

" This setting makes search case-insensitive when all characters in the string
" being searched are lowercase. However, the search becomes case-sensitive if
" it contains any capital letters. This makes searching more convenient.
set ignorecase
set smartcase

" Enable searching as you type, rather than waiting till you press enter.
set incsearch

" Unbind some useless/annoying default key bindings.
nmap Q <Nop> " 'Q' in normal mode enters Ex mode. You almost never want this.

" Disable audible bell because it's annoying.
set noerrorbells visualbell t_vb=

" Enable mouse support. You should avoid relying on this too much, but it can
" sometimes be convenient.
set mouse+=a

" Try to prevent bad habits like using the arrow keys for movement. This is
" not the only possible bad habit. For example, holding down the h/j/k/l keys
" for movement, rather than using more efficient movement commands, is also a
" bad habit. The former is enforceable through a .vimrc, while we don't know
" how to prevent the latter.
" Do this in normal mode...
nnoremap <Left>  :echoe "Use h"<CR>
nnoremap <Right> :echoe "Use l"<CR>
nnoremap <Up>    :echoe "Use k"<CR>
nnoremap <Down>  :echoe "Use j"<CR>
" ...and in insert mode
inoremap <Left>  <ESC>:echoe "Use h"<CR>
inoremap <Right> <ESC>:echoe "Use l"<CR>
inoremap <Up>    <ESC>:echoe "Use k"<CR>
inoremap <Down>  <ESC>:echoe "Use j"<CR>
```

## Node.js

    brew install node

## Carthage

    brew install carthage

## Cocoapods

    sudo gem install cocoapods

## Git

    brew install git

### Gitignore

Use this global `~/.gitignore` file for all projects

```
# Folder view configuration files
.DS_Store
Desktop.ini

# Thumbnail cache files
._*
Thumbs.db

# Files that might appear on external disks
.Spotlight-V100
.Trashes

# Application specific files
venv
node_modules
.sass-cache
```

Then run this command to git use this file

    git config --global core.excludesfile ~/.gitignore

### Change pager settings

    git config --global --replace-all core.pager "less -F -X"

### Git Workflow

    brew install git-flow

## Java

    brew cask install java

Add to `~/.zshrc` file

    export JAVA_HOME="`/usr/libexec/java_home`"

## Xcode

You can install it from [App Store](https://apps.apple.com/pl/app/xcode/id497799835?l=pl&mt=12)

Command Line Developer Tools for Xcode

    xcode-select --install

[Cleaner for Xcode](https://apps.apple.com/pl/app/cleaner-for-xcode/id1296084683?l=pl&mt=12)

## Android Studio

    brew cask install android-studio

## IntelliJ IDEA Community Edition

    brew cask install intellij-idea-ce

## Atom

    brew cask install atom

## Alfred 4

    brew cask install alfred

## Docker

    brew cask install docker

## Ngrok

    brew cask install ngrok

## Travis CI

    sudo gem install travis --no-document

## Yarn

    brew install yarn

## Heroku CLI

    brew tap heroku/brew && brew install heroku

## Other Apps & Tools

- 4k Video Downloader

  `brew cask install 4k-video-downloader`

- [Advanced Network Care](https://www.macbooster.net/anc.php)

- [Affinity Photo](https://apps.apple.com/pl/app/affinity-photo/id824183456?l=pl&mt=12)

- [Amphetamine](https://apps.apple.com/pl/app/amphetamine/id937984704?l=pl&mt=12)

- Android File Transfer

  `brew cask install android-file-transfer`

- [Be Focused](https://apps.apple.com/pl/app/be-focused-focus-timer/id973134470?l=pl&mt=12)

- Brave Browser

  `brew cask install brave-browser`

- Carbon Copy Cloner

  `brew cask install carbon-copy-cloner`

- Charles

  `brew cask install charles`

- CheatSheet

  `brew cask install cheatsheet`

- chkrootkit

  `brew install chkrootkit`

* CleanMyMac X

  `brew cask install cleanmymac`

* [ColorSlurp](https://apps.apple.com/pl/app/colorslurp/id1287239339?l=pl&mt=12)

- Dash

  `brew cask install dash`

- Deadbolt

  `brew cask install deadbolt`

* DeepL

  `brew cask install deepl`

* Dropbox

  `brew cask install dropbox`

- [EarMaster7](https://www.earmaster.com/downloads/free-versions.html)

* [Elmedia Video Player](https://apps.apple.com/pl/app/elmedia-video-player/id1044549675?l=pl&mt=12)

* Firefox

  `brew cask install firefox`

* [Focus To-Do](https://apps.apple.com/pl/app/focus-to-do-pomodoro-tasks/id1258530160?l=pl&mt=12)

- FortiClient VPN

  `brew cask install forticlient`

- [Free Ruler](https://apps.apple.com/pl/app/free-ruler/id1483172210?l=pl&mt=12)

- Google Chrome

  `brew cask install google-chrome`

- Grammarly

  `brew cask install grammarly`

- [Hammerspoon](https://www.hammerspoon.org/)

- Handbrake

  `brew cask install handbrake`

- [HEIC Converter](https://apps.apple.com/pl/app/heic-converter/id1294126402?l=pl&mt=12)

- [Hungrymark](https://apps.apple.com/pl/app/hungrymark/id1482778901?l=pl&mt=12)

- [Icon Set Creator](https://apps.apple.com/pl/app/icon-set-creator/id939343785?l=pl&mt=12)

- [IconKit](https://apps.apple.com/pl/app/iconkit/id507135296?l=pl&mt=12)

- ImageAlpha

  `brew cask install imagealpha`

- ImageOptim

  `brew cask install imageoptim`

- iMazing

  `brew cask install imazing`

- Insomnia

  `brew cask install insomnia`

- [iPaste](https://apps.apple.com/app/id1056935452?mt=12)

- iSimulator

  `brew cask install isimulator`

- jq

  `brew install jq`

- [Jump Desktop](https://apps.apple.com/pl/app/jump-desktop-rdp-vnc-fluid/id524141863?l=pl&mt=12)

- [Loca Studio](https://apps.apple.com/app/id1465684707)

- Lynis

  `brew install lynis`

- [Magnet](https://apps.apple.com/pl/app/magnet/id441258766?l=pl&mt=12)

- [Monosnap](macappstores://itunes.apple.com/ru/app/monosnap/id540348655)

- NetSpot

  `brew cask install netspot`

- [Noizio](https://apps.apple.com/pl/app/noizio-focus-relax-sleep/id928871589?l=pl&mt=12)

- [Nucleo](https://nucleoapp.com/)

- Numi

  `brew cask install numi`

- OpenSim

  `brew cask install opensim`

- [Ora](https://apps.apple.com/pl/app/ora-simple-task-management/id1340501510?l=pl&mt=12)

- OverSight

  `brew cask install oversight`

- [Paste JSON as Code - quicktype](https://apps.apple.com/pl/app/paste-json-as-code-quicktype/id1330801220?l=pl&mt=12)

- [Patterns](https://apps.apple.com/us/app/patterns-the-regex-app/id429449079?mt=12)

- [Phiewer - Image Viewer](https://apps.apple.com/pl/app/phiewer-image-viewer/id1226444549?l=pl&mt=12)

- Postman

  `brew cask install postman`

- Pusher

  `brew cask install pusher`

- [Realm Browser](https://apps.apple.com/pl/app/realm-browser/id1007457278?l=pl&mt=12)

- [Reeder 4](https://apps.apple.com/pl/app/reeder-4/id1449412482?l=pl&mt=12)

- Reflector 3

  `brew cask install reflector`

- [Relax Melodies](https://apps.apple.com/pl/app/relax-melodies-sleep-sounds/id467103113?l=pl&mt=12)

- rkhunter

  `brew install rkhunter`

- [Screen-O-Matic](https://screencast-o-matic.com/screen-recorder)

- SimPholders

  `brew cask install simpholders`

- Skitch

  `brew cask install skitch`

- [Smart JSON Editor](https://apps.apple.com/pl/app/smart-json-editor/id1268962404?l=pl&mt=12)

- [SnippetsLab](https://apps.apple.com/pl/app/snippetslab/id1006087419?l=pl&mt=12)

- [SoundSource](https://www.rogueamoeba.com/soundsource/)

- Sourcetree

  `brew cask install soutcetree`

* Spotify

  `brew cask install spotify`

* Station

  `brew cask install station`

- Sqlectron

  `brew cask install sqlectron`

- SQLiteStudio

  `brew cask install sqlitestudio`

- TablePlus

  `brew cask install tableplus`

- The Unarchiver

  `brew cask install the-unarchiver`

* [Timork](https://apps.apple.com/pl/app/timork-focus-timer/id1195964402?l=pl&mt=12)

- tldr

  `brew install tldr`

* [To MP3 Converter](https://apps.apple.com/pl/app/to-mp3-converter-free/id983472324?l=pl&mt=12)

- Vysor

  `brew cask install vysor`

- Wireshark

  `brew cask install wireshark`

- [Woodpecker](https://apps.apple.com/cn/app/woodpecker/id1333548463?mt=12)

- [yEd Graph Editor](https://www.yworks.com/products/yed)
