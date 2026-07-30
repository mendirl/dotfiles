### install archlinux in wsl (in powershell)
```
wsl --install archlinux
```
### connect with root and define password (in powershell)
```
wsl -u root -d archlinux
passwd
```
### configure sudo
```
pacman -Suy sudo
groupadd sudo
vim /etc/sudoers
(and uncomment the line related to group sudo/wheel)
```
### create a new user
```
useradd -m fabien
passwd fabien
usermod -aG sudo fabien
```
### install yay
```
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd .. && rm -rf yay/
```
### install applications
```
yay -S oh-my-posh-bin bun-bin golang chezmoi nvim zip unzip ssh ffmpeg ping inetutils -noconfirm
```
### install [sdkman](https://sdkman.io/)
```
curl -s "https://get.sdkman.io" | bash
```
### config [chezmoi](https://www.chezmoi.io/)
```
chezmoi init https://github.com/mendirl/dotfiles.git
```
##### modif de fichiers directement (ex.)
```
chezmoi re-add .bashrc
```
### config neovim
```
git clone https://github.com/LazyVim/starter --depth 1 ~/.config/nvim
rm -rf ~/.config/nvim/.git*
```
### config ssh
```
ssh-keygen -t ed25519 -C "fabien.couillard+dev@gmail.com"
ssh-copy-id -p 2222 fabien@192.168.1.90
```
### need to know
##### + contact windows from WSL2
use this : ```"$(hostname).local"``` (FIXE-WIN.local in my case)

#####  issue with chezmoi
https://github.com/microsoft/WSL/issues/10498

``` 
sudo mkdir /run/user/1000 && sudo chmod 700 /run/user/1000 && sudo chown $(whoami): /run/user/1000
```


## LLM

#### tester ollama (windows) depuis wsl

```bash
curl http://YOGAxWIN.local:11434/api/generate -d '{
  "model": "gemma4",
  "prompt": "Pourquoi le ciel est bleu ?",
  "stream": false
}'

curl http://localhost:11434/api/chat -d '{
  "model": "gemma4",
  "messages": [
    { "role": "user", "content": "Salut, ça va ?" }
  ],
  "stream": false
}'

curl http://YOGAxWIN.local:11434/api/chat -d '{
  "model": "gemma4",
  "messages": [
    { "role": "user", "content": "Salut, ça va ?" }
  ],
  "stream": false
}'
```

### utilisation de mcp toolbox de docker desktop
si le mcp fait référence à un serveur se trouvant dans docker, il faut utiliser l'url : `host.docker.internal`
