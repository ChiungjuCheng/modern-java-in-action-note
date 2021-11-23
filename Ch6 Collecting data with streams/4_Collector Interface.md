# Collector interface
* T - stream中的element型別
* A - accumulator的型別，在collection的過程中，有部分已經處理好的結果會被裝在這個型別中
* R - collect operation回傳的型別
```java
public interface Collector<T, A, R> {
    Supplier<A> supplier();
    BiConsumer<A, T> accumulator();
    BinaryOperator<A> combiner();
    Function<A, R> finisher();
    Set<Characteristics> characteristics();
}
```
# Collector 方法的執行步驟
1. supplier - 回傳Result container，讓運算完的結果可以放在此container中。
```java
public Supplier<List<T>> {
    return ArrayList::new
}
```
2. accumulator 回傳可以執行reduction operation的function，這個function將已經traversed的element放進result container。
```java
public BiConsumer<List<T>, T> accumulator(){
    return List::add; // (list, item) -> list.add(item);
}
```
3. finisher 將Result container轉換成需要的型別，但通常在執行完整個collection process的時候，result container已經轉換成需要的型別了，因此可以回傳identity方法 (相當於回傳自己)。
```java
public Function<List<T>, List<T>> finisher(){
    return Function.identiy();
}
```
以上三個步驟使用下圖表示(取自書籍)
![CollectorProcess](/Picture/CollectorProcess.jpg)

4. combiner 合併兩個result container，在toList中則會是簡單的呼叫list.addAll

# 使用Lamda自定義Collector
除了真的寫一個Collector的實作類別並override所有需要的方法外，可以直接在stream的collect方法中，傳入lamda。
以下是很簡單的將數字1到10乘以2後加到新的List裡面。
```java
IntStream.rangeClosed(0, 10).boxed()
		.collect(()-> new ArrayList<Integer>(), // Supplier
							
				(list, number)-> list.add(number*2), // Accumulator
							
				(list1, list2)-> list1.addAll(list2)) //Combiner
					
		.forEach(System.out::print);
```