## Java语言的IO流

借助输入输出包Java.io来实现

### 流的概念

数据的传输方向:输入流与输出流

流的内容:字节流与字符流

**输入流?**只能读取数据不能写入数据

**输出流?**只能写入数据不能读取数据

**字节流?**处理的是数据单元是8位的字节

**字符流?**处理的是数据单元是16位字符

### 输入输出流类库

java.io包中有四个基本类:InputStream、OutputStream、Reader及Writer类

字节流:InputStream OutputStream

字符流:Reader Writer

这些都是抽象类,所以使用的时候并不会直接使用这些类,而是用他们的子类对文件处理

#### InputStream和OutputStream流类

这些都是用来处理以位(bit)为单位的流--->二进制文件、文本文件都可以

**!!**但是如果文本文件中出现中文,则会出现乱码的状态,操作Unicode字符可以选择字符流操作~

都是抽象类,具体应用根据子类和具体情况



#### 输入输出流的应用

##### 文件输入输出流

FileInputStream和FileOutputStream分别是InputStream和OutputStream的直接子类,负责完成对本地磁盘文件的顺序输入与输出操作的流

input表示一个文件字节输入流,从中可读取一个字节或一批字节--->理解为我写入的数据

output表示一个文件字节输出流,写入一个字节或一批字节--->理解为目标文件,把数据输出到文件中

**我理解一下这段程序~**

```java
package Main;

import java.io.*;

class App10_1 {
    public static void main(String[] args) throws IOException {
        char ch;
        int data;
        try (
                FileInputStream fin = new FileInputStream(FileDescriptor.in);
                FileOutputStream fout = new FileOutputStream("D:/Study/test.txt");
        // 后面是写入的文件地址
        ) {
            System.out.println("请输入一串字符串,并以#结束:");
            while ((ch = (char) fin.read()) != '#')
                fout.write(ch);
            // 这个理解为写入的字符
        } catch (FileNotFoundException e) {
            System.out.println("文件没找到!");
        } catch (IOException e) {
        }
        try (
                FileInputStream fin = new FileInputStream("D:/Study/test.txt");
                FileOutputStream fout = new FileOutputStream(FileDescriptor.out);) {
            while (fin.available() > 0) {
                data = fin.read();
                fout.write(data);
            }
        } catch (IOException e) {
        }
    }

}
```

fin和fout分别是文件输入流对象和文件输出流对象~ 也就是说fin对象用来获取用户键盘输入的数据,而fout对象用来把数据传进目标文件中

怎么实现的?  fin对象调用的read()方法依次读取数据,直到遇到'#'结束,然后fout对象调用write()方法,把数据写入目标文件中~

下面的就是相反了~从文件中输入,与上面从键盘中输入相反,然后输出到屏幕上

##### 顺序输入流



##### 管道输入输出流



##### 过滤输入输出流

FilterInputStream和FilterInputStream派生出数据输入流类DataInputStream和数据输出流类DataOutputStream等子类

作用可以这样理解--->二进制文件---FileInputStream(字节)---DataInputStream(int型数据)

**理解一下这段程序~:**

```java
package Main;

import java.io.*;

public class App10_3 {
    public static void main(String[] args) throws FileNotFoundException, IOException {
        try (
                FileOutputStream fout = new FileOutputStream("D:/Study/test.txt");
                DataOutputStream dout = new DataOutputStream(fout);) {
            dout.writeInt(10);
            dout.writeLong(12345);
            dout.writeFloat(3.141345f);
            dout.writeDouble(535345.123);
            dout.writeBoolean(true);
            dout.writeChars("Goodbye!");
        }
        try (
                FileInputStream fin = new FileInputStream("D:/Study/test.txt");
                DataInputStream din = new DataInputStream(fin);) {
            System.out.println(din.readInt());
            System.out.println(din.readLong());
            System.out.println(din.readFloat());
            System.out.println(din.readDouble());
            System.out.println(din.readBoolean());
            char ch;
            while ((ch = din.readChar()) != '\0')
                System.out.print(ch);
        }
    }
}
```

##### 标准输入输出流

这个就不是很复杂了,System.in是BufferedInputStream类的对象,需要从键盘读入数据时,只需要调用System.in的read()方法即可,这个有返回值?奇怪...返回值是字节单位~

System.out一样~

**高位字节和低位字节什么意思....?**

可以理解为按照权重划分的二进制,左边和右边分别代表高位和低位~

