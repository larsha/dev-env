# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
  # Basics
  sudo locale-gen "en_US.UTF-8"
  sudo apt-get update
  sudo apt-get install apt-utils
  sudo apt-get install tig

  su ubuntu

  # Programming languages
  sudo curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
  sudo apt-get update
  sudo apt-get install -y nodejs
  sudo apt-get install -y build-essential
  sudo add-apt-repository ppa:longsleep/golang-backports
  sudo apt-get update
  sudo apt-get install golang-go

  # Vim
  mkdir -p /home/ubuntu/.vim/autoload /home/ubuntu/.vim/bundle && \
  curl -LSso /home/ubuntu/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
  git clone https://github.com/fatih/vim-go.git /home/ubuntu/.vim/bundle/vim-go
  git clone https://github.com/pangloss/vim-javascript.git /home/ubuntu/.vim/bundle/vim-javascript
  git clone https://github.com/kien/ctrlp.vim.git /home/ubuntu/.vim/bundle/ctrlp.vim
  git clone https://github.com/scrooloose/nerdtree.git /home/ubuntu/.vim/bundle/nerdtree
  git clone https://github.com/jdkanani/vim-material-theme /home/ubuntu/.vim/bundle/vim-material-theme
  git clone https://github.com/jistr/vim-nerdtree-tabs.git /home/ubuntu/.vim/bundle/vim-nerdtree-tabs
  git clone git://github.com/tpope/vim-sleuth.git /home/ubuntu/.vim/bundle/sleuth.vim

cat > /home/ubuntu/.vimrc << EOL
execute pathogen#infect()
syntax on
filetype plugin indent on
set runtimepath^=~/.vim/bundle/ctrlp.vim
set t_Co=256
set background=dark
colorscheme material-theme
let g:nerdtree_tabs_open_on_console_startup=1
set number
set clipboard=unnamed
EOL
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.hostname = "docker"
  config.vm.network "private_network", ip: "192.168.50.4"
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 12288
    v.cpus = 8
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.provision "shell", inline: $script
end
