# Powerline インストール #

## Ubuntu ##

``` shell
sudo apt-get install powerline
```

## Mac ##

``` shell
pip install psutil
pip install powerline-shell
```
- (You can use the --user option to install for just your user, if you'd like. But you may need to fiddle with your PATH to get this working properly.)

-------------------------------------------------------------------------------

# Powerline fonts #

## Ubuntu ##

``` shell
sudo apt-get install fonts-powerline
```

## Other environments ##

``` shell
git clone https://github.com/powerline/fonts.git --depth=1
fonts/install.sh
rm -rf fonts
```

-------------------------------------------------------------------------------

# Setup shell prompt #

## Bash ##

### Add the following to your .bashrc file: ###

``` shell
function _update_ps1() {
    PS1=$(powerline-shell $?)
}

if [[ $TERM != linux && ! $PROMPT_COMMAND =~ _update_ps1 ]]; then
    PROMPT_COMMAND="_update_ps1; $PROMPT_COMMAND"
fi
```

## Zsh ##

### Add the following to your .zshrc: ###

``` shell
function powerline_precmd() {
    PS1="$(powerline-shell --shell zsh $?)"
}

function install_powerline_precmd() {
  for s in "${precmd_functions[@]}"; do
    if [ "$s" = "powerline_precmd" ]; then
      return
    fi
  done
  precmd_functions+=(powerline_precmd)
}

if [ "$TERM" != "linux" ]; then
    install_powerline_precmd
fi
```

## Fish ##

### Redefine fish_prompt in ~/.config/fish/config.fish: ###

``` fish
function fish_prompt
  powerline-shell --shell bare $status
end
```

## Tcsh ##

### Add the following to your .tcshrc: ###

``` tcsh
alias precmd 'set prompt="`powerline-shell --shell tcsh $?`"'
```
