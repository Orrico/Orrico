# Linux Setup

## System - Ubuntu / Debian
sudo apt update
sudo apt upgrade
sudo apt install build-essential git sqlite3 curl wget unzip zstd vim btop ca-certificates openssh-server nginx

## Shell
### tmux
sudo apt install tmux libevent-dev ncurses-dev bison pkg-config
tar -zxf tmux-*.tar.gz
cd tmux-*/
./configure
make && sudo make install

### zsh
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
chsh -s $(which zsh) /* Edit: vim ~/.bashrc if [ -t 1 ]; then   exec zsh fi */
ZSH_THEME="fino-time"
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
grep "^alias " ~/.bashrc >> ~/.zshrc

## Redes
### UFW
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw status

### Nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo service --status-all

### SSH
sudo systemctl enable ssh
sudo systemctl start ssh
sudo service --status-all

### Tailscale
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
sudo systemctl enable tailscaled
sudo systemctl start tailscaled
sudo tailscale up --ssh

## Git
git config --global user.name "[USER.NAME]"
git config --global user.email "[USER.EMAIL]"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global push.default simple
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage "reset HEAD --"
git config --global alias.last 'log -1 HEAD'
git config --global alias.lg 'log --graph --pretty=format:'\''%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\'' --abbrev-commit'
ssh-keygen -t ed25519 -C "[USER.EMAIL]"
cat ~/.ssh/id_ed25519.pub

## Python
sudo apt install python3 python3-pip python3-venv
sudo apt install pipx
pipx ensurepath
pipx install uv

## Bun Runtime
curl -fsSL https://bun.sh/install | bash

## Node
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install nodejs

## nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
nvm install --lts
nvm use --lts
nvm alias default lts

## pnpm
curl -fsSL https://get.pnpm.io/install.sh | sh -

## Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install gcc
brew doctor

## Ollama
curl -fsSL https://ollama.com/install.sh | sh
sudo apt install nvidia-driver-55 ?

## OpenClaw
curl -fsSL https://openclaw.ai/install.sh | bash
import keys from ENV or file

## Claude Code
curl -fsSL https://claude.ai/install.sh | bash

## Docker
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo usermod -aG docker $USER
newgrp docker
