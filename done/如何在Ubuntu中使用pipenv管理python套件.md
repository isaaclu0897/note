#how-to , #ubuntu , #python , #pip, #pipenv

## 1.安裝pipenv

### 安裝pip

```bash
sudo apt update    # 更新系統套件
sudo apt install python3-pip    # 透過apt安裝系統系統用的pip3
```

### pip安裝pipenv
```bash
pip3 install pipenv    # 透過pip3安裝pipenv及相依套件
```
經過研究發現，安裝pipenv順便幫你在`~/.local`建立本地環境，這樣就安心多了。
1. 在`~/.local`中，建立pip3
2. 軟鏈接`pip3 > pip`，這樣我們可以直接使用`pip`
3. 安裝`pipenv`以及相依套件。可以使用`pip list --user`查看

### 備註
#### 可移除python3-pip
因爲已經在`~/.local`中安裝`pip`，系統的就可以移除掉了
```bash
sudo apt remove python3-pip
```

#### 如何讓`pip`在`bash`中補齊命令
發現`pip`不能補齊命令，查了一下，可以使用下面的命令讓他補齊
```bash
pipenv --completion >> ~/.bashrc && . ~/.bashrc
```

#### 如何讓`pipenv`在`bash`中補齊命令

```bash
pipenv --completion >> ~/.bashrc && . ~/.bashrc
```

## 2.如何使用pipenv

### 建立與刪除環境

```bash
# 創建
pipenv --three    # 產生 Python 3 虛擬環境
pipenv --two    # 產生 Python 2 虛擬環境
pipenv --python 3.6 # 產生 Python 3.6 虛擬環境

# 列出虛擬環境的所在位置
pipenv --where

# 刪除
pipenv --rm    # 刪除最近的環境
```



### 套件安裝及卸載

在虛擬環境中安裝套件。若在安裝後加上 --dev 參數則會安裝開發階段的套件，不會影響到穩定版。
```bash
pipenv install requests
pipenv install pytest --dev  // development 環境

pipenv uninstall requests
pipenv uninstall pytest --dev  // development 環境

```

#### 使用requirements安裝套件

使用pipenv的話：
```
pipenv install    # 安裝Pipfile內所有套件
pipenv install -r path/to/requirements.txt # 從requirements.txt安裝套件至虛擬環境中
```

使用pip的話：
```
pip install -r requirements.txt  # 安装requirement.txt中记录的依赖
```

導出 requirements.txt 給別人用
```
pipenv lock --requirements > requirements.txt
```

```
$ pipenv lock -r 
#從 Pipfile 和 Pipfile.lock 文件<br>
並產生 requirements.txt
```

### 運行環境

根據 virtualenv 執行相關 python 指令 （不進入虛擬環境中）
```bash
pipenv run python test.py
```

進入虛擬環境中，類似於 “source venv/bin/activate”
```bash
pipenv shell // 進入
exit         // 退出，也可以使用'Ctrl+D'
```



### 列出套件相依圖
```
pipenv graph
```

### 備註
```
pipenv --where    # 顯示虛擬環境根目錄資訊
pipenv --venv    # 顯示虛擬環境執行檔所在目錄
pipenv --py    # 顯示目前使用的python執行檔資訊(同which python)
pipenv --envs    # 輸出相關環境變數
pipenv --version    # 顯示版本
```

## 3.pipfile簡介
初始化虛擬環境後，會產生 Pipfile 跟 Pipfile.lock

* Pipfile 是一個 toml 格式的檔案
    * source: 指定要去找套件的 PyPI ，比較常見的使用案例是加上自己私有的 PyPI
    * dev-package: 開發環境所需套件
    * packages: 預設安裝套件（通常是 Production 用）
    * requires: 限定在某個版本的 Python

```javascript
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]

[packages]

[requires]
python_version = "3.6"
```

* Pipfile.lock 則是 JSON 格式的檔案
    * 同樣是記錄安裝的套件，但會同時記錄下套件相依的其他套件（假設安裝了 requests 套件，而 `requests` 相依於 `urllib3` ，則 `requests` 跟 `urllibs` 都會列在這）
```javascript
{
    "_meta": {
        "hash": {
            "sha256": "..."
        },
        "pipfile-spec": 6,
        "requires": {
            "python_version": "3.7"
        },
        "sources": [
            {
                "name": "pypi",
                "url": "https://pypi.org/simple",
                "verify_ssl": true
            }
        ]
    },
    "default": {},
    "develop": {}
}
```

通常沒有什麼特別的理由，可以不用動到 `Pipfile` 跟 `Pipfile.lock`
交給 `pipenv` 去管理就好


### pipenv 缺點

#### Lock时间长

第一次使用安裝jupyterthemes的時候也發生這個問題，也是因爲該套件含有科學包

> 1. Lock时间长
用户经常抱怨pipenv lock的时间长，特别是涉及到一些科学计算的库时，如numpy, sklearn, tensorflow，会慢得让你怀疑人生。pipenv lock其实做的就是依赖解析，而慢的原因是，Pipenv需要下载所有的安装包来计算它们的哈希值，要命的是，像numpy这种库，一个版本就有17个包，每个包的大小是10M~20M不等，总共下载的大小就有300多M左右。也有人提PR希望修改这个逻辑，但后来都不了了之。[文章鏈接](https://zhuanlan.zhihu.com/p/80695813)

