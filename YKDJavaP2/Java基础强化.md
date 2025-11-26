由于Java是一个面向对象的语言，Java把一切内容（字符串、数字、布尔、日期、时间)都用对象来表示，所以在ava的世界中
变量内容就是对象。



数学函数

```java
double value = Math.random();		//生成随机数
```



比较运算符两边对象类型必须一样，int与int，double与double等等

数组长度  Array.length  可以获取

实际上数组的数据初始化，还有一个简写方式，如果数据已经很确定的情况下可以在声明时就对列表一次性赋值
String[]tables=new string[]{"张三"，"李四"，"王五"}；

字符串对象有.length()方法

取字符串中的一个字符charAt()

trim()去掉左右多余的空格

indexOf(str)

indexOf(str, 开始索引值)

substring()字符串截取

str.startsWith/endsWith()

str.replaceAll(A,B)   新值B可以为空格，能起到删除内容的作用

str.split()

str.toUpperCase/toLowerCase()

str1.equals(str2)



数字转字符串

Integer . parseInt(str)

""+str 也可以使数字变为字符串类型数据

String . valueOf()   可以接受数字，浮点，布尔类型转化为字符串



getMonth0和getDayOfWeek0方法的返回值不是具体的数字，而
是一个对象(Java官方的设计)，所以必须用getValue0得到具体
的数字。
等大家Jva能力提升后，可以自己查阅官方文档，学习细节。目
前不用纠结具体返回什么对象

