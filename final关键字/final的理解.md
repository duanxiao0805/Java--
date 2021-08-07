## final

类,属性,方法和局部变量都可以修饰

**类--->可以保证不被继承**

```java
final class A {

}

class B extends A{

}
//这样B是不可以继承A的
```



**方法--->不被重写**

```java
class C {
    final public void f() {

    }
}

class D extends C {
    @Override
    public void f() {
    }
}
//这个方法f()是不可以重写的
```



**属性--->不被修改**

一个意思

**局部变量--->不被修改**

一个意思







### 有几个细节和规则:

修饰的属性名一般用xx_xx_xx命名

修饰属性的时候,必须赋初值,并且以后就不能被修改了

1.定义时的初值

2.构造器中的初值

3.代码块中

但是如果final修饰的属性是静态的,则初始化的位置只能是定义的时候和静态代码块中,就不能构造器里赋值了

为什么呢,因为上面的属性值不能再修改了,你在构造器里再进行初始化,就不行了!!!

```java
class E {
    public final double A = 0.01;
    
    // 这里先不赋初值
    public final double B;
    public final double C;
    // 构造器里赋初值
    
    public E() {
        B = 0.02;
    }
    
    // 在代码块里赋初值
    {
        C = 0.03;
    }
}

//关于静态呢?
class F {
    public static final double A = 0.01;

    public static final double B;
    public static final double C;

    static {
        B = 0.02;
    }

    // 构造器里能不能给初值???
    public F() {
        c = 0.03;
    }
    
}
```

**关于为什么不能在构造器里赋值,本质问题是什么?**

其实就是,这个static是在类加载的时候就要赋初值,这个时候构造器在干嘛?还没出现呢,因为构造器只能是对象创建好的时候才会触发!!!!!!!!!





如果这个类已经是final类了,就没必要再将方法修饰成final方法

final方法不能修饰构造方法

final和static搭配效率更高,底层编译器做了优化处理

final类--->Integer,Double,Float,Boolean,String都是