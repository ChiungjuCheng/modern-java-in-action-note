# Numeric stream
在以下的程式中，Integer要先unboxing後才能做加總，但又不能直接在reduce後面直接加上sum()方法，因為reduce回傳的是Stream，為了解決這個狀況就有了 primitive stream specializations。
```java
int result1 = Stream.of(1,2,3)
                    .reduce(0, Integer::sum);
		
System.out.println(result1); // 6
```

## IntStream, DoubleStream and LongStream
* 讓元素為基本型別，並提供許多相關運算方法，例如sum(),max()等等
* 並不是繼承Stream，而是和Stream一樣繼承BaseStream。
* Stream使用mapToXX轉換成相對應的基本型別Stream。
* 可以將元素再轉回物件

## 使用IntStream計算總和
```java
// 60
int result = Stream.of(new Item(10), new Item(20), new Item(30))
                    .mapToInt(Item::getPrice) // 取得IntStream
                    .sum();
```

## 使用boxed或mapToObj將基本型別Stream轉換回Stream
boxed轉換成相對應的物件型別
```java
IntStream intStream = Stream.of(new Item(10), new Item(20), new Item(30))
                            .mapToInt(Item::getPrice);
		
Stream<Integer> stream =  intStream.boxed();
```
mapToObj轉換成return回來的物件型別
```java
IntStream intStream = Stream.of(new Item(10), new Item(20), new Item(30))
							.mapToInt(Item::getPrice);
intStream.mapToObj(e->"test").forEach(System.out::println); // test test test 
```
## 使用rangeClosed或range產生一個範圍的數字集合
```java
IntStream.range(0, 3)
		    .forEach(System.out::println); // 0 1 2
```