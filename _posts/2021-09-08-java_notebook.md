---
layout: post
title: java学习笔记
description: 根据在java使用中遇到的困难进行记录
tags: 编程笔记
---

# 小知识点

## 统计程序运行时间

```java
long start = System.currentTimeMillis();
Thread.sleep(1000);
long end = System.currentTimeMillis();
long timeElapsed = end - start; // 单位为毫秒
System.out.println(timeElapsed);
```

## for循环的种类

https://www.yiibai.com/java/java-for-loop.html

## 运算符

异或运算符：`^`

求余运算符：`%`

## 输出百分数

```java
NumberFormat nf= NumberFormat.getPercentInstance();
// 设置保留两位小数
nf.setMinimumFractionDigits(2);
System.out.println(nf.format(3.0/17.0));
```

## 输出固定位数小数

### 输出double

BigDecimal.ROUND_HALF_UP表示四舍五入，BigDecimal.ROUND_HALF_DOWN也是五舍六入，BigDecimal.ROUND_UP表示进位处理（就是直接加1），BigDecimal.ROUND_DOWN表示直接去掉尾数。

```java
new BigDecimal(114.1124).setScale(2, BigDecimal.ROUND_HALF_UP).doubleValue()
```

### 输出String

不确定是否四舍五入

```java
DecimalFormat df = new DecimalFormat("0.00");
System.out.println(df.format(4.0/3.0));
```