```java
package Main;

import java.io.*;

public class App10_4 {
    public static void main(String[] args) {
        try {
            byte[] b = new byte[128];
            System.out.print("请输入字符:");
            // read返回字节型,是字符的话也只能返回ASCII码
            int count = System.in.read(b);
            System.out.println("输入的是:");
            for (int i = 0; i < count; i++)
                System.out.print(b[i] + " ");
            System.out.println();
            for (int i = 0; i < count - 2; i++)
                System.out.print((char) b[i] + " ");
            System.out.println();
            System.out.println("输入的字符个数为" + count);
            Class inClass = System.in.getClass();
            Class outClass = System.out.getClass();
            System.out.println("in所在的类是:" + inClass.toString());
            System.out.println("out所在的类是:" + outClass.toString());
        } catch (IOException e) {
            // TODO: handle exception
        }
    }
}
```

#### 使用Reader和Writer流类

这两个输入输出流类对比前面的InputStream和OutputStream

前面的那个是处理字节数据的,也就是那些二进制数据,这个呢,就是处理字符数据的--->字符流~

同样,这都是抽象类,需要用它的子类创建对象

##### 使用FileReader类读取文件

```java
package Main;

import java.io.*;

public class App10_5 {
    public static void main(String[] args) throws IOException {
        char[] c = new char[500];
        try (FileReader fr = new FileReader("D:/Study/test.txt")) {
            int num = fr.read(c);
            String str = new String(c, 0, num);
            System.out.println("读取的字符个数为:" + num + ",其内容如下");
            System.out.println(str);
        }
    }
}
```

我在读取中文文本的时候,出现了乱码!!!

**怎么解决呢?**

原因肯定是乱码的问题

```java
InputStreamReader fr = new InputStreamReader(new FileInputStream("D:/Study/test.txt"), "UTF-8");
```

怎么理解这段代码...

过滤字节输入流--->字符输入流

过滤字节输入流的作用是干嘛的? 可以理解为去转换它的编码格式,然后再转换成字符输入流进行输入~

##### 使用FileWriter类写入文件

```java

```

##### 使用BufferedReader类读取文件

缓冲字符输入流类继承自Reader类,用来读取缓冲区里的数据

读取数据之前,必须先创建FileReader类对象,再用这个对象为参数创建BufferedReader类的对象

```java
package Main;

import java.io.*;

public class App10_7 {
    public static void main(String[] args) throws IOException {
        String thisLine;
        int count = 0;
        try (
                FileReader fr = new FileReader("D:/Study/test.txt");
                BufferedReader bfr = new BufferedReader(fr);) {
            while ((thisLine = bfr.readLine()) != null) {
                count++;
                System.out.println(thisLine);
            }
        } catch (IOException ioe) {
            System.out.println("错误!" + ioe);
        }
    }
}
```

这个呢,就是先创建的fr对象,再用这个对象为参数创建BufferedReader类的对象



#### 文件的管理与随机访问

计算机程序运行的时候,数据都保存在系统的内存中,由于关机时内存中的数据全部丢失,所以必须把那些需要长期保存的数据存放在磁盘文件里,需要时再从文件里读出

##### Java语言对文件与文件夹的管理

使用文件管理,需要使用File类管理磁盘文件和文件夹,不负责数据的输入输出,在io包中

File类对象表示一个磁盘文件或文件夹,对象属性包含了各种的相关信息~

**分析一下这段程序~**

```java
package Main;

import java.io.*;

public class App10_9 {
    public static void main(String[] args) throws IOException {
        String str = new String();
        try (
                InputStreamReader isr = new InputStreamReader(System.in);
                BufferedReader inp = new BufferedReader(isr);) {
            String sdir = "D:/Study";	//文件夹地址
            String sfile;
            File fdir1 = new File(sdir);	//创建文件夹对象,为了后面的操作
            if (fdir1.exists() && fdir1.isDirectory()) {
                System.out.println("文件夹:" + sdir + "已经存在");
                //下面这段代码,依次遍历这个文件夹的所有文件夹
                //也就是说,fdir1.list()里面存放的是本文件夹下的所有文件夹
                for (int i = 0; i < fdir1.list().length; i++)
                    System.out.println((fdir1.list())[i]);
                //创建文件夹对象,方便操作
                File fdir2 = new File("D:/Study/temp");
                //这个文件夹不存在,然后创建出来
                if (!fdir2.exists())
                    fdir2.mkdir();
                System.out.println();
                System.out.println("建立新文件后的文件列表");
                for (int i = 0; i < fdir1.list().length; i++)
                    System.out.println((fdir1.list())[i]);

            }
            System.out.println("请输入该文件夹中的一个文件名:");
            sfile = inp.readLine();
            File ffile = new File(fdir1, sfile);
            if (ffile.isFile()) {
                System.out.print("文件名:" + ffile.getName());
                System.out.print(";所在文件夹:" + ffile.getPath());
                System.out.println(";文件大小:" + ffile.length() + "字节");
            }
        } catch (IOException e) {
            System.out.println(e.toString());
        }
    }
}
```

