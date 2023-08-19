#goLang, #vim, #vimrc, #vundle, #setUp

所謂《工欲善其事，必先利其器》，一切的開始必須先從工具開始，工具可以自己打造也可以使用現成的。因此在編寫`GoLang`前，需要先粗略的瞭解語言特性、如何建立開發環境、如何使用。

### 語言特性

1. open source
2. 強型別
3. 編譯速度
4. 原生支援併發
5. 強制規範的 code style

### 設定開發環境

依照經驗指示，安裝方法有三種，初次開發當然使用最簡單的標準安裝套件安裝啦～
1. 透過 source code 安裝
2. 使用標準安裝套件安裝
3. 透過第三方工具進行安裝（`apt`、`yum`、`dnf`etc.）

![|500](../../../attachments/1-建立GoLang開發環境.png)


### 使用標準安裝包安裝Go語言

1. 到[官網](https://go.dev/dl/)下載標準包
2. 解壓縮
3. 設定環境變數
4. 重新載入環境變數

![](../../../attachments/1-建立GoLang開發環境-1.png)

command line
``` bash=
wget https://go.dev/dl/go1.18.4.linux-amd64.tar.gz # 下載go語言安裝包
tar zxvf go1.18.4.linux-amd64.tar.gz -C /home/wei # 解壓縮到指定目錄
echo -e '\nexport PATH="/home/wei/go/bin:$PATH"\n' >> ~/.bashrc # 設定環境變數
. ~/.bashrc # reload 環境變數
```

> [Golang 介紹與環境設定](https://ithelp.ithome.com.tw/articles/10233594)
> [Go 安裝](https://willh.gitbook.io/build-web-application-with-golang-zhtw/01.0/01.1#linux-an-zhuang)

### 確認執行環境

```
go version
```

### go語言基本指令與使用

#### 指令

```bash
go run # 執行程式 臨時編譯並運行

go get # 下載遠端程式並安裝 類似於python的pip

go fmt # 格式化source code

go mod # 模組化管理

go test # 測試程式

go build # 編譯程式

go install # build + 移動到bin
```

#### hello world

第一支go 程式，hello world。
```go=
package main

import "fmt"

func main() {
	fmt.Println("vim-go")
}
```

在terminal執行它

```bash
$ go run main.go
vim-go
```



### 設定IDE

用`VIM`也有段時間了，有時候覺得學一個新的語言就要學一個新的IDE真的好麻煩！所以最終還是決定使用`VIM`，一套打天下！而且在工作上，常常會透過SSH連入Server去處理issue，根本沒有機會讓你使用GUI，所以呀～還是好好把最簡單的工具用到如火純青吧！

1. update VIM
2. Install Vundle
3. Intall plugin fatih/vim-go
4. Intall plugin ycm-core/YouCompleteMe

#### Update VIM

```bash
sudo add-apt-repository ppa:jonathonf/vim # 更新VIM套件庫
sudo apt install vim # 安裝VIM，VIM version 8.2
```

#### Install Vundle

1. clone Vundle from git
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim # 利用git將Vundle從github拉到.vim中
```

2. 在.vimrc中插入vundle設定
```vimrc
" ===== vundle started =====
" disable vi compatibility
set nocompatible

filetype off  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim

call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" Plugin 'fatih/vim-go', { 'do': ':GoInstallBinaries' }

" Plugin 'ycm-core/YouCompleteMe'



" All of your Plugins must be added before the following line
call vundle#end()            " required

" To ignore plugin indent changes, instead use:
"filetype plugin on
filetype plugin indent on    " required


" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
" turn the line numbers on

" ===== vundle end =====
```

3. source vimrc & intall plugin
```vimrc
:PlugInstall # 在vim中鍵入
```

#### Install plugin fatih/vim-go

1. insert Plugin 'fatih/vim-go' into vimrc
```vimrc
Plugin 'fatih/vim-go'
```

2. source vimrc & intall plugin
```vimrc
:PlugInstall # 在vim中鍵入
```

3. go intall binaries
```vimrc
:GoInstallBinaries
```

出现 vim-go: installing finished! 表示安装成功，可以使用 Go 包的相关功能了！
此時在vim中使用`<C-x> <C-o>`可以使用gopls的omnifunc補齊功能。另外在初次使用`vim main.go`時，編輯器會自動帶出go 語言hello world 的程式。


#### Intall plugin ycm-core/YouCompleteMe


1. insert Plugin 'fatih/vim-go' into vimrc
```vimrc
Plugin 'fatih/vim-go'
```

2. source vimrc & intall plugin
```vimrc
:PlugInstall # 在vim中鍵入
```

3. install 編譯用工具
```bash
sudo apt install build-essential cmake python3-dev
```

4. make
```bash
cd ~/.vim/plugged/YouCompleteMe
python3 install.py --go-completer
or
./install.py --go-completer
```

### reference

P.s.在編譯過程，有報一個錯誤，錯誤訊息如下。解決方法，下載更高版本的gcc替換，即可成功編譯。

```bash
YCM requires CMake 3.13 or greater. If your CMake is too old, you may be able to
simply `pip install --user cmake` to get a really new version.
```

解決方法如下：
https://stackoverflow.com/questions/65284572/your-c-compiler-does-not-fully-support-c17