[教程链接](https://www.php.cn/java/base/442406.html#:~:text=java%E5%AE%9E%E7%8E%B0double%E4%BF%9D%E7%95%99%E5%B0%8F%E6%95%B0%E7%82%B9%E5%90%8E%E4%B8%A4%E4%BD%8D%E5%B0%8F%E6%95%B0%E7%9A%84%E6%96%B9%E6%B3%95%E6%98%AF%EF%BC%9A1%E3%80%81%E5%9B%9B%E8%88%8D%E4%BA%94%E5%85%A5%EF%BC%8C%E4%BE%8B%E5%A6%82%E3%80%90d%20%3D%20%28double%29%20Math.round%28d,%2A%20100%29%20%2F%20100%E3%80%91%EF%BC%9B2%E3%80%81%25.2f%EF%BC%8C%E4%BE%8B%E5%A6%82%E3%80%90String.format%28%22%25.2f%22%2C%20d%29%E3%80%91%E3%80%82)

## == 与 equal的区别

### [==](https://www.php.cn/java/base/442406.html#:~:text=java%E5%AE%9E%E7%8E%B0double%E4%BF%9D%E7%95%99%E5%B0%8F%E6%95%B0%E7%82%B9%E5%90%8E%E4%B8%A4%E4%BD%8D%E5%B0%8F%E6%95%B0%E7%9A%84%E6%96%B9%E6%B3%95%E6%98%AF%EF%BC%9A1%E3%80%81%E5%9B%9B%E8%88%8D%E4%BA%94%E5%85%A5%EF%BC%8C%E4%BE%8B%E5%A6%82%E3%80%90d%20%3D%20%28double%29%20Math.round%28d,%2A%20100%29%20%2F%20100%E3%80%91%EF%BC%9B2%E3%80%81%25.2f%EF%BC%8C%E4%BE%8B%E5%A6%82%E3%80%90String.format%28%22%25.2f%22%2C%20d%29%E3%80%91%E3%80%82)：

**基本数据类型**（也称原始数据类型） ：byte,short,char,int,long,float,double,boolean。他们之间的比较，应用双等号（==）,**比较的是他们的值**。

**复合数据类型（类）**：当他们用（==）进行比较的时候，比较的是他们在内存中的存放地址（确切的说，**是堆内存地址**）。

### equal：

**复合数据类型**之间进行equals比较，在没有覆写equals方法的情况下，他们之间的比较还是内存中的存放位置的地址值，跟双等号（==）的结果相同；**如果被复写，按照复写的要求来。**

## JSON

JSON是一种与开发语言无关的、轻量级的数据格式。全称`JavaScript Object Notation.`

优点：易于人的阅读和编写，易于程序解析与生产

### 读json

```java
File file=new File("/Users/eleme/IdeaProjects/data/exprawdata/jsonTimeAndOrderId.json");
String content= FileUtils.readFileToString(file,"UTF-8");
JSONArray jsonArray = new JSONArray(content);
JSONArray jsonArray1 = jsonArray.getJSONArray(0);
jsonArray.length();
Long o = Long.parseLong((String) jsonArray1.get(0));
System.out.println("");
```

## assert

assert关键字语法很简单，有两种用法：

 1、assert <boolean表达式>

如果<boolean表达式>为true，则程序继续执行。

如果为false，则程序抛出AssertionError，并终止执行。

2、assert <boolean表达式> : <错误信息表达式>

如果<boolean表达式>为true，则程序继续执行。

如果为false，则程序抛出java.lang.AssertionError，并输入<错误信息表达式>。

##  继承方法的执行顺序

子类继承父类，调用方法时先是调用子类中的方法，如果没有就调用父类中的方法

## 父类强转成子类

Java中父类强制转换成子类的原则：父类型的引用指向的是哪个子类的实例，就能转换成哪个子类的引用。

## 深浅copy

待补充

## 对象的内存地址

HashCode不是内存地址，是根据排列算出来的一个值，相当于对象的身份证，但绝不是内存地址，大家一定要注意这个误区。

## List无法增删

List无法增删：发生问题的原因如下：  https://blog.csdn.net/lin451791119/article/details/82705557
调用Arrays.asList()生产的List的add、remove方法时报异常，这是由Arrays.asList() 返回的市Arrays的内部类ArrayList， 而不是java.util.ArrayList。Arrays的内部类ArrayList和java.util.ArrayList都是继承AbstractList，remove、add等方法AbstractList中是默认throw UnsupportedOperationException而且不作任何操作。java.util.ArrayList重新了这些方法而Arrays的内部类ArrayList没有重新，所以会抛出异常。

## List浅copy

```java
List<Integer> tempSolvingOrder = new ArrayList<>(solvingOrder);
```

## List切片

注意切片是前闭后开

```java
List<Integer> subList = oneList.subList(2,oneList.size());
```

## List遍历

## Map复制

```java
HashMap<String, Integer> map2 = new HashMap<>(map1);
```

## Map的遍历

常用第一种方法

```java
private static volatile Hashtable<Integer, Channel> hm = new Hashtable<Integer, Channel>();
java.util.Iterator<Entry<Integer, Channel>> iter = hm.entrySet().iterator();

        while (iter.hasNext()) {    
            Map.Entry entry = (Map.Entry) iter.next();
            //获取key
            int key = (Integer) entry.getKey();
            //获取Value
            channel = (Channel) entry.getValue();
            System.out.println("key=" + key);

        }1.2.3.4.5.6.7.8.9.10.11.12.
```

常用第二种方法 性能好 简单

```java
for (Entry<String, Integer> entry : hmp.entrySet()) {
      System.err.println("人物hashKey = " + entry.getKey() + ", Value = " + entry.getValue());
 }
```

## Map的连接

 ```java
// 合并        
Map<String, String> combineResultMap = new HashMap<String, String>();        
combineResultMap.putAll(map1);        
combineResultMap.putAll(map2);
 ```

## 判断key是否在Map里

`map.containsKey()`

## Map的key不存在

返回`null`

## Map转List

```java
Map<String, String> map = new HashMap<>();
// Convert all Map keys to a List
List<String> result = new ArrayList(map.keySet());
// Convert all Map values to a List
List<String> result2 = new ArrayList(map.values());
// Java 8, Convert all Map keys to a List
List<String> result3 = map.keySet().stream()
	.collect(Collectors.toList());
// Java 8, Convert all Map values  to a List
List<String> result4 = map.values().stream()
	.collect(Collectors.toList());
// Java 8, seem a bit long, but you can enjoy the Stream features like filter and etc.
List<String> result5 = map.values().stream()
	.filter(x -> !"apple".equalsIgnoreCase(x))
	.collect(Collectors.toList());
// Java 8, split a map into 2 List, it works!
// refer example 3 below
```

## List的连接

```java
        // First ArrayList
				ArrayList<String> arraylist1=new ArrayList<String>();
        //Second ArrayList
        ArrayList<String> arraylist2=new ArrayList<String>();
        arraylist1.addAll(arraylist2);
```

## String分割

String 类的 split() 方法可以按指定的分割符对目标字符串进行分割，**返回一个字符串数组**。该方法主要有如下两种重载形式：

```java
str.split(String sign)
str.split(String sign,int limit)
```


其中，str 为需要分割的目标字符串；sign 为指定的分割符，可以是任意字符串；limit 表示分割后生成的字符串的限制个数，如果不指定，则表示不限制，直到将整个目标字符串完全分割为止。

## String切片

Java中的String类提供了一个substring(int from, int to)方法，前闭后开同时to是可以省略的（多态），to缺省的情况下为截取到字符串的最后一位。

```java
String str = "i like yanggb";
System.out.println(str.substring(str.length() - 6)); // yanggb 截取后六位
```

## Srting复制然后连接

```java
//方法1
String.format("%0" + n + "d", 0).replace("0",s);
//方法2
String.join("", Collections.nCopies(50, "*")
```

## 获取某一变量的数据类型

### 引用数据类型：

​	使用反射的方法： `变量名.getClass().getSimpleName()`来判断。

​	使用 instanceof 来判断：`变量名 instanceof 类型`来判断。

### 基本数据类型：

​		使用 instanceof 来判断：`变量名 instanceof 类型`来判断。

- [ ] ## java里返回多个值

- [ ] ## Map与HashMap的区别

- [ ] ## int数组与Integer数组的区别

- [ ] ## Comparator

- [ ] ## 关于BiFunction的泛型：传一个数，再穿一个数，返回一个值，再把返回值作为第一个数   

  <img src="/Users/eleme/Library/Application Support/typora-user-images/image-20210727171744650.png" alt="image-20210727171744650" style="zoom:33%;" />

- [ ] ## BinaryOperator是个啥

- [ ] ComparisonChain

- [ ] idea 导入依赖之后必须要重启

- [ ] 子类父类转换

# 基本类型转换

基本类型：int double String

## String->int

`Integer.parseInt(String)`方法

​	接收第一位可以是正负号的数字字符串，返回一个int变量

`Integer.valueOf(String)`方法。

​	接收第一位可以是正负号的数字字符串，返回一个Integer变量

## Int->String

`int + ""`

## String->long

```java
long minNum2 = Long.parseLong(aStr.split("/")[0]);
```

跟int类似

## List->[]

List转换成数组，可以使用List的`toArray()`或者`toArray(T[] a)`方法。

```java
List<Integer> res = new ArrayList<>();
res.toArray(new Integer[0]);
```



数组转换成List，可以使用`Arrays.asList()`或者`Collections.addAll()`方法。

# 常用类

## Arrays工具类

java.util.Arrays类即为操作数组的工具类，包含了用来操作数组（比如排序和搜索）的各种方法。

1 **boolean equals(int[] a,int[] b)** 判断两个数组是否相等。

2 **String toString(int[] a)** 输出数组信息。

3 **void fill(int[] a,int val)** 将指定值填充到数组之中。

4 **void sort(int[] a)** 对数组进行排序。

5 **int binarySearch(int[] a,int key)** 对排序后的数组进行二分法检索指定的值

## String

1. 被final修饰的一个类 不能再被继承

2. 是支持序列化的（支持网络传输）

3. 底层存储是用的char数组

4. 是一个常量 创建之后不能修改  

5. 不需要new 可以直接赋值 有点像基本数据类型 但是不是 是字面量

6. 具体字符串储存在方法区的字符串常量池，字符串常量池中不会储存相同的字符串

   ## String常用方法

   ## String与基本数据类型的转换

   ## String与char数组的转换

   ## StringBuffer

## 比较器

### **自然排序：**java.lang.Comparable：

实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过 compareTo(Object obj) 方法的返回值来比较大小。如果当前对象this大 于形参对象obj，则返回正整数，如果当前对象this小于形参对象obj，则返回负整数，如果当前对象this等于形参对象obj，则返回零。

实现Comparable接口的对象列表（和数组）可以通过 Collections.sort 或Arrays.sort进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的元素，无需指定比较器。

### 定制排序：java.util.Comparator

当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，或者实现了java.lang.Comparable接口的排序规则不适合当前的操作，那么可以考虑使用** Comparator 的对象来排序，强行对多个对象进行整体排序的比较

<img src="/Users/eleme/Library/Application Support/typora-user-images/image-20210712142131087.png" alt="image-20210712142131087" style="zoom:25%;" />

## Systems类

## Math类

## 枚举类

类中对象的个数是确定的

## 元注解

对现有的注解的进行解释的注解 Retention与Target

## lombok

待解决

# 集合 	

Jav a 集合类可以用于存储数量不等的多个对象，还可用于保存具有映射关系的关联数组， **Java 集合：Collection 和 Map**

## **Collection**接口：

单列数据，定义了存取一组对象的方法的集合

### **List（动态数组）**：元素有序、可重复的集合

1. 创建一个List

   ```java
   List<Integer> tempList = Arrays.asList(1,0,3,2,4,5);
   List<Integer> greedyOrderAssignOrder = new ArrayList<Integer>(tempList);
   ```

2. python中的`list.append与list.extend`对比java中的`list.add与list.addAll`

### **Set（高中的集合）**：元素无序、不可重复的集合

<img src="/Users/eleme/Library/Application Support/typora-user-images/image-20210712152414589.png" alt="image-20210712152414589" style="zoom:25%;" />

## Iterator迭代器接口

提供一种方法访问一个容器(container)对象中各个元素，而又不需暴露该对象的内部细节。**迭代器模式，就是为容器而生。**类似于“公

交车上的售票员”、“火车上的乘务员”、“空姐”。 **现在不咋用**

```java
boolean hasHex()
Returns true if the iteration has more elements
next()
Returns the next element in the iteration
void remove()
Removes from the underlying collection the last element returned by the iterator (optional operation).
```



## **Map**接口：

双列数据，保存具有映射关系“key-value对”的集合

<img src="/Users/eleme/Library/Application Support/typora-user-images/image-20210712152335180.png" alt="image-20210712152335180" style="zoom:25%;" />



## List排序

```java
List<Integer> oneList = Arrays.asList(1, 6, 3,9,7);
Collections.sort(oneList);
```

改变list本身 无返回值

## 常用方法

```java
// 因为Collections是抽象类 所以声明可以用Collections new要使用实现类 ArrayList
Collections coll = new ArrayList()
coll.add(Object e ) //不仅可以添加元素 还可以添加另一个Collections 相当于python的list.append()
coll.addAll() // 相当于python的list.expend()
coll.size()
coll.isEmpty()
coll.clear()
coll.removerif(i -> i.equal())

```



## Pair

1. List<Pair<>>和Map<>才是类似的东西。 前者可以用for(int i =0; i<xx.length; i++)这样遍历，后者我只能用for(元素 x :map名称)遍历
2. List<Pair<K,V>>和Map<K,V>最本质的区别无非是Map一个Key对应一个Value，而List<Pair>没有这个限制。比如我先添加(1, {a:1} )，再添加（1, {a:2} ），那么List<Pair>会保留两个值，而Map则是后面的值替换掉前面的值。
3. 综上所述，由于Map中使用Entry来存放Key和Value，又由于Map使用EntrySet来提供对外接口，导致直接对Map中的Value进行排序不方便。因此你看到有人直接使用List来存储Pair<Key,Value>，这样的话对Value进行排序就很方便了。

## 待编辑

# 泛型

 所谓泛型，就是允许在定义类、接口时通过一个标识表示类中某个属性的类 型或者是某个方法的返回值及参数类型。这个类型参数将在使用时（例如， 继承或实现这个接口，用这个类型声明变量、创建对象时）确定（即传入实 际的类型参数，也称为类型实参）。

## java泛型中`<T>`和`<?>`区别

**T 代表一种类型，?是通配符,泛指所有类型**

# Serializable

Serializable是java.io包中定义的、用于实现Java类的序列化操作而提供的一个语义级别的接口。https://developer.51cto.com/art/201905/596334.htm

Serializable序列化接口没有任何方法或者字段，只是用于标识可序列化的语义。**实现了Serializable接口的类可以被ObjectOutputStream转换为字节流，同时也可以通过ObjectInputStream再将其解析为对象。**

而这一点对于面向对象的编程语言来说是非常重要的，因为**无论什么编程语言，其底层涉及IO操作的部分还是由操作系统其帮其完成的，而底层IO操作都是以字节流的方式进行的，所以写操作都涉及将编程语言数据类型转换为字节流，而读操作则又涉及将字节流转化为编程语言类型的特定数据类型。**而Java作为一门面向对象的编程语言，对象作为其主要数据的类型载体，为了完成对象数据的读写操作，也就需要一种方式来让JVM知道在进行IO操作时如何将对象数据转换为字节流，以及如何将字节流数据转换为特定的对象，而Serializable接口就承担了这样一个角色。

# Optional

Optional 类是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。

**Optional 是个容器：它可以保存类型T的值，或者仅仅保存null。**Optional提供很多有用的方法，这样我们就不用显式进行空值检测。

Optional 类的引入很好的解决空指针异常。

# 匿名内部类

```java
interface A{
	public abstract void fun1();
}
public class Outer{
  public static void main(String[] args) {
    new Outer().callInner(new A(){
      //接口是不能new但此处比较特殊是子类对象实现接口，只不过没有为对象取名
      public void fun1() {
      System.out.println(“implement for fun1");
      }
    });// 两步写成一步了
    }
    public void callInner(A a) {
    a.fun1();
  }
}
```

# lambda表达式

Lambda 是一个**匿名函数**，我们可以把 Lambda 表达式理解为是**一段可以**传递的代码（将代码像数据一样进行传递）。使用它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使Java的语言表达能力得到了提升。

**lambda表达式的本质：函数式接口的一个实例**    

`->`lambda表达式

## 注意事项

lambda表达式里面用不了全局变量

`::`方法引用

## 函数式接口

只包含一个抽象方法的接口，称为**函数式接口**。

## 方法引用

方法引用可以看做是Lambda表达式深层次的表达。换句话说，方法引用就是Lambda表达式，也就是函数式接口的一个实例，通过方法的名字来指向一个方法，可以认为是Lambda表达式的一个语法糖。

# StreamAPI

Stream 是 Java8 中处理集合的关键抽象概念，它可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。 使用Stream API 对集合数据进行操作，就类似于使用 SQL 执行的数据库查询。也可以使用 Stream API 来并行执行操作。**简言之，Stream API 提供了一种高效且易于使用的处理数据的方式。**

## Predicate p

输入一个变量 返回一个布尔值

## 创建

1. 通过集合创建
   1. `集合.stream()`
   2.  **如何通过map创建stream：不能直接创建**
      1. someMap.value().stream()
2. 通过数组创建
   1. `Arrays.stream(数组)`
3. 通过Stream.of()
   1. `Stream.of(1,2,3,4)`
4. 创建无限流 一般用来造数据
   1. 前十个偶数`Stream,iterate(0, t -> t+2).limit(10).forEach(System.out :: println)`
   2. 前十个随机数`Stream.generate(Math :: random).limit(10).forEach(System.out :: println)`

## 中间操作

1. 筛选与切片

   1. **filter(Predicate p)** 接收 Lambda ， 从流中排除某些元素
   2. **distinct()** 筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素
   3. **limit(long maxSize)** 截断流，使其元素不超过给定数量
   4. **skip(long n)**跳过元素，返回一个扔掉了前 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补

2. 映射

   1. **map(Function f)**接收一个函数作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素。
   2. **mapToDouble(ToDoubleFunction f)** 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 DoubleStream。
   3. **mapToInt(ToIntFunction f)** 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 IntStream。
   4. **mapToLong(ToLongFunction f)** 接收一个函数作为参数，该函数会被应用到每个元素上，产生一个新的 LongStream。
   5. **flatMap(Function f)** 接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流 **可以理解为stream的数组**

3. 排序

   **sorted()** 产生一个新流，其中按自然顺序排序

   **sorted(Comparator com)** 产生一个新流，其中按比较器顺序排序 排序是默认升序

   ```
   // 员工先按照年龄 后按照工资排序
   List<Employee> employees = EmployeeData.getEmployees();
   employees.stream().sorted( (e1,e2) -> {
      int ageValue = Integer.compare(e1.getAge(),e2.getAge());
      if(ageValue != 0){
          return ageValue;
      }else{
          return -Double.compare(e1.getSalary(),e2.getSalary());
      }
   }).forEach(System.out::println);
   ```

## 终止操作

1. 匹配与查找

   1. **allMatch(Predicate p)** 检查是否匹配所有元素 **返回布尔型变量**
   2. **anyMatch**(**Predicate p**) 检查是否至少匹配一个元素 **返回布尔型变量**
   3. **noneMatch(Predicate p)** 检查是否没有匹配所有元素 **返回布尔型变量**
   4. **findFirst()** 返回第一个元素 **返回Optionnal类型**
   5. **findAny()** 返回当前流中的任意元素
   6. **count()** 返回流中元素总数
   7. **max(Comparator c)** 返回流中最大值
   8. **min(Comparator c)** 返回流中最小值
   9. **forEach(Consumer c)** 内部迭代(使用 Collection 接口需要用户去做迭代，称为外部迭代。相反，Stream API 使用内部迭代——它帮你把迭代做了)

2. 规约 比如说求和

   1. **reduce(T identity, BinaryOperator b)** 可以将流中元素反复结合起来，得到一个值。返回 T
   2. **reduce(BinaryOperator b)** 可以将流中元素反复结合起来，得到一个值。返回 Optional<T>

3. 收集

   1. **collect(Collector c)** 将流转换为其他形式。接收一个 Collector接口的实现，用于给Stream中元素做汇总的方法

      ```java
      List<Employee> employees = EmployeeData.getEmployees();
      List<Employee> employeeList = employees.stream().filter(e -> e.getSalary() > 6000).collect(Collectors.toList());
      ```

   2. Collector 接口中方法的实现决定了如何对流执行收集的操作(如收集到 List、Set、Map)。另外， Collectors 实用类提供了很多静态方法，可以方便地创建常见收集器实例，



# ComparisonChain

 翻开ComparisonChain类的源码，我们发现，它其实是一个抽象类，其提供了主要有三个抽象方法，start()用于返回内部的一个 ComparisonChain实现；重载了许多compare()方法，用收各种类型的参数，**compare方法返回的仍然是 ComparisonChain对象；**result()方法用于返回比较后的结果。

总结：通过对ComparisonChain的学习，以及前面[Guava中Obejects实用工具类的学习](http://www.xx566.com/detail/128.html)等，我们发现，Guava中大量存在这种类似的链式编码，熟悉设计模式的不难理解，**这正是Builder建造者模式的应用。**

# 反射

## 反射的作用

- 在运行时判断任意一个对象所属的类
- 在运行时构造任意一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时获取泛型信息
- 在运行时调用任意一个对象的成员变量和方法
- 在运行时处理注解
- 生成动态代理

## 反射几个问题

1. 什么时候用反射：需要动态性的时候
2. 反射与封装性的矛盾：不矛盾，只是能调用封装的属性方法。

# Maven

用于**项目构建**和**依赖管理**，构建就是以我们编写的 Java 代码、框架配置文件、国际化等其他资源文件、JSP 页

面和图片等静态资源作为“原材料”，去“生产”出一个可以运行的项目的过程。

## 常见Maven命令

# Spring

# Junit

一般在test里面

## 关键字

@Test

assertion

@BeforeEach @AfterEach @BeforeAll @AfterAll

# git

## stash与pop

其实如果我们不想提交完成一半或者不完善的代码，但是却不得不去修改一个紧急Bug，那么使用`git stash`就可以将你当前未提交到本地（和服务器）的代码推入到Git的栈中，这时候你的工作区间和上一次提交的内容是完全一样的，所以你可以放心的修Bug，等到修完Bug，提交到服务器上后，再使用`git stash apply`将以前一半的工作应用回来。

### 命令：

1. `git stash`
2. `git stash pop`命令恢复之前缓存的工作目录, 这个指令将缓存堆栈中的第一个stash删除，并将对应修改应用到当前的工作目录下。你也可以使用`git stash apply`命令，将缓存堆栈中的stash多次应用到工作目录中，但并不删除stash拷贝。

# IDEA

## [启动太慢](https://zhuanlan.zhihu.com/p/268033408#:~:text=IDEA%E9%BB%98%E8%AE%A4%E5%90%AF%E5%8A%A8%E9%85%8D%E7%BD%AE%E4%B8%BB%E8%A6%81%E8%80%83%E8%99%91%E4%BD%8E%E9%85%8D%E7%BD%AE%E7%94%A8%E6%88%B7%EF%BC%8C%E5%8F%82%E6%95%B0%E4%B8%8D%E9%AB%98%EF%BC%88%E9%BB%98%E8%AE%A4%E6%9C%80%E4%BD%8E128m%EF%BC%8C%E6%9C%80%E9%AB%98512m%EF%BC%89%EF%BC%8C%E5%AF%BC%E8%87%B4%E5%90%AF%E5%8A%A8%E6%85%A2%EF%BC%8C%E7%84%B6%E5%90%8E%E8%BF%90%E8%A1%8C%E4%B9%9F%E4%B8%8D%E6%B5%81%E7%95%85%EF%BC%8C%E8%BF%99%E9%87%8C%E6%88%91%E4%BB%AC%E9%9C%80%E8%A6%81%E4%BC%98%E5%8C%96%E4%B8%8B%E5%90%AF%E5%8A%A8%E5%92%8C%E8%BF%90%E8%A1%8C%E9%85%8D%E7%BD%AE%EF%BC%9B%E4%BD%86%E6%98%AF%E5%9C%A8%E5%B7%A5%E4%BD%9C%E4%B8%AD%E7%9A%84%E7%94%B5%E8%84%91%E4%B8%80%E8%88%AC%E9%83%BD%E6%98%AF8G%E6%88%96%E8%80%8516G%E7%9A%84%E8%BF%90%E8%A1%8C%E5%86%85%E5%AD%98%EF%BC%8C%E6%89%80%E4%BB%A5%E6%88%91%E4%BB%AC%E9%9C%80%E8%A6%81%E6%89%8B%E5%8A%A8%E5%8E%BB%E4%BF%AE%E6%94%B9%E9%BB%98%E8%AE%A4%E7%9A%84IDEA%E9%85%8D%E7%BD%AE%E3%80%82%20%E5%9C%A8%20Settings%20-%3E%20Appearance%20%26%20Behavior,%E8%AE%BE%E7%BD%AE%E7%AA%97%E5%8F%A3%E4%B8%AD%EF%BC%8C%E5%8B%BE%E9%80%89%20Show%20memory%20indicator%20%E9%80%89%E9%A1%B9%EF%BC%8C%E7%84%B6%E5%90%8E%E4%B8%BB%E7%95%8C%E9%9D%A2%E5%8F%B3%E4%B8%8B%E8%A7%92%E4%BC%9A%E6%98%BE%E7%A4%BA%20Heap%20%E6%80%BB%E5%A4%A7%E5%B0%8F%E4%BB%A5%E5%8F%8A%E4%BD%BF%E7%94%A8%E7%8A%B6%E5%86%B5%E4%BA%86%E3%80%82)

## Introduce local variable

Option + Command + V 或者 option + enter +enter

## 相对路径

对于maven下面test的文件，相对路径到模块：到`dispatch-decision`

```
/Users/eleme/IdeaProjects/dispatch-solver/dispatch-decision/src/test/resources/expdata/4/4_2.json
```



# 问题

- [x] 数组初始化写法：见集合->list

- [ ] for循环的写法

- [x] 递增list写法 courierLabel = Stream.iterate(0, item -> item+1).limit(courierSize).collect(Collectors.toList());

- [ ] java 继承接口的类可以实现非接口的方法吗：
- [ ] java操作csv文件
