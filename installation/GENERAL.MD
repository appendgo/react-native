# Installation / General

## [oh-my-zsh](https://ohmyz.sh/) install

* `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

## Homebrew install

* `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
* `(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/adam/.zprofile eval "$(/opt/homebrew/bin/brew shellenv)"`

## Watchman

* `brew install watchman`

## Git

* `brew install git`
* `git --version`
* `git config --global user.name "Emma Paris"`
* `git config --global user.email "eparis@atlassian.com"`
* [Github desktop](https://desktop.github.com) - recommended

## NVM

* `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh |bash`
* `nvm --version` **(in a new terminal window)**
* `nvm list`
* `nvm install 16.20.0`
* `nvm use 16.20.0`
* `node --version`

## NVM - SYMLINK

* `ln -s $(which node) /usr/local/bin/node`

## Yarn

* `npm install --global yarn`
* `yarn --version`

