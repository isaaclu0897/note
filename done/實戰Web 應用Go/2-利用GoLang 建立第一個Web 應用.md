#goLang, #web 

上篇簡單介紹了GoLang 的特性，並且建立了開發環境，已經可以開始編寫程式了。

但...要寫什麼呢？

爲了不要拖泥帶水，這次打算使用敏捷式學習法，快速達到目的，持續學習、更新、迭代。相信這樣的學習模式，可以幫助我在最短的時間內，充分瞭解一個語言。

所以硬一點！直接練習做出一個Web吧！

### 如何建立一個簡單的Web 應用

GoLang 提供了一個完善的Web 套件叫做net/http，透過這個套件可以很輕鬆的建立一個可執行的Web service。同時能簡單地對Web 路由、靜態檔案、模版、cookie 等資料進行設定和操作。

#### 代碼
```go=
package main

import ( // 套件引入可以直接用括號包起來，看起來很舒服
	"fmt"
	"log"
	"net/http"
	"strings"
)

func sayhelloName(w http.ResponseWriter, r *http.Request) { // 看起來func的需要傳入http讀寫器，http.Request用了*不知道是什麼意思
	// 解析參數，預設不會解析
	r.ParseForm() // Q：留個疑問，不解析會怎樣？

	//這些資訊是輸出到Server的
	fmt.Println(r.Form)
	fmt.Println("path", r.URL.Path)
	fmt.Println("scheme", r.URL.Scheme)
	fmt.Println(r.Form["url_long"])
	for k, v := range r.Form {
		fmt.Println("key:", k)
		fmt.Println("val:", strings.Join(v, ""))
	}

	fmt.Fprintf(w, "Hello ISAAC!") // 這個寫入到 w 的是輸出到客戶端的
}

func main() {
	http.HandleFunc("/", sayhelloName)     // 設定路由與處理func
	err := http.ListenAndServe(":9453", nil) // 設定監聽的port
	if err != nil {
		log.Fatal("ListenAndServe: ", err) // Q：這裏報錯不知道會記錄到哪裏去？
	}
}
```

#### 執行結果
![](../../../attachments/2-利用GoLang%20建立Web%20應用.png)

雖然有諸多不理解的地方，不過第一個Web service 就這樣完成了...

嘗試第一只程式，真的發現GoLang 的方便，像是`go run`、`go fmt`，雖不及動態語言方便，但和其他靜態語言一比，真是天差地遠。例如說寫C 的話就要自己安裝GCC 編譯環境什麼的，這些東西Go 官方都提供給你了。

語法看起來也很直觀，雖然沒寫過什麼靜態語言，但是基本上能理解代碼的意思。有些許不理解的部分，我想是原先對與Web 開發就不熟悉，這個就後面慢慢來瞭解了。

### 其他疑問

* Q：若不解析http request會怎樣？會變成字串所以無法使用嗎？留給以後的自己回答
* Q：log.Fatal就寫這樣，報錯不知道會記錄到哪裏去？
A：結果馬上就報錯:rolling_on_the_floor_laughing:。在執行代碼時，使用到被綁定的80 port，就發生error。看起來是直接輸出到terminal，不知道如果要記錄到日誌中該怎麼做呢？
```bash
2022/08/06 14:08:58 ListenAndServe: listen tcp :80: bind: permission denied exit status 1
```

> [Go 建立一個簡單的web 服務](https://willh.gitbook.io/build-web-application-with-golang-zhtw/03.0/03.2)


