
https://www.reddit.com/r/MechanicalKeyboards/comments/aykjiy/how_to_get_working_arrow_keys_on_your_ducky_one_2/

https://www.reddit.com/r/DuckyKeyboard/comments/vz9rew/guide_how_to_set_fn_wasd_to_arrow_keys_ducky_one/

https://www.reddit.com/r/MechanicalKeyboards/comments/sfg81l/ducky_one_mini_3_why_did_they_remap_the_arrow_keys/

https://www.reddit.com/r/DuckyKeyboard/comments/123wym0/ducky_one_3_mini_functions_key_lock/

https://www.zhihu.com/question/519170777/answer/2760940614

https://headtr1p.com/peripherals/ducky-one-2-mini-arrow-keys

鍵盤電路原理
https://ergotaiwan.tw/self-keyboard-basic-1/

如何將鍵盤使用qmk fireware燒寫
https://ziteh.github.io/posts/diyqmkkeyboard-2/
https://progcat.gitlab.io/p/bacon-65-%E8%B2%B3-%E6%BA%96%E5%82%99nuc123%E7%9A%84%E9%96%8B%E7%99%BC%E7%92%B0%E5%A2%83/



Q：如果想自己修改鍵盤firmware，但是又怕自己把firmware改壞，怎麽辦？
A：想到的辦法有，備份原有的firmware
從官方的update firmware將fireware程式copy出來
這裏剛好看到一篇文章介紹如何做到。
https://www.reddit.com/r/DuckyKeyboard/comments/zdkbn1/upgrade_firmware_for_ducky_one_3_tkl_rgb_on/
https://www.reddit.com/r/DuckyKeyboard/comments/zker40/upgrade_firmware_for_ducky_one_3_tkl_rgb_on
看起來很像是把原廠的firmware解出來，這樣可以做到我要的備份firmware
貌似可以在虛擬機逆向工程他（poster說他是這樣做的

https://blog.csdn.net/qq_36810852/article/details/107377821
https://blog.csdn.net/pq113_6/article/details/106541581
應該是可以直接在Wireshark操作，在延申兩篇wireshark usbcap操作

Ghidra 看起來是一款與ida pro相似的逆向程式，但是他是Java寫的
nu-isp-cli 看來使用這個，應該是新唐的cli，不知道是不是原生的，會比較簡單
總結兩個辦法
1. 使用hidapitester發送訊號給鍵盤進入bootloader模式，然後等5秒，nu-isp-cli更新韌體
2. usb鍵盤開機用 d l 進入bootloader，nu-isp-cli更新
根據上面網友提的，再來我應該要，通過usb接上鍵盤，使用原廠的fireware update，然後把原始的fireware逆向出來，在u-boot不損壞的情況下，應該可以還原。
1. 接上usb，進入boot模式
2. 更新fireware
3. 使用wireshark usbcap捕獲bin看看([[How to capture USB packets via Wireshark]])
4. 然後可以在用Ghidra或是ida pro把代碼解析出來看看

如果不小心把鍵盤燒成磚，可能可以用這個icp修好u-boot，但是真的到這裏就...有點慘了...
p.s. nuc123這個晶片，看起來是arm的系統跟一般的mcu不一樣，所以他有自己的kernel，應該吧
https://danchouzhou.blogspot.com/2017/11/numicro-isp.html?m=1

https://cloud.tencent.com/developer/article/1515285
binwalk看起來有搞頭，可以快速提取檔案，但是不知道能不能提取exe中的bin
利用binwalk取出檔案內容 binwalk --dd='.*' <檔案名稱>

還有其他的工具像是
* resource hacker 免費看起看只能改exe的資源，但是不能提取文件
* Resource Tuner 要錢

應該也可以先從新唐這裡入手，從source build一個bin，來看build出來的東西會長怎樣
https://github.com/Pr0gCat/Bacon65

應該可以用新唐的工具先找到我鍵盤arm的型號
-> 看起來我的晶片是 NUC1261SG4AE 但是我的APROM跟Data有點大，不知道是不是因爲我改過設定的關係
https://www.techpowerup.com/review/ducky-one-3-sf/4.html
這裏有相似的鍵盤layout
http://www.51hei.com/bbs/dpj-40116-1.html
燒錄看起來有兩種方式 icp與isp，icp需要專用工具，isp可以通過usb燒錄。當然icp比isp多支持燒寫ldrom，雖然還不知道那個是幹嘛的
我的aprom 跟 data看起來很大，是因爲我有修改鍵盤設定嗎，可以把鍵盤設定回復出廠模式看看
看了資料LDROM應該是存bootload用的，我要搞的fireware應該就是APROM沒錯

佈局

* 60%的鍵盤沒有上下左右
* 右邊的功能鍵除了shift偶爾會使用到，其他還真的不好用
  其中一個原因是右手有空閑的時候，就會去拿滑鼠
* 另外發現有時候backspace太遠了，每次刪除字，手都要離開（這個是及有問題
* 然後寫程式的時候，使用`+-*/`的情況也是常見（及有問題

情景：
* 瀏覽網站
	* 左手在左鍵區，右手拿滑（或者只有右手拿滑鼠
* 瀏覽代碼
	* 左手一定在左鍵區，隨時保持編輯的狀態
* 編輯代碼
	* 雙手一定在鍵盤標準位置
ctrl 單獨使用
alt不會單獨使用

因爲60鍵盤本身沒有上下左右，有時候要做一些win+方向鍵的時候還是不行，所以把幾乎沒有用到的右側win、alt、ctrl、shift換成上下左右。唯一的遺憾是左shift偶爾還打字會用到，可能在這裏會有些卡頓。

中文打字因爲用的是拼音輸入，這些配置倒沒什麽問題。
英文打字也是沒有問題。
輸入符號的時候，左側的shift被換掉，有點小小差異。
