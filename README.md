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
yay oh-my-posh bun-bin golang chezmoi nvim zip unzip
```
### install [sdkman](https://sdkman.io/)
```
curl -s "https://get.sdkman.io" | bash
```
### config [chezmoi](https://www.chezmoi.io/)
```
chezmoi init https://github.com/mendirl/dotfiles.git
```
### 
