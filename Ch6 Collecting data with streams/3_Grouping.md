# Grouping

## groupingBy source code
第一個參數傳入分類規則，第二個則是對每一個群組內的類別的操作
```java
public static <T, K, A, D>
    Collector<T, ?, Map<K, D>> groupingBy(Function<? super T, ? extends K> classifier,
                                          Collector<? super T, A, D> downstream) {
        return groupingBy(classifier, HashMap::new, downstream);
    }
```

將stream內的elemement分群
```java
Map<DishTypeEnum, List<Dish>> result = Stream.of(new Dish("FISHA", 50, DishTypeEnum.FISH),
                                                new Dish("FISHB", 100, DishTypeEnum.FISH),
                                                new Dish("MEATA", 200, DishTypeEnum.MEAT), 
                                                new Dish("MEATB", 300, DishTypeEnum.MEAT))
                                                .collect(groupingBy(Dish::getType)); 
// {MEAT=[Dish [type=MEAT, name=MEATA, calories=100], Dish [type=MEAT, name=MEATB, calories=100]], FISH=[Dish [type=FISH, name=FISHA, calories=100], Dish [type=FISH, name=FISHB, calories=100]]}

```
操作各群組間的elements
```java
Map<DishTypeEnum, Long> groupByAndCounting =  Stream.of(new Dish("FISHA", 50, DishTypeEnum.FISH),
                                                        new Dish("FISHB", 100, DishTypeEnum.FISH),
                                                        new Dish("MEATA", 200, DishTypeEnum.MEAT),
                                                        new Dish("MEATB", 300, DishTypeEnum.MEAT))
                                                    .collect(groupingBy(Dish::getType,counting()));
		
System.out.println(groupByAndCounting);
// {MEAT=2, FISH=2}
```

groupingBy的第二個參數可以放各種不同的Collectors，只要把group想成是產生多個stream。