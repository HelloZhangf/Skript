# Skript 基礎教學


****<a class="link-gray" href="https://github.com/SkriptLang/Skript/releases">Skript</a>是一款 <a class="link-gray" href="https://www.minecraft.net/zh-hant/">Minecraft</a> 的腳本插件 , 其主要功用為提供給不會寫程式語言的人 , 讓他們能撰寫屬於自己的腳本****

****Skirpt(以下簡稱SK) , SK你可以將它當作一個程式語言 , 因為他的語法較為簡單 , 比較好理解 , 是屬於高階語言 , 如果你接觸過Python , 那你對SK的上手速度會快上很多****

****SK非常適合想寫Minecraft插件但自己不會編寫的初學者 , 他可以利用簡簡單單的幾行完成一個腳本 , 並且能隨改隨生效 , 非常適合作為寫插件前的初學者****

****我該如何安裝SK呢? 請參考以下文章: <a class="link-gray" href="https://forum.gamer.com.tw/C.php?bsn=18673&snA=123879">Here</a>****

****我這裡比較強調實作應用 , 所以每講完一個基本要素 , 就會帶入更多它的實作應用給您****

****
# 進入正篇教學

SK 其主要組成要素有: <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#1events">Events</a>(事件), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#2effects">Effects</a>(效果), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#3expressions">Expressions</a>(表達式), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#4conditions">Conditions</a>(條件), Variables(變數), Functions(函式), Loops(迴圈或等等用法...)

首先你要到 Plugins資料夾內找到Skript , 然後進去 , 再找到 Script這個資料夾 , 並在裡面創立一個 名為 ```<想要的名稱>. sk``` 的資料夾

注意! 副檔名一定要是```.sk``` , 不然SK不會去讀取他

在檔案面前加上 ```-``` 就不會去讀取 EX: ```-Hello.sk```

常用SK指令:

```/sk reload all``` 重新讀取全部SK檔案

```/sk reload <檔名>``` 重新讀取指定的檔案(不用加副檔名)

# 1.Events
  事件: 他是一種動作 , 當玩家在做 或者 做完某個動作時會觸發以下的動作......
  ```diff
  On Death of player: #這就是一個事件 , 當玩家死後會觸發下列效果
    broadcast "%player% 你怎麼死了OAO???"  #廣播 %player% 你怎麼死了OAO??? ,%player% 是一種變量 , 就是兩個%%裡面放要顯示出來的物件 ex:%now% , %name of player's tool% , %player's uuid%
  
 # 注意! SK在寫的時候 , 同個.sk檔案內 , 在換行時候 , 請一併使用同個空格格式 例如: 4個 空白建(或兩個空白鍵) = 一個tab
 - 不然會出錯!
 - 錯誤訊息: indentation error: expected 4 spaces, but found 1 tab
 
 
 ```
  ****
  ```diff
  + 玻璃掉落
  On break of glass: #當玻璃被破壞時
    drop 1 glass at event-location #掉落一個玻璃在被破壞的位置
 ```
 ****
 ```diff
 + 玩家初次加入
 On first join: #當玩家第一次加入
  chance of 50%: #有50%的機率觸發以下條件
    ban player due to "你是天選之人!" #BAN掉他並且告訴他是天選之人
 ```
 ****
 ```diff
 + 右鍵傳訊息
 On rightclcik: #當玩家按右鍵的時候
  send "HI" to player #發送HI給玩家
```
****


# 2.Effects
  顧名思義 , 就是當事件被觸發時會執行的腳本 , 直接給範例
  
  ```diff
  + 加入廣播
  On join: #當玩家加入遊戲時
    broadcast "%player% 闖進伺服器!"  #廣播 %player% 闖進了伺服器 , 建議用set join message
 ```
 因這個比較簡單 , 這就介紹到這
 ****
 
 # 3.Expressions
  這個介紹起來比較抽象 , 他就是類似像 ```set ......``` 可以去做其他操作的語句
  ```diff
  + 更改加入訊息
  On join: #當玩家加入遊戲時
    set join message to "&a%player% 加入了HELLOLIME伺服器!" #將登入訊息改為 &a%player% 加入了HELLOLIME伺服器!
  ```
  ****
  ```diff
  + 方塊變空氣
  On rightclick: #當玩家按右鍵時
    clicked block is set #玩家點擊到的種類是方塊
    set event-block to air #將玩家點擊到的方塊設置成空氣(也就是直接清除)
  ```
  
# 4.Conditions
  作為判斷是否往下繼續讀的語法 , ```if```, ```else```, ```else if```
  ```diff
  + 特定物品
  On rightclick:                                 #當玩家按右鍵時
    clicked is set                               #玩家點擊的類型是一個方塊 
    if name of player's tool is "清除大棒":       #如果玩家手持的物品的名稱是 清除大棒 , 就執行以下動作 , 如果不是 , 則讀都不讀直接跳到 else if 或 else ; 注意! 有if 後面要加上冒號 ' : '
      set event-block to air                     #將點擊方塊設置成空氣
      send "指定的方塊已被清除"                   #發送 指定的方塊已被清除 的訊息給玩家 (to player 可加可不加 , 但在特定時候要加 ,例如On damage 或 On death 的事件)
    else if name of player's tool is "閃電棒":    #如果玩家手持的物品的名稱是 閃電棒 , 就執行以下動作 , 如果不 , 則跳到 else 
      strike lightning at the event-location     #打一道閃電在點擊的位置
      send "天雷!"                               #發送 天雷! 的訊息給玩家
    else:                                        # 當上述條件句都未達成是會執行的語句
      send "手上並無指定物品"                     #發送 手上並無指定物品 的訊息給玩家
      
  -不一定一個IF就要配一個 else if 或者 else if 
```
****
```diff
  On damege:                   #當實體在受傷的時候
    if victim is a player:     #受傷的實體是玩家
      cancen event             #取消受傷事件
```
****由上面可知 , 不用else也能 , else 是用在當條件有正反兩個或兩個以上結果時要用 , EX: 當A是B 就執行 , 不是A不是B 就執行ELSE****

****

 
  
  

