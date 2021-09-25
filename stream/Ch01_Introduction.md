### 簡介
stream 是java 8出的API，能利用宣告式(Declarative way)*的方式來處理集合中的資料。

下面為簡單的範例程式，能先對何謂stream API有個大略的概念:
```java
import java.util.List;
import java.util.ArrayList;
import java.util.stream.Collectors;


class HelloWorld {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("a");
        list.add("c");
        list.add("b");
        list.add("d");
        List<String> list2 = list.stream() // 回傳一個Stream物件
                                .sorted((a,b)->a.compareTo(b)) // 傳入比較方法
                                .collect(Collectors.toList()); // 將Stream物件轉換為何種集合(reduction operation)
        
        System.out.println(list2);//output: [a, b, c, d]
    }
}


```

### 概念
1. 來自於java.util.stream.Interface Stream<T>
2. Stream operation
   共分成兩大類:
   **(A) intermediate operation**
   filter和sorted等等會回傳另一個Stream物件的方法就是屬於此類，因為這個特性，能夠幫助每個運算串接，已形成像是查詢句子般的語法， <mark>而這類的方法只有當Terminal operation加入這個pipeline時才會開始執行</mark>。

   **(B) Terminal operation**
   負責從pipeline回傳一個非Stream的結果，例如Integer、List或是void。例如上述範例中的collect就是一個Terminal operation。

3. Stream vs Collection
   前者就像是從網路上觀看串流影片一樣，只會先讀取目前消費者所需要看到的片段，後者則是像DVD，需要先將整個檔案都讀取完畢之後才能讓消費者看到畫面。

```java
import java.util.ArrayList;
import java.util.stream.Collectors;

class HelloWorld {
    public static void main(String[] args) {
        
        Meat m1 = new Meat(20,"duck");
        Meat m2 = new Meat(30,"beef");
        Meat m3 = new Meat(60,"chicken");
        Meat m4 = new Meat(70,"port");
        
        List<Meat> list = new ArrayList<>();
        list.add(m1);
        list.add(m2);
        list.add(m3);
        list.add(m4);
       
        List<String> result = list.stream()
                                .filter((e)->{
                                    System.out.println("the "+e.getName() + " is filtering.");
                                    return e.getWeight() > 50;
                                })
                                .map((e)->{
                                    System.out.println("the "+e.getName() + " is Mapping.");
                                    return e.getName();
                                })
                                .collect(Collectors.toList());
        System.out.println(result);
        // output:
        // the duck is filtering.
        // the beef is filtering.
        // the chicken is filtering.
        // the chicken is Mapping.
        // the port is filtering.
        // the port is Mapping.
        // [chicken, port]
    }        
}

class Meat {
    int weight;
    String name;
    
    public Meat(int weight,String name){
        this.weight = weight;
        this.name = name;
    }
    public int getWeight(){
        return this.weight;
    }
    
    public String getName(){
        return this.name;
    }
}
```

4. 只能讀取一次
   就像Iterator一樣，只能遍歷一次，若要再進行一次則需要從原來的集合中拿取新的stream。

### 總結
使用Stream介面有三個構成要素:
1. data source ，例如集合
2. itermediate operation 能夠將各種運算串接起來的pipeline
3. terminal operation 幫助執行stream pipeline並回傳一個結果
其實整體而言整個Stream API就像是builder pattern。

*宣告式(Declarative way): 是一種寫成式的方式，常被用來與命令式(Imperative way)做比較，詳細請參考Declarative_Imperative.md