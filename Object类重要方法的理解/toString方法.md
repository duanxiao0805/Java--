## toString方法

### 重写toString

因为toString是Object中的方法,所以所有的类都可以继承--->那么所有的类都可以对它进行重写!!!

重写用来输出对象的属性



1. **必须被声明为public**
2. **返回类型为String**
3. **方法的名称必须为toString,且无参数**
4. **方法体中不要使用输出方法System.out.println()**