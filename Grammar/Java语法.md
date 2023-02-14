# Java语法笔记

每个 Date 对象以一种非常有趣的形式存储时间：自格林威治标准时间 1970 年 1 月 1 日以来的毫秒数。这个数字太大，以至于 **int** 中没有足够的空间容纳它，因此必须将其存储在 **long** 中。但是，计算任意两个日期之间的差值非常方便。只需执行减法即可得到精确到毫秒的差值。它还解决了日期变更线和夏令时的问题。

### 获取当前日期

```java
public static void main(String[] args) throws Exception
{
     Date today = new Date();
     System.out.println("当前日期：" + today);
}
```



### 计算两个日期之间的差值

```java
public static void main(String[] args) throws Exception
{
    Date currentTime = new Date();           // 获取当前日期和时间
    Thread.sleep(3000);                      // 等待 3 秒（3000 毫秒）
    Date newTime = new Date();               // 获取新的当前时间

    long msDelay = newTime.getTime() - currentTime.getTime(); // 计算差值
    System.out.println("时间差值为：" + msDelay + "，以毫秒表示");
}
```



## ArrayList 和 LinkedList

在内部，**ArrayList** 是作为普通数组实现的。因此，在中间插入元素要求我们首先将所有后续元素移动一个位置，然后将新元素放入空闲插槽。获取和设置元素（get、set）的速度很快，因为这些操作只是处理相关的数组元素。

**LinkedList** 具有不同的内部结构。它是作为包含相互关联元素的列表实现的：一组不同的元素，每个元素存储对列表中下一个和上一个元素的引用。要将元素插入此类列表的中间位置，只需更改其未来邻近元素的引用即可。但是，要获取第 130 个元素，必须从 0 到 130 遍历每个对象。换句话说，get 和 set 操作的速度会很慢.



| 说明                   | 操作         | ArrayList | LinkedList |
| ---------------------- | ------------ | --------- | ---------- |
| 获取元素               | get          | 快        | 慢         |
| 设置元素               | set          | 快        | 慢         |
| 添加元素（到列表末尾） | add          | 快        | 快         |
| 插入元素（在任意位置） | add(i,value) | 慢        | 快         |
| 删除元素               | remove       | 慢        | 快         |

### 可以对映射进行的操作

| 操作               | 方法               |
| ------------------ | ------------------ |
| 获取所有的集合     | entrySet()         |
| 获取所有键的集合   | KeySet()           |
| 获取所有值的集合   | values()           |
| 添加对             | put(key,value)     |
| 获取指定键的值     | get(key)           |
| 检查指定键是否存在 | containsKey(key)   |
| 检查指定值是否存在 | containsValue(key) |
| 检查映射是否为空   | isEmpty()          |
| 清除映射           | clear()            |
| 删除指定键的值·    | remove(key)        |

## ArrayList

- ArrayList默认长度是10

```java
public static void main(String[] args) {
   ArrayList<Car> cars = new ArrayList<>();
}
```

## Collections类

- 排序

Collections.sort();

- 最大值和最小值
- 倒叙 reverse()
- 打乱顺序 shuffle()
- 判断是否innerjoin disjoint()

## LinkedList

- addFirst();在链表开头添加
- addLast();在链表结尾添加
- peekFirst();返回第一个元素
- peekLast();返回最后一个元素
- pollFirst();pollLast()返回然后删除



## Map

```java
HashMap<Integer, String> passportsAndNames = new HashMap<>();
```

- putAll()两个map组成一个
- Map.Entry分解了整个map,entrySet() 返回一个list形式

## Calender

```java
public static void main(String[] args) {

  Calendar calendar = new GregorianCalendar(2017, 0 , 25);
}
```

```java
public static void main(String[] args) {
   Calendar calendar = new GregorianCalendar();
   calendar.set(Calendar.YEAR, 2017);
   calendar.set(Calendar.MONTH, 0);
   calendar.set(Calendar.DAY_OF_MONTH, 25);
   calendar.set(Calendar.HOUR_OF_DAY, 19);
   calendar.set(Calendar.MINUTE, 42);
   calendar.set(Calendar.SECOND, 12);

   System.out.println(calendar.getTime());
}
```

## 异常处理

### try catch

- 如果 **try** 块中发生异常，代码会在发生异常的位置停止执行，此时 **catch** 块开始执行。
- 如果没有异常发生，那么 try 块执行到最后，而且 **catch** 块不会执行。

在 Java 中，异常分为两种：已检查和未检查（即必须捕获的异常和不必捕获的异常）。默认情况下，必须捕获所有[异常](https://codegym.cc/groups/posts/exceptions-in-java)。

如果方法中抛出ClassNotFoundException或FileNotFoundException，那么程序员仅需在方法中指出它们。这些就是已检查异常。



## 抽象类

- 抽象类可以声明方法，而无需实现它
- 抽象方法会带有关键字==abstract==标记，如果一个类有多个抽象方法，那这个类也可以标记为abstract。
- 我们无法给抽象类创建对象，有如此意图的代码讲无法编译     

 在所有的普通方法上都会有一个人{}，这个表示方法体，抽象方法是指没有方法体的方法，必须加abstract做修饰。

​          

- 抽象方法i虚伪public或proteced，缺省情况下默认为public；
- 抽象类不能直接实例化，需要依靠子类向上转型的方式处理；
- 抽象类必须有子类，使用extends继承，一个子类只能继承一个抽象类
- 子类必须覆写抽象类之中的全部抽象方法

​                                                                                                                                                                                                                                                                                                                                                                                                                    
