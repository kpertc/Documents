```shell
# open homepage of Homebew
brew home
```

```shell
brew install packagename
brew uninstall packagename

# Casks → Mac OS apps
brew install --cask firefox
brew uninstall --cask firefox
brew list --cask

# to homepage of pycharm
brew home pycharm

# show info about the package
brew info packagename

# list installed packages
brew list

brew outdated

# refresh the formula index
brew update

# install newer versions
brew upgrade

# remove old version
brew cleanup

# diagnos tool
brew doctor

# add repo
brew tap packagepath
```

install to `/opt/homebrew/Cellar/` (Apple Silicon) / `/usr/local/Cellar/` (Intel) — `brew --prefix` prints the live answer

```shell
# search formulae by regex
brew search /wge*/
# search + regex
```

Formulae → command line app



> Install GNU version software to overwrite Mac BSD version
[[GNU]]