("加1天："+now.plusDays(1));
("加1周："+now.plusWeeks(1));
("加1月："+now.plusMonths(1);
("加1年："+now.plusYears(1));
("减1天："+now.minusDays(1));
("减1周："+now.minusWeeks(1));
("减1月："+now.minusMonths(1));
("减1年："+now.minusYears(1));

两个日期时间的判断

  .isBefore()

  .isAfter()

  .isEqual()



我们把在类中直接定义的变量称为对象属性，或者类属性





#### File 对象的其他方法

  1 public String getName()

返回由此抽象路径名表示的文件或目录的名称。

  2 public String getParent()、

返回此抽象路径名的父路径名的路径名字符串，如果此路径名没有指定父目录，则返回 null。

  3 public File getParentFile()

返回此抽象路径名的父路径名的抽象路径名，如果此路径名没有指定父目录，则返回 null。

  4 public String getPath()

将此抽象路径名转换为一个路径名字符串。

  5 public boolean isAbsolute()

测试此抽象路径名是否为绝对路径名。

  6 public String getAbsolutePath()

返回抽象路径名的绝对路径名字符串。

  7 public boolean canRead()

测试应用程序是否可以读取此抽象路径名表示的文件。

  8 public boolean canWrite()

测试应用程序是否可以修改此抽象路径名表示的文件。

  9 public boolean exists()

测试此抽象路径名表示的文件或目录是否存在。

  10 public boolean isDirectory()

测试此抽象路径名表示的文件是否是一个目录。

  11 public boolean isFile()

测试此抽象路径名表示的文件是否是一个标准文件。

  12 public long lastModified()

返回此抽象路径名表示的文件最后一次被修改的时间。

  13 public long length()

返回由此抽象路径名表示的文件的长度。

  14 public boolean createNewFile() throws IOException

当且仅当不存在具有此抽象路径名指定的名称的文件时，原子地创建由此抽象路径名指定的一个新的空文件。

  15 public boolean delete()

删除此抽象路径名表示的文件或目录。

  16 public void deleteOnExit()

在虚拟机终止时，请求删除此抽象路径名表示的文件或目录。

  17 public String[] list()

返回由此抽象路径名所表示的目录中的文件和目录的名称所组成字符串数组。

  18 public String[] list(FilenameFilter filter)

返回由包含在目录中的文件和目录的名称所组成的字符串数组，这一目录是通过满足指定过滤器的抽象路径名来表示的。

  19 public File[] listFiles()

返回一个抽象路径名数组，这些路径名表示此抽象路径名所表示目录中的文件。

  20 public File[] listFiles(FileFilter filter)

返回表示此抽象路径名所表示目录中的文件和目录的抽象路径名数组，这些路径名满足特定过滤器。

  21 public boolean mkdir()

创建此抽象路径名指定的目录。

  22 public boolean mkdirs()

创建此抽象路径名指定的目录，包括创建必需但不存在的父目录。

  23 public boolean renameTo(File dest)

重新命名此抽象路径名表示的文件。

  24 public boolean setLastModified(long time)

设置由此抽象路径名所指定的文件或目录的最后一次修改时间。

  25 public boolean setReadOnly()

标记此抽象路径名指定的文件或目录，以便只可对其进行读操作。

26 public static File createTempFile(String prefix, String suffix, File directory) throws IOException

在指定目录中创建一个新的空文件，使用给定的前缀和后缀字符串生成其名称。

27 public static File createTempFile(String prefix, String suffix) throws IOException

在默认临时文件目录中创建一个空文件，使用给定前缀和后缀生成其名称。

28 public int compareTo(File pathname)

按字母顺序比较两个抽象路径名。

29 public int compareTo(Object o)

按字母顺序比较抽象路径名与给定对象。

30 public boolean equals(Object obj)

测试此抽象路径名与给定对象是否相等。

31 public String toString()

返回此抽象路径名的路径名字符串。





比如我们所熟悉的String、int、boolean这些其实也都是由Java创建的
对象。
有个特殊的点，需要大家了解一下：
int、boolean(小写)这个是编程语言的原生对象
实际上ava也有类似String这样的对象类型（也叫做包装类）：
int的Java对象就是Integer;
boolean的Java对象就是Boolean;
double的Java对象是Double。
原生对象和包装类的主要区别在于，包装类的默认值是null
比如int的默认值是0,但是Integer的默认值是null;boolean的
默认值是false,但是Boolean的默认值是null。

1.1 add 方法

add()方法



1.2 get/size 方法


> 一般我们对索引的单词使用是 index

根据这两个特性也可以进行循环处理啦，大家可以回想一下 for 语句，我们改造一下上面的代码

1.4 List 和 ArrayList

List 是接口，ArrayList是其中一个常用的实现类。当然还有其它一些不常用的实现类。

```
ArrayList<String> strs = new ArrayList<>();
```

写作

```
import java.util.List;

List<String> strs = new ArrayList<>();
```

会更好，更符合面向对象的编程原则。


2 Map

Java 中常用的可以存储对象的集合容器，除了按顺序存储对象的 ArrayList，还有一种是 Map 。

Map 不强调存储的顺序，而是通过键值对来存储和读取。

我们大部分的情况下，都会使用 HashMap 这个 Map 的实现类。所以如果想得到一个 Map 的实例的话可以使用 HashMap

```
import java.util.Map;
import java.util.HashMap;

// key value 得是 Java 类型
Map<key, value> map = new HashMap<>();
```

> Map是接口，HashMap 是常用的实现了。当然 Map 接口还有其它很多不常用的实现类。有兴趣的同学可以自己看书学习

2.1 存入数据

可以使用 `map.put(key,value)` 这个方法完成数据的存储

由于 Map 的键和值都是 Java 对象类型，所以我们在实际创建的时候也需要指定对应的类型，上面的案例中 key 是数字类型：Integer，value 是字符串类型:String，所以我们可以用 `Map<Integer, String>` 来表示，这也是关于**泛型**的用法

现在这个 map 实例已经包含了 7 条记录啦，我们完成了集合的存储。

2.2 读取数据

如果我们想知道数字 3 对应的值，那么我们就可以使用 `map.get(key)`这个方法来获取啦

```
String weekText = map.get(3);
System.out.println(weekText);
```

大家看一看，使用 Map 存储这种键值对的数据是不是很方便？

由于 Map 也是一种集合数据，所以也有集合大小的方法：`size()`和遍历能力`for`

比如上面的代码想要打印出集合大小

```
int size = map.size();
System.out.println(size);
```

2.3 遍历所有数据

Map 的遍历相对麻烦一点，因为是 key：value 格式，所以我们一般先得到这个数据格式的集合（entrySet），完整的例子如下：

```
 for (Map.Entry<Integer,String> entry : map.entrySet()){

   System.out.println("Key = " + entry.getKey() +
                  ", Value = " + entry.getValue());
 }
```

> 调用 put 方法写入数据

而读取数据时，需要给 get 方法传入正确的 Key

> 调用 get 方法读取数据

> 完整的 Map 接口方法可以 [点击查看文档](https://ham.youkeda.com/articles/detail/5f3758fe5e205f30b2c2b2f0)

