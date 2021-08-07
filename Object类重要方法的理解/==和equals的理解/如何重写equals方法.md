## 如何重写equals方法?

因为这个equals除了String和Integer类型的,都是比较地址,没法比较具体的内容啊

所以有一个类创建好的对象,对他们进行内容比较没法保证是正确的

equals属于Object类的方法,那么所有的类都可以重写!

```java
class Person {
    private String name;
    private int age;
    private char gender;

    public Person(String name, int age, char gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
    }

    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        // 类型判断
        if (obj instanceof Person) {
            Person p = (Person) obj;
            return this.name.equals(p.name) && this.age == p.age && this.gender == p.gender;
        }
        return false;
    }
}

public class test {
    public static void main(String[] args) {
        Person p1 = new Person("duanxiao1", 18, 'a');
        Person p2 = new Person("duanxiao1", 18, 'a');
        boolean bool = p1.equals(p2);
        System.out.println(bool); // false
        // equals是Object中的方法,默认是比较p1,p2的地址是否相等
        // 显然里面无论是什么内容,只要对象不同(也就是地址不同),肯定是fasle
        // 所以这个时候可以把equals重写一下~

    }
}
```

