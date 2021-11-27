# removeIf 移除特定元素
若使用for-each並且用Collection方法移除元素的話會拋出ConcurrentModificationException，一定要使用Iterator的remove才行。
Java 8提供removeIf解決這個困境
```java
List<String> alphabets = Stream.of("A", "B", "C").collect(Collectors.toList());
alphabets.removeIf(alphabet->"C".equals(alphabet));
alphabets.forEach(System.out::println); // A B
```

# replaceAll 取代元素
若使用map和collectors會產生一個新的List。
```java
// map + collector
alphabets.stream()
		.map(alphabet->{
			if("A".equals(alphabet)) {
				return "D";
			}			
			return alphabet;
		})
		.collect(Collectors.toList())
		.forEach(System.out::println);// DBC
```

但有時只想改變stream內元素的值，可以使用replaceAll

```java
alphabets.replaceAll(alphabet->{
			if("A".equals(alphabet)) {
				return "D";
			}			
			return alphabet;
		});
alphabets.forEach(System.out::println); // DBC
```