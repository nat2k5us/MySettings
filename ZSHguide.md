# Beautify your terminal in 5 mins

## Step 1: install homebrew if you don't have it already
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Step 2: install iterm2
```
 brew install item2
```
## Step 3: install zsh
``` 
brew install zsh
```

## Step 4: install powerline 10k
```
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```
## Step 5: Install powerline font (optional)

```
open https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf
```

 ## Step 6: In Iterm2 run powerline configure
```
p10k configure
```
## Step 7 : Activate the new zsh terminal
```
exec zsh
```

# That is it - you have ZSH beautiful terminal

### bonus 
```
brew install neofetch
neofetch
```
