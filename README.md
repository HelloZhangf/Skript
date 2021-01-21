# Skript 基礎教學

****因為我要準備學測! , 所以更新的速度很慢喔!****

****<a class="link-gray" href="https://github.com/SkriptLang/Skript/releases">Skript</a>是一款 <a class="link-gray" href="https://www.minecraft.net/zh-hant/">Minecraft</a> 的腳本插件 , 其主要功用為提供給不會寫程式語言的人 , 讓他們能撰寫屬於自己的腳本****

****Skirpt(以下簡稱SK) , SK你可以將它當作一個程式語言 , 因為他的語法較為簡單 , 比較好理解 , 是屬於高階語言 , 如果你接觸過Python , 那你對SK的上手速度會快上很多****

****SK非常適合想寫Minecraft插件但自己不會編寫的初學者 , 他可以利用簡簡單單的幾行完成一個腳本 , 並且能隨改隨生效 , 非常適合作為寫插件前的初學者****

****我該如何安裝SK呢? 請參考以下文章: <a class="link-gray" href="https://forum.gamer.com.tw/C.php?bsn=18673&snA=123879">Here</a>****

****我這裡比較強調介紹更多語法以及其他功能 , 所以基礎觀念基本上都是帶過 , 有問題的朋友寫可以用 <a class="link-gray" href="https://github.com/HelloZhangf/Skript/issues">Issues</a> 問我****

