# Reduction operation 
將所有的元素做運算並回傳一個結果，需要兩個參數。
1. 起始值，若沒有則會讓結果回傳Optional物件
2. 結合所有eleme的運算式

使用BinaryOperator<T>();
## 將所有數值加總
```java
// 給初始值
int result1 = Stream.of(1,2,3)
			.reduce(0, Integer::sum);
		
System.out.println(result1); // 6

// 未給定初始值
Stream.of(1,2,3)
	.reduce((a,b) -> a+b) // Integer::sum
	.ifPresent(System.out::println); // 6
```

## 找出最大值和最小值

```java
// 找出最小值
Stream.of(1,2,3)
	.reduce(Integer::min)
	.ifPresent(System.out::println);
		
// 找出最大值
Stream.of(1,2,3)
		.reduce(Integer::max)
		.ifPresent(System.out::println);
```