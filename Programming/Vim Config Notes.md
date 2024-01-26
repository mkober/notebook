#+title: Vim

* Neovim
** .config/nvim
*** after
*** lua
*** pack
*** plugin
*** init.lua

* Current Neovim config
vim.g.mapleader = ' '
vim.opt.nu = true
vim.opt.relativenumber = true
vim.opt.tabstop = 4
vim.opt.softtabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true
vim.opt.smartindent = true
vim.opt.wrap = false
vim.opt.swapfile = false
vim.opt.backup = false
vim.opt.undodir = os.getenv("HOME") .. "/.vim/undodir"
vim.opt.undofile = true
vim.opt.hlsearch = false
vim.opt.incsearch = true
vim.opt.scrolloff = 8
vim.opt.isfname:append("@-@")
vim.opt.updatetime = 50
vim.opt.cursorline = true

* Old .vimrc config
syntax on
filetype plugin indent on

set nocompatible
set t_Co=256
set number
set nowrap
set linebreak
set ruler
set showmatch
set mat=5
set backspace=indent,eol,start
set wildignore+=*.o,*.obj,.git,*.rbc,*.class,.svn,vendor/gems/*
set matchpairs+=<:>
set hlsearch
set incsearch
set ignorecase
set smartcase
set smartindent
set autoindent
set foldmethod=indent
set foldopen=block,hor,mark,percent,quickfix,tag
set foldlevel=99
set sidescrolloff=2
set numberwidth=2
set softtabstop=4
set shiftwidth=2
set tabstop=2
set list lcs=tab:\|\
set expandtab
set mouse=a
set ttyfast
set smarttab
set magic
set history=1000
set lazyredraw
set clipboard=unnamed
set pastetoggle=<F2>
set shiftround
set lazyredraw
set complete-=i
set cursorline
set noerrorbells
set visualbell
set title
set background=dark
set nospell
set wildmenu
set omnifunc=syntaxcomplete#Complete
set completeopt=longest,menuone