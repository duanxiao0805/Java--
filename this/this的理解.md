## this的理解

```java
class test {
    public static void main(String[] args) {
        thisTest test = new thisTest(1);
        test.test(2);
        System.out.println(test.a);
    }
}

class thisTest {
    
    int a;
    
    public thisTest(int a) {
        this.a = a;
    }

    public void test(int a) {
        a = a;
    }
}

```

![this1](D:\Java学习\Java\this\this1.PNG)

啊...并不会啊

所以这个方法中的a并不会去执行赋值



**为什么?**

如果加上this.a=a;呢

这个方法的a只是在这个作用域之内有效,如果加上this,这个this就代表当前对象这个整体,然后this.a可以理解为这个对象调用的属性a--->即上面的int a



**图解一下吧**





其实这个this是对象自带隐藏的一个属性,它指向的地址就是这个对象本身,所以这个this不能置空,因为它保证是自己存在的





this访问构造器的时候只需要--->**this(参数列表)**即可     只能在构造器中使用

```java
class thisTest {
    public thisTest(int a) {
        this.a = a;
    }

    public thisTest() {
        this(3);
    }
}
```

这样是可以的,如果你把this(3)拿出来,就会报错