****
# 進入正篇教學
- [1.Events](#1events)
SK 其主要組成要素有: <a class="link-gray" href="#-1.Events">Events</a>(事件), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#2effects">Effects</a>(效果), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#3expressions">Expressions</a>(特定物件), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#4conditions">Conditions</a>(條件), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#5Variables">Variables</a>(變數), <a class="link-gray" href="https://github.com/HelloZhangf/Skript/blob/master/README.md#6commands">Commands</a>(製作指令), Loops(迴圈或等等用法...) , Functions(函式)

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
  
 # 注意! SK在寫的時候 , Notepad++中(同個.sk檔案內 , 在換行時候 , 請一併使用同個空格格式 例如: 4個 空白建(或兩個空白鍵) = 一個tab)-->除非特別設定
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
  表達一個指定的物件 , 可以是玩家 , 物品 , 方塊等等......
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
  On damege:                                                #當實體在受傷的時候
    if victim is a player:                                  #受傷的實體是玩家
      send "你受到了伺服器的保護!" to victim                 #告訴受傷的玩家 你受到了伺服器的保護! 
      send "伺服器保護著所有人以至於你打不到他!" to attacker  #伺服器保護著所有人以至於你打不到他!
      cancen event                                          #取消受傷事件
```
****由上面可知 , 不用else也能 , else 是用在當條件有正反兩個或兩個以上結果時要用 , EX: 當A是B 就執行 , A不是B 就執行ELSE****

****

# 5.Variables
  變數可以存放Value(值) , 可以存許多東西 , EX:數字 , 字串 , 等等......
  
  在SK的變數分為兩種:
  
  ```
  區域變數(本地變數):
    用法: {_LocalVariable} , 以兩個大括號以及一個底線為主 , 同樣名稱的區域變數 , 只能在單一事件內使用 , 跨事件就會完全是不一樣的Value , 並且會隨著事件結束而刪除
    主要用於: 單一事件內的計算或者將某物件存放在變數內簡化其寫法
  ```
****
  ```
  全域變數(全局變數):
    用法: {GlobalVariable} , 以兩個大括號為主 , 可以跨事件使用 , 並且無刪除之前 , 都會一直存在(直到關服) , 否則他就會占用著伺服器記憶體 
    主要用於: 如上 , 如若要做跨事件 , 就必須用到 , 其主要功能與區域變數一樣 , 在於事件結束會不會不見
  ```
****
  ```
  列表變數(陣列):
    用法: {_ListVariable::*} or {ListVariable::*} , 跟其他變數一樣 , 後面加上兩個冒號或一個*或其他value , 上面那兩個變數只能儲存單個value , 列表變數則可一次儲存大於一個的value
    主要用於: 當要記錄超過一個的值時 , 就可以使用
  ```
****

```diff
+ 死亡位置
On Death:                                        #在玩家死亡的時候 , 也可寫成 event-entity is player
  victim is player                               #死亡的實體是玩家
  set {_DeathLoc} to event-location              #將玩家死亡的位置存放到 {_DeathLoc}
  send "%{_DeathLoc}% 是你的死亡位置" to victim   #告訴死亡的玩家 %{_DeathLoc}% 是你的死亡位置 , %%一樣可以把變數內存在的value印出來
```
****
```diff
+ 死亡次數 
On Death:                                                              #在玩家死亡的時候 , 也可寫成 event-entity is playe
  victim is player                                                     #死亡的實體是玩家
  if {NumberOfDeath.%player%} is not set:                              #如果計算玩家死亡次數的變數未設置
    set {NumberOfDeath.%player%} to 1                                  #將計算死亡次數的變數設置為1 ,也就是玩家第一次死亡
    send "你的死亡次數已累積至: %{NumberOfDeath.%player%}%" to victim   #告訴死亡的玩家 你的死亡次數已累積至: %{NumberOfDeath.%player%}%
  else:                                                                #如果計算玩家死亡次數的變數已經設置過了
    add 1 to {NumberOfDeath.%player%}                                  #加一到計算玩家死亡的變數
    send "你的死亡次數已累積至: %{NumberOfDeath.%player%}%" to victim   #告訴死亡的玩家 你的死亡次數已累積至: %{NumberOfDeath.%player%}%
```
****
```diff
+ 破壞紀錄
On break:                             #當玩家破壞方塊時
  add {BlockLog::*} to event-block    #將玩家破壞的方塊添加到 {BlockLog::*} 此列表裡面
  send "%{BlockLog::*}%"              #告訴玩家 %{BlockLog::*}% , 如你破壞了 泥土 , 草地 , 玻璃 那將他列印出來會是 --> Dirt , Grass , Glass  
```
****變數的應用很廣 , 如果你想寫個很強大的腳本 , 絕對不能缺少****

# 6.Commands
  SK可以註冊屬於自己的指令 , 指令可以當作一個事件 , 執行後觸發effects
  ```diff
  + 註冊指令
  commnad /sayhi: #註冊一個指令 : /hi
    trigger:      #這是註冊指令必寫語句 , 意思就是執行這指令會觸發什麼Effects
      send "hi"   #告訴玩家 hi
  ```
  ****
  ```diff
  + 傳送點設置
  command /setpoint [<text>]:                          #註冊一個指令: /setpoint <可輸入文字>
    trigger:                                           #這是註冊指令必寫語句 , 意思就是執行這指令會觸發什麼Effects
      if player is op:                                 #檢查玩家是否是OP , 如果不是就跳到他對應的else (也可改成if player has permission "<你想要的權限>":)
        if arg exists:                                 #檢查 <文字> 是否有輸入 , 如果不是就跳到他對應的else 
          arg is not "list"                            #玩家輸入的點不是List此名稱 , list是下面Loop範例會用到的檢查傳點需要與用到的 
          set {point::%arg%} to location of player     #將玩家的位置添加到 {point::*} 此列表
          send "名稱: %arg% 的位置設置成功"             #告訴玩家 名稱: %arg% 的位置設置成功 ,arg = argument , 也就是指令 /setpoint <text> 所輸入的<text> ,EX: /setpoint 家
          stop                                         #停止繼續往下執行 , 這可不能亂加 , 如果你想要執行完以上的effects之後不要往下執行才加 , 不需要則不用加
        else:                                          #當arg 沒有輸入時
          send "請輸入位置的名稱!"                      #告訴玩家 請輸入位置的名稱!
          send "指令用法: /setpoint <傳點名稱>"         #告訴玩家 指令用法: /setpoint <傳點名稱>
          stop                                         #停止繼續往下執行 , 這可不能亂加 , 如果你想要執行完以上的effects之後不要往下執行才加 , 不需要則不用加
      else:                                            #當玩家不是OP時
        send "你並不是管理員!"                          #告訴玩家 你並不是管理員!
   ```
   ****
# 7. Loops
  loop 的用法有很多種 , 包括檢查列表變數內的值 , 或者當迴圈使用
  ```diff
  + loop列表
  command /pointlist                            #註冊一個指令: /pointlist
    trigger:                                    #這是註冊指令必寫語句 , 意思就是執行這指令會觸發什麼Effects
      loop {point::*}:                          #逐一檢查 {point::*} 裡面的每一個value
        send "%loop-index% : %loop-value%"      #告訴玩家 %loop-index% : %loop-value% , 其中loop-index傳送點設置時的 title , 然後他裡面還存放著一個value , 那也就是當初設置的位置
                                                #EX: 當初設定點名稱為: pointest , 腳下位置在 x= 100 y=63 z= 100 ,那依照我這樣寫印出來會是: pointset : x= 100.0 , y= 63.0 , z= 100.0
 ```
 ****
 接下來介紹他<a class="link-gray" href="https://zh.wikipedia.org/wiki/%E8%BF%B4%E5%9C%88">迴圈</a>的用法
 
 SK的迴圈分為兩種 , 一種是 ```loop``` , 則另一種是 ```while```
 
 ```
 loop 迴圈:
  通常用在知道迴圈執行次數時
```

```
while 迴圈:
  通常用在不知道迴圈執行次數時 , 無止盡的迴圈 , 或是等到迴圈判斷條件不符合時
```

****
```diff
Loop 迴圈範例
+ 計算
command /count:           #註冊一個指令: /count
  trigger:                #這是註冊指令必寫語句 , 意思就是執行這指令會觸發什麼Effects
    set {_count} to 0     #將 {_count} 此變數的value設置成0
    loop 100 times:       #將在迴圈內的Effects 執行一百次
      add 1 to {_count}   #當每次在執行時 , +1 到 {_count} 此變數
    send "%{_count}%"     #當結束迴圈時 , 告訴告玩家 {_count} 內的 value , 如果將send 寫在迴圈內 , 將在每次執行結果告訴玩家
```

****

```diff
while迴圈範例
+ 計算
command /count:            #註冊一個指令: /count
  trigger:                 #這是註冊指令必寫語句 , 意思就是執行這指令會觸發什麼Effects
    set {_count} to 0      #將 {_count} 此變數的value設置成0
    while {_count} < 100:  #當{_count} 內的 value 小於 100時會執行以下Effects
      add 1 to {_count}    #當每次在執行時 , +1 到 {_count} 此變數
    send "%{_count}%"      #當結束迴圈時 , 告訴告玩家 {_count} 內的 value , 如果將send 寫在迴圈內 , 將在每次執行結果告訴玩家
```

****

****由上兩範例結果 , 可得知 ,Loop迴圈是用在明確知道迴圈內的 Effects要執行幾次而達到你想要的結果才結束 ; While迴圈則是當條件未符合時 , 執行到條件不符合時****

```diff
+ loop 其他用法
On death of player:                         #當玩家死亡的時候
  loop blocks in radius 3 of victim:        #loop 以玩家為中心的半徑三的範圍之方塊
    set loop-blocks to air                  #將loop到的方塊設置成為 空氣
  broadcast "%victim% 死亡時吞噬了旁邊的方塊"   #廣播 %victim% 死亡時吞噬了旁邊的方塊
```

****
loop 除了 迴圈 以外還有檢查半徑的用法 , 所以loop是一個很重要的語法 , 能善用者就能寫出很厲害的東西
****


