# of和ofEntries 建立Map
兩種方式建立Map
* of(Key1, Value1, Key2, Value2 ...) 在java中有宣告Overloading的方法，在創建小於10個Entries的Map的時候可以使用，不使用args是因為可以減少多包一層Array。
```java
Map<String, Integer> ageOfFriend = Map.of("Mary",10,"Jerry",12, "Jason",32);
```

* ofEntries 
```java
Map<String, Integer> ageOfFriend = Map.ofEntries(   Map.entry("Mary",10),Map.entry("Jerry",12),Map.entry("Jason",32));
```

# forEach 同時traversing key和value
```java
ageOfFriends.forEach((name, age)->{
			System.out.println(name+" is "+age);
		});
// Jason is 32
// Jerry is 12
// Mary is 10
```
# Sorting

* Entry.comparingByKey 使用key排序
```java
ageOfFriends.entrySet()
	.stream()
	.sorted(Entry.comparingByKey())
	.forEachOrdered(System.out::println);
// Jason=32
// Jerry=12
// Mary=10
```

* Entry.comparingByValue 使用value排序
```java
ageOfFriends.entrySet()
    .stream()
    .sorted(Entry.comparingByValue())
    .forEachOrdered(System.out::println);
// Mary=10
// Jerry=12
// Jason=32
```
# Compute patter - computIfAbsent, computeIfPresent, compute
* computIfAbsent 當key的value不存在或回傳null時執行傳入方法並且回傳值，若key有值則回傳該value且不執行傳入方法。

```java
// 當Bety不存在於map中，就將key傳入方法(第二個方法)中並且執行後回傳
int result =  ageOfFriends.computeIfAbsent("Bety", key-> 0);
// 0
```

這個方法對於value為集合的Map滿有用的，例如要創建Map<String, List>時，當相對應的key沒有list時，先創立一個新的list，若有則直接回傳list
```java
friendsToMovies.computeIfAbsent("Raphael", name -> new ArrayList<>())
            .add("Star War");
```

# Remove pattern

# Replace pattern
# Merge