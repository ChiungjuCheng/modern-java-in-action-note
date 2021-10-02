Java8提供許多新的functional interface 在java.util.function的套件當中。
# Predicate
傳入一個物件，並回傳boolean

```java
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);

}
```
source code
https://github.com/frohoff/jdk8u-jdk/blob/master/src/share/classes/java/util/function/Predicate.java

# Consumer
傳入一個物件，並回傳void。
當要對一個物件進行運算時，會用到Consumer，例如使用forEach印出List裡面的所以物件。
```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```
https://github.com/frohoff/jdk8u-jdk/blob/master/src/share/classes/java/util/function/Consumer.java
```java
# Function
傳入一個物件，並回傳另一種物件。
使用stream的map可以使用
```java
@FunctionalInterface
public interface Function<T, R> {

    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);
}
```

https://github.com/frohoff/jdk8u-jdk/blob/master/src/share/classes/java/util/function/Function.java

# Primitive specializations
上述三種都是要傳入參考，而可以傳入基本型別是因為Java有auto-boxing的機制，但若在整個執行當中，不斷的auto-boxing 或 unboxing且物件都是儲存在Heap中，因此會影響到效能，，因此上述的Functional 都有其相對應的基本型別可以使用，例如IntPredicate:
傳入一個基本型別int值

```java
@FunctionalInterface
public interface IntPredicate {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param value the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(int value);
}
```

