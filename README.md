# Skript 基礎教學


****<a class="link-gray" href="https://github.com/SkriptLang/Skript/releases">Skript</a>是一款 <a class="link-gray" href="https://www.minecraft.net/zh-hant/">Minecraft</a> 的腳本插件 , 其主要功用為提供給不會寫程式語言的人 , 讓他們能撰寫屬於自己的腳本****

****Skirpt(以下簡稱SK) , SK你可以將它當作一個程式語言 , 因為他的語法較為簡單 , 比較好理解 , 是屬於高階語言 , 如果你接觸過Python , 那你對SK的上手速度會快上很多****

****SK非常適合想寫Minecraft插件但自己不會編寫的初學者 , 他可以利用簡簡單單的幾行完成一個腳本 , 並且能隨改隨生效 , 非常適合作為寫插件前的初學者****

****我該如何安裝SK呢? 請參考以下文章: <a class="link-gray" href="https://forum.gamer.com.tw/C.php?bsn=18673&snA=123879">Here</a>****

****我這裡比較強調實作應用 , 所以每講完一個基本要素 , 就會帶入更多它的實作應用給您****

****
# 進入正篇教學

SK 其主要組成要素有: Events(事件), Effects(效果), Expressions(表達式), Conditions(條件), Variables(變數), Functions(函式), Loops(迴圈或等等用法...)

# 1.Events
  事件: 他是一種動作 , 當玩家在做 或者 做完某個動作時會觸發以下的動作......
  ```diff+
  On Death of player: #這就是一個事件 , 當玩家死後會觸發下列效果
    broadcast "%player% 你怎麼死了OAO???"  #廣播 %player% 你怎麼死了OAO???
  ```
  
  ```diff
  + 現在想做一個破壞玻璃會掉落玻璃的腳本
  On break of glass: #當玻璃被破壞時
    drop 1 glass at event-location #掉落一個玻璃在被破壞的位置
 ```
 


