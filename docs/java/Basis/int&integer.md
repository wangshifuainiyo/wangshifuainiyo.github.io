- [1 int与Integer的基本使用对比](#1-int%e4%b8%8einteger%e7%9a%84%e5%9f%ba%e6%9c%ac%e4%bd%bf%e7%94%a8%e5%af%b9%e6%af%94)
- [2 int与Integer的深入对比](#2-int%e4%b8%8einteger%e7%9a%84%e6%b7%b1%e5%85%a5%e5%af%b9%e6%af%94)
- [Java两种数据类型](#java%e4%b8%a4%e7%a7%8d%e6%95%b0%e6%8d%ae%e7%b1%bb%e5%9e%8b)
    - [Java两种数据类型分类](#java%e4%b8%a4%e7%a7%8d%e6%95%b0%e6%8d%ae%e7%b1%bb%e5%9e%8b%e5%88%86%e7%b1%bb)
    - [Java为每个原始类型提供了封装类](#java%e4%b8%ba%e6%af%8f%e4%b8%aa%e5%8e%9f%e5%a7%8b%e7%b1%bb%e5%9e%8b%e6%8f%90%e4%be%9b%e4%ba%86%e5%b0%81%e8%a3%85%e7%b1%bb)
- [基本解析](#%e5%9f%ba%e6%9c%ac%e8%a7%a3%e6%9e%90)
    - [自动装箱：将基本数据类型重新转化为对象](#%e8%87%aa%e5%8a%a8%e8%a3%85%e7%ae%b1%e5%b0%86%e5%9f%ba%e6%9c%ac%e6%95%b0%e6%8d%ae%e7%b1%bb%e5%9e%8b%e9%87%8d%e6%96%b0%e8%bd%ac%e5%8c%96%e4%b8%ba%e5%af%b9%e8%b1%a1)
    - [自动拆箱：将对象重新转化为基本数据类型](#%e8%87%aa%e5%8a%a8%e6%8b%86%e7%ae%b1%e5%b0%86%e5%af%b9%e8%b1%a1%e9%87%8d%e6%96%b0%e8%bd%ac%e5%8c%96%e4%b8%ba%e5%9f%ba%e6%9c%ac%e6%95%b0%e6%8d%ae%e7%b1%bb%e5%9e%8b)

## 1 int与Integer的基本使用对比
* Integer是int的包装类；int是基本数据类型； 
* Integer变量必须实例化后才能使用；int变量不需要； 
* Integer实际是对象的引用，指向此new的Integer对象；int是直接存储数据值 ； 
* Integer的默认值是null；int的默认值是0。

## 2 int与Integer的深入对比
* 由于Integer变量实际上是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）。

```java
Integer i = new Integer(100);
Integer j = new Integer(100);
System.out.print(i == j); //false
```
* Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）

```java
Integer i = new Integer(100);
int j = 100；
System.out.print(i == j); //true
```
 

* 非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。（因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同）

```java
Integer i = new Integer(100);
Integer j = 100;
System.out.print(i == j); //false
```

* 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

```java

Integer i = 100;
Integer j = 100;
System.out.print(i == j); //true

Integer i = 128;
Integer j = 128;
System.out.print(i == j); //false
```

 

　　对于第4条的原因： java在编译Integer i = 100 ;时，会翻译成为Integer i = Integer.valueOf(100)。而java API中对Integer类型的valueOf的定义如下，对于-128到127之间的数，会进行缓存，Integer i = 127时，会将127进行缓存，下次再写Integer j = 127时，就会直接从缓存中取，就不会new了。


```java
public static Integer valueOf(int i){
    assert IntegerCache.high >= 127;
    if (i >= IntegerCache.low && i <= IntegerCache.high){
        return IntegerCache.cache[i + (-IntegerCache.low)];
    }
    return new Integer(i);
}
```

## Java两种数据类型
#### Java两种数据类型分类
> 1.基本数据类型，分为boolean、byte、int、char、long、short、double、float；   
> 2.引用数据类型 ，分为数组、类、接口。

#### Java为每个原始类型提供了封装类
　　为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作，Java为每 一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换。

>1.基本数据类型: boolean，char，byte，short，int，long，float，double  
>2.封装类类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double
## 基本解析
#### 自动装箱：将基本数据类型重新转化为对象

```java
 public class Test {  
        public static void main(String[] args) {  
            //声明一个Integer对象
            Integer num = 9;

            //以上的声明就是用到了自动的装箱：解析为:Integer num = new Integer(9);
        }  
    }  
```

 

　　9是属于基本数据类型的，原则上它是不能直接赋值给一个对象Integer的，但jdk1.5后你就可以进行这样的声明。自动将基本数据类型转化为对应的封装类型，成为一个对象以后就可以调用对象所声明的所有的方法。

#### 自动拆箱：将对象重新转化为基本数据类型

```java
public class Test {  
        public static void main(String[] args) {  
            //声明一个Integer对象
            Integer num = 9;

            //进行计算时隐含的有自动拆箱
            System.out.print(num--);
        }  
    }  
```

 

　　因为对象时不能直接进行运算的，而是要转化为基本数据类型后才能进行加减乘除。对比：

```java
/装箱
Integer num = 10;
//拆箱
int num1 = num;
```