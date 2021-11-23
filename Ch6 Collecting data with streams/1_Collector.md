# Collector
在這個章節主要是介紹Collectors utility裏頭的static collector factory方法，若要自定義Collector，需參考Collector interface方法。

* 呼叫collector方法會引起reduction operation，讓所有element經過collector後轉換成另一個資料結構。
* stream中的collect方法的參數
* 可以將stream中的element轉換成collection
* Collectors utility提供很多static的方法建立collector物件實體(predefined Collector)，例如Collectors.toList(),maxBy(Collector collector)

# Collectors utility Predefined Collector
主要提供三類  
* Reducing and summarizing
* Grouping
* Partitioning

分別由接下來的章節介紹

[2_Reducing and summarizing](/Ch6%20Collecting%20data%20with%20streams/2_Reducing%20and%20summarizing.md)