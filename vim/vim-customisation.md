# VIM: Customisation

## Resources
- [Vim: Tutorial on Customization and Configuration (2020)](https://youtu.be/JFr28K65-5E) 
- [Leeren - Vim Native Organization and Customization](https://bit.ly/2yD63Gb) 

## Initialization
**Execute Ex commands (usually from a vimrc file)** `:h vimrc`

First, initialize (if defined) the system vimrc (see `:version`):
```bash
$VIM/vimrc 
```

Then, initialize the first found of the following user vimrc configurations:
```bash
$VIMINIT                  (this is an environment variable)
$HOME/.vimrc                    
$HOME/.vim/vimrc
$EXINIT                   (this is an environment variable)
$HOME/.exrc 
$VIMRUNTIME/defaults.vim
```
### What if I don’t want to load anything?
```bash
$ vim -u NONE
$ vim -u NORC
```

## Plugin / Package Scripts
**Load plugin scripts** `:h load-plugins`

First, plugin scripts are loaded, which is equivalent to running:
```bash
:runtime! plugin/**/*.vim   (EXCEPT FOR rtp directories ending “after” - more on that later)
```

Usually, this is `$HOME/.vim/plugin/**/*.vim `

Then, packages are loaded...

Usually, this is `$HOME/.vim/pack/foo/start/bar/plugin/**/*.vim`
(`foo` and `bar` are completely arbitrary - put any string there and it would load as a package)

## runtimepath
**A List of directories which will be searched for runtime files.**

### Search Order
1. User Home `.vim`
2. Sysadmin folder
3. `$VIMRUNTIME`
4. Sysadmin `after` folder
5. User Home `after` folder

You’ll usually only add to 1 and 5, but will often examine 3 (system runtime).

For Unix: `runtimepath=$HOME/.vim,$VIM/vimfiles,$VIMRUNTIME,$VIM/vimfiles/after,$HOME/.vim/after`

### Structure
Each of the runtimepath directories (default 5) has this dir structure:
```bash
syntax/
compiler/
ftdetect/
filetype.vim
scripts.vim
autoload/
ftplugin/
plugin/
pack/
colors/
doc/
import/
keymap/
lang/
menu.vim
print/
spell/
tutor
indent/
```
