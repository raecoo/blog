---
layout: post
title: VIM配置文件
---

备份一下VIM配置文件<!--more--><pre><code>set nocompatible
set bsdir=buffer
set autochdir
set autoread
set enc=utf-8
set fenc=utf-8
set fencs=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
set langmenu=en_US.UTF-8
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
colorscheme vibrantink
syntax on
set cmdheight=1
set nobackup
set nowritebackup
set showmatch
set nu!
set hlsearch
set ambiwidth=double
set guioptions-=T
" set guioptions-=m
"正确地处理中文字符的折行和拼接
set formatoptions+=mM
"设置状态行，使其能额外显示文件的编码信息
set statusline=%&lt;%f\ %h%m%r%=%k[%{(&amp;fenc==\"\")?&amp;enc:&amp;fenc}%{(&amp;bomb?\",BOM\":\"\")}]\ %-14.(%l,%c%V%)\ %P
" 增强检索功能
set tags=./tags,./../tags,./**/tags
" 保存文件格式
set fileformats=unix,dos
"自动回到最后编辑的位置
autocmd BufReadPost * if line("'\"") &amp;&amp; line("'\"") &lt;= line("$") | exe "normal `\"" | endif
"""""""""""""""""""""""""""""
" Text Formatting/Layout
"""""""""""""""""""""""""""""
set fo=tcrqn " See Help (complex)
set autoindent
set smartindent
set cindent
set tabstop=2
set softtabstop=2
set shiftwidth=2
set smarttab
set lbr " 防止单词断行
set guioptions+=b " 水平滚动条
set tw=100
filetype plugin indent on
" Load matchit (% to bounce from do to end, etc.)
"runtime! macros/matchit.vim
augroup myfiletypes
" Clear old autocmds in group
autocmd!
" autoindent with two spaces, always expand tabs
autocmd FileType ruby,rhtml,html,erb,eruby,yaml set ai sw=2 sts=2 et
augroup END
"""""""""""""""""""""""""""""
"多语言文字设置
"""""""""""""""""""""""""""""
" multi-encoding setting
if has("multi_byte")
set bomb
set fileencodings=ucs-bom,utf-8,cp936,big5,euc-jp,euc-kr,latin1
" CJK environment detection and corresponding setting
if v:lang =~ "^zh_CN"
" Use cp936 to support GBK, euc-cn == gb2312
set encoding=cp936
set termencoding=cp936
set fileencoding=cp936
elseif v:lang =~ "^zh_TW"
" cp950, big5 or euc-tw
" Are they equal to each other?
set encoding=big5
set termencoding=big5
set fileencoding=big5
elseif v:lang =~ "^ko"
" Copied from someone's dotfile, untested
set encoding=euc-kr
set termencoding=euc-kr
set fileencoding=euc-kr
elseif v:lang =~ "^ja_JP"
" Copied from someone's dotfile, untested
set encoding=euc-jp
set termencoding=euc-jp
set fileencoding=euc-jp
endif
" Detect UTF-8 locale, and replace CJK setting if needed
if v:lang =~ "utf8$" || v:lang =~ "UTF-8$"
set encoding=utf-8
set termencoding=utf-8
set fileencoding=utf-8
endif
else
echoer
""""""""""""""""""""""""""
" Plugins map
""""""""""""""""""""""""""
" NERDTree config
nmap ee :NERDTree&lt;CR&gt;
"for FuzzyFinderFile plugin
nnoremap &lt;C-p&gt; :FuzzyFinderFile &lt;C-r&gt;=fnamemodify(getcwd(), ':p')&lt;CR&gt;&lt;CR&gt;
nnoremap &lt;C-t&gt; :FuzzyFinderFile &lt;C-r&gt;=expand('%:~:.')[:-1-len(expand('%:~:.:t'))]&lt;CR&gt;&lt;CR&gt;
" miniBufExpl config
let g:miniBufExplSplitBelow=0
let g:miniBufExplMapWindowNavVim = 1
let g:miniBufExplMapWindowNavArrows = 1
let g:miniBufExplMapCTabSwitchBufs = 1
let g:miniBufExplModSelTarget = 1
let g:miniBufExplUseSingleClick = 1</code></pre>
