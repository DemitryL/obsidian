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
cd .config/alacritty/alacritty.yml
```

```alacritty.yml
font:
	size: 14
window:
	padding:
		x: 0
		y: 0
	opacity: 0.92
	decorations: full
	dynamic_padding: true
	
cursor:
	unfocused_hollow: true
	style:
		blinking: Never
		
env:
	TERM: xterm-256color
	
scrolling:
	history: 2000
	auto_scroll: true

#######################################
## START OF COLOR SCHEMES ##
#######################################
```
Yml - > [Link](https://gist.github.com/adibhanna/5657ec0301f462a4577cffe11afd80e4)

