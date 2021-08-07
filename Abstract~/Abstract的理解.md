## Abstarct的理解

当父类的一些方法不能确定时,可以用abstract关键字来修饰该方法,这个方法就是抽象方法,用abstract来修饰该类就是抽象类



```java
abstract class A{
    
    abstract public void f();
    //不写具体的实现方法
}
class B extends A{
    
}
```

就是可以想成一个框架呗,后面设计会用到

抽象类不能被实例化--->不能创建对象

抽象类不一定包含抽象方法,也就是说抽象类可以没有abstract方法

但是如果有抽象方法的话,这个类必须声明为抽象类

抽象类除了抽象方法没有方法体,跟普通类没什么区别

**关于继承的使用?**

如果一个类继承了抽象类,则它必须实现抽象类所有的抽象方法,除非它自己也声明为abstract!





**!!!**

```java
abstract final class A{}
```

这个是不能编译通过的,这两个修饰的不能共存,因为final修饰的类不能被继承,但是abstract修饰的类可以被继承--->产生了矛盾

```java
abstract public static void test();
```

abstract和static也不能同时存在,因为abstract方法需要子类的重写,但是static允许重写,那么这个就矛盾了!

```java
public private ......?
```

private更不可能了,后面都没机会继承了

### 模板设计模式

多个类,完成不同的任务job

要求能够得到各自完成任务的时间

```java
abstract class Template {
    public abstract void job();
    public void Time() {
        long start = System.currentTimeMillis();
        job();
        long end = System.currentTimeMillis();
        System.out.println("执行时间" + (end - start));
    }
}
class H extends Template {
    public void job() {
        long num = 0;
        for (long i = 1; i <= 8000000; i++) {
            num += i;
        }

    }
}
class test {
    public static void main(String[] args) {
        Template h = new H();
        h.Time();
    }
}
```

其实就是利用了一个向上转型调用重写方法而已,因为抽象类也是相当于一个父类而已~



