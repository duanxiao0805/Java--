## Object里的hashCode

有两个引用如果是同一个对象,哈希值相同,不是同一对象,哈希值不同

哈希值是根据地址计算出来的,但是它不等价于地址,用来判断地址就好

```java
        AA aa1 = new AA();
        AA aa2 = new AA();
        AA aa3 = aa1;
        System.out.println(aa1.hashCode());
        System.out.println(aa2.hashCode());
        System.out.println(aa3.hashCode());
```

这里的aa1和aa2就不是同一个对象,也就是地址不同--->hashCode不相等

aa1和aa3指向的地址相同--->hashCode相等

