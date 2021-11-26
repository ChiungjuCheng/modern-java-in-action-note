# Parallel Stream 
Jave 8之後，可以使用多核心的處理器來做到Parallel Stream。將一個stream裏頭的element拆成好幾個chunks，並使用不同的thread來處理這些chunks，等待處理完後，將結果合併。

![SequentialVsParallelStream](/Picture/SequentialVsParallelStream.jpg)

圖片來源  
https://www.geeksforgeeks.org/what-is-java-parallel-streams/