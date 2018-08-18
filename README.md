# · 

There's many like this but this is mine.

## Setting up dotfiles on a new machine

1. Install [Brew][1] package manager

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2. Install `git`

```
brew install git
```

3. Add the following `alias` in your `.bashrc`.

```
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

4. Add `.cfg` in your global `.gitignore` to avoid recursion issue when cloning this repository.

```
echo ".cfg" >> ~/.gitignore
```

5. Clone this repository

```
git clone --bare git@github.com:faizmokhtar/dotfiles.git $HOME/.cfg
```

6. Define `alias` for current scope

```
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

7. Checkout the content from repository to your `$HOME`. If there's any issue, simply checkout the working files.

```
Checkout the actual content from the bare repository to your $HOME:
```

8. Set `showUntrackedFiles` to `no`

```
config config --local status.showUntrackedFiles no
```

9. Now, you can use `config` like how you normally use `git`. Eg;

```
config status
config add .vimrc
config commit -m "Add vimrc"
config add .bashrc
config commit -m "Add bashrc"
config push
```

## Set `zsh` as the default shell

Make sure you already installed `zsh`. Then, run the following;

```
sudo sh -c "echo $(which zsh) >> /etc/shells"
chsh -s $(which zsh)
```

### References

If something fucks up, simply refer to the original article
by [Nicola Paolucci][2] to debug it yourself.

[1]:https://brew.sh/
[2]:https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/