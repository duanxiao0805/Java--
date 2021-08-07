## main方法的理解

**一直写public static void main(String[] args){ } 这个main方法,用Java虚拟机解释一下**

需要调用类的main()方法,那么该方法的访问权限就是public了

在执行main方法时不必创建对象,所以该方法必须是static

该方法接受String类型的数组参数,该数组中保存执行Java命令时传递给所运行的类的参数

Java执行的程序--->参数1,参数2,参数3......





**到底是谁在调用main方法?**

其实是Java虚拟机调用的,调用的时候根本不在同一个类,那么必须是public



在main方法中,可以直接调用main方法所在的静态方法或静态属性

但是,不能直接访问该类中的非静态变量成员,必须创建该类的一个实例对象后,才能通过这个对象去访问类中的静态成员

```java
public class test3 {
    // 静态成员
    public static int a = 10;
    // 非静态成员
    public int b = 100;

    public static void main(String[] args) {
        f2();
        test3 t3 = new test3();
        t3.f1();
        int a1 = a;
        int b1 = t3.b;
    }

    // 非静态方法
    public void f1() {

    }

    // 静态方法
    public static void f2() {

    }
}
```



