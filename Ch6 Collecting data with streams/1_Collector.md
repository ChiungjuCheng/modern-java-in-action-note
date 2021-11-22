# Collector
* 呼叫collector方法會引起reduction operation，讓所有element經過collector後轉換成另一個資料結構。
* stream中的collect方法的參數
* 可以將stream中的element轉換成collection
* Collectors utility提供很多static的方法建立collector物件實體，例如Collectors.toList()、maxBy(Collector collector)

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