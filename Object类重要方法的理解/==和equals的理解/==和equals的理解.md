## ==

既可以判断基本类型,有课呀判断引用类型

基本类型--->判断值是否相等

引用类型--->判断地址是否相等,因为指向的对象是地址,所以能判断是否是同一个对象





**举个例子+图解一下**

```java
class A {
    
}
class test {
   public static void main(String[] args){
       A a=new A();
       A b=a;
       A c=b;
   }
}
```

**先图解对象a,b,c的内存存在形式**

![==](D:\Java学习\Java\==和equals的理解\==.PNG)

a指向的地址和b,c指向的地址相同,那么他们就是同一个对象

验证一下 **==** 运算符

```java
class test {
   public static void main(String[] args){
       A a=new A();
       A b=a;
       A c=b;
       boolean bool1=a==b;
       boolean bool2=a==c;
       boolean bool3=b==c;
   }
}
```

看了程序运行结果都是true,所以这样验证是成功的

这个时候想到的是,这都是同一个类啊,如果类不同的话,指向的是同一地址可不可以说明是统一对象呢?

```java
B b=a;
```

这个就跟前面联系起来了,虽然是B编译类型,但是它的运行类型是a,也就是说它指向的内存是a对象,所以还是同一个地址--->true

**当然要保证B继承A!**





## equals

equals:是Object类中的方法,只能判断引用类型



### 子类重写equals

equals 本质上就是 ==，只不过 String 和 Integer 等重写了 equals 方法，把它变成了值比较。

```java
Integer integer1=new Integer(1000);
Integer integer2=new Integer(1000);

boolean b1=integer1==integer2;
boolean b2=integer1.equals(integer2);
```

这里的b1是false

引用类型,因为1和2的内存肯定不一样--->对象也就不一样了,==比较的是地址

而值比较却是相等的

String类型也同理