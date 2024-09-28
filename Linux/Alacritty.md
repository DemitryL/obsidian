### 1. Update Ubuntu 22.04
```bash
sudo apt update && sudo apt upgrade
```

### 2. Install Alacritty Terminal on Ubuntu 22.04
```bash
sudo apt install wget apt-transport-https gnupg2 software-properties-common

sudo add-apt-repository ppa:aslatter/ppa

sudo apt update
sudo apt install alacritty
```

### 3. Start Compiling process
```bash
cd .config/alacritty/alacritty.toml
```

```alacritty.toml
[cursor]
unfocused_hollow = true

[cursor.style]
blinking = "Never"

[font]
size = 15

[window]
decorations = "full"
opacity = 0.80

[window.padding]
x = 5
y = 5

#######################################
## START OF COLOR SCHEMES ##
#######################################
```
Yml - > [Link](https://gist.github.com/adibhanna/5657ec0301f462a4577cffe11afd80e4)

