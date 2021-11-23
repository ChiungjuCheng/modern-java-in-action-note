# Reducing and summarizing
## 找到最大值
```java
import static java.util.stream.Collectors.*; // Collectors類別內有很多static的Collectors工廠方法

public class CollectorDemo {
	public static void main(String[] args) {

		Comparator<Dish> dishCaloriesComparator = Comparator.comparingInt(Dish::getCalories);
		
		Stream.of(new Dish("dishA",100),new Dish("dishB",200))		
			.collect(maxBy(dishCaloriesComparator)) // maxBy 來自Collectors
			.ifPresent(System.out::println);
	}
}
```

## 平均
```java
double average = Stream.of(new Dish("dishA",100),new Dish("dishB",200))
                        .collect(averagingInt(Dish::getCalories));
System.out.println(average);
```

## reduce方法
reducing(Initial value, Transformation function, Aggregating)
```java
int sum =  Stream.of(new Dish("dishA",100),new Dish("dishB",200))
				.collect(reducing(0,Dish::getCalories,Integer::sum));
		
System.out.println(sum);
```