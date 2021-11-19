# 尋找特定的Element

## allMatch, anyMatch, moneMatch
Stream中有無element符合傳入方法的predicate(條件)，若確定結果則會讓方法提早結束並回傳boolean。

```java
boolean result = Stream.of("A","B","C")
		                .anyMatch(text->"A".equals(text));
System.out.println(result); // true
	
result = Stream.of("A","B","C")
	            .allMatch(text->"A".equals(text));
System.out.println(result); // false
	    
result = Stream.of("A","B","C")
	        .noneMatch(text->"D".equals(text));
System.out.println(result); // true
```

## findAny, findFirst

和filter搭配使用，若有Elememt通過filter，則回傳該元素。
使用parallism才會注意到兩者的差異，在parallel中findFirst是有受到限制的，若不在意到底是哪個Element回傳，則可以使用findAny
```java
Stream.of(1,2,3,4,5)
	.filter(number-> number > 3)
	.findAny() // 回傳Optional
	.ifPresent(System.out::println); // 4

```