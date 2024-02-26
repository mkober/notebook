* POP OS
** Set Default audio on PopOS
https://wolfgang-ziegler.com/blog/prevent-changing-of-default-ubuntu-sound-device

* Install Node 16 on Ubuntu 20.04
** sudo apt install curl
** curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
** sudo apt install -y nodejs

* Install Yarn on Ubuntu 20.04
** curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
** echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
** sudo apt update
** sudo apt install yarn
** yarn set version berry // Update to version 2

* GIMP
** Adjust font size for HDPI screens
/usr/share/gimp/2.0/themes/
font_name = "sans 20"

* Setup Ubuntu WSL 2

** Install Pre-Reqs
*** sudo add-apt-repository --yes --update ppa:ansible/ansible
*** sudo apt install ansible gh nvm epiphany-browser gnome-tweaks gnome-extras gnome build-essential libgtk-3-dev libgnutls28-dev libtiff5-dev libgif-dev libjpeg-dev libpng-dev libxpm-dev libncurses-dev texinfo autoconf ninja-build gettext cmake unzip curl fd-find ripgrep python3-neovim
*** nvm install 16

** Dark Mode on WSl2 Ubuntu
*** https://www.gnome-look.org/p/1252100/
*** Copy Yaru-dark folder to /usr/share/themes/

** Emacs with GTK for WSL 2
*** git clone git://git.sv.gnu.org/emacs.git
*** cd emacs
*** ./autogen.sh
*** ./configure --with-pgtk
*** make -j8
*** sudo make install

** Doom Emacs
*** git clone --depth 1 https://github.com/doomemacs/doomemacs ~/.config/emacs
*** ~/.config/emacs/bin/doom install

** Neovim
*** git clone https://github.com/neovim/neovim
*** cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo
*** sudo make install
*** git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim

** Node and NVM
*** curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
*** source ~/.bashrc

** Docker
*** sudo install -m 0755 -d /etc/apt/keyrings
*** curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
*** sudo chmod a+r /etc/apt/keyrings/docker.gpg
*** echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
*** sudo apt update
*** sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

#### Permanently hide the Ubuntu Dock from your desktop
gsettings set org.gnome.shell.extensions.dash-to-dock autohide false
gsettings set org.gnome.shell.extensions.dash-to-dock dock-fixed false
gsettings set org.gnome.shell.extensions.dash-to-dock intellihide false

