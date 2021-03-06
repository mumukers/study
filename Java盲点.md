# 面向对象三大特性

---

## 封装

​			把抽象出来的数据【属性】和对数据的操作【方法】封装到一起。数据被保护在内部，程序的其他部分只有通过被			授权的操作【方法】才能对数据进行操作。

### 			好处：

​			1.隐藏实现细节
​			2.可以对数据进行验证

## 继承

​			解决代码复用性问题，当多个类存在相同的属性和方法时，可以从这些类中抽象出父类，在父类中定义这些相同的			属性和方法，其他类不需要再声明这些属性和方法，只需要通过extends声明继承父类即可。

### 		好处：

​				1.代码复用性提高了
​				2.代码扩展性和可维护性提高了

### 		本质：

​				当继承关系确定后，子类对象创建时，建立的是一个查找的关系

### 		细节：

​				1.子类继承了父类所有属性和方法，非私有的属性和方法子类可以直接访问，私有的属性和方法只能通过父类提					供的公有方法访问
​				2.子类没有继承父类构造器，但是必须调用父类构造器，完成父类初始化。
​				3.当创建子类对象时，关键字不管使用哪个子类构造器默认总会调用父类构造器。如果父类中没有提供无参构造					器，则必须要通过**super**关键字指定用父类中哪个构造器。
​				4.可以用**super**关键字显式指定使用父类中哪个构造器。
​				**5**.super在使用时只能放在构造器第一行，super只能在构造器中使用。
​				**6**.super（）和this（）都只能在构造器第一行，所以不能同时存在。
​				**7**.super（）父类构造器的调用不只限于直接父类，可以一直上溯到Object类
​				8.Java只支持单继承。要继承两个，就要串起来。
​				9.不能滥用继承

## 多态

​			方法和对象具有多种形态，是面向对象的第三大特性，是建立在封装和继承的基础上的

### 			多态具体实现：

#### 					方法多态：

​							方法重载和方法重写

#### 					对象多态：

​							1.对象的编译类型和运行类型可以不同，编译类型是在定义时就确定了，不能变化
​							2.对象的运行类型是可以变化的，可以通过getClass（）方法获取查看
​							3.编译类型看等号左边，运行类型看等号右边

### 					Java的动态绑定机制：

​							1.当调用对象方法时，该方法和对象内存地址/运行类型绑定
​							2.当调用对象属性时，没有动态绑定机制，哪里声明，哪里使用
​								示例：B继承A，A a=new B()，调用a对象中的属性时，是调用A类中的而不是B类中的
​							3.调用普通方法时，使用的是动态单分派：根据new的类型确定对象
​								调用静态方法时，使用的是静态多分派：根据静态类型确定对象



# 转义符 \

当遇到特殊字符需要转为别的意思时，需要使用 \ 来转义，如 \t

当字符被双斜线包裹时,就要用双斜线 ，如

```java
"\\."
```



# 包

---

## 注意

​			当引入一个包时，只允许访问该目录下的所有类，而不允许访问子目录下的类（除非单独引入）

​			解释：该子目录下可能**有相同的类名导致冲突**



# main方法语法说明

1.由JVM来调用main方法

2.JVM调用main方法，所以main方法的访问权限必须是public

3.JVM在调用main方法不需要创建对象

4.main方法接收String类的数组为参数，该数组中保存执行java命令时传递给所运行的类的参数

​	示例：java hello 参数一	参数二	参数三

## 特别注意：

main方法依旧遵守static的使用规则

1.可以调用所在类中静态成员和静态方法

2.不能调用非静态成员和方法，只能通过声明类的一个实例对象来使用

## 如何在idea传递参数给args：

正上方锤子旁边- 》点击edit Configurations

# 基本类型的自动装箱和拆箱

---

## 适用位置

​				引用类型和值类型之间

## 装箱

​			把基础类型封装为一个类

### 			具体实现：

​							调用包装器的**valueOf**方法实现。

## 拆箱

​			把类转化为基础类型（把引用类型的对象转化为值类型的对象）

### 			具体实现：

​							调用包装器的**xxValue**方法实现。

## 注意：



​			1.==比较与变量声明方式和值范围有关：
​				包装类和基础类型**用==比较时，包装类型拆箱 **直接比较 值

​				对于Integer来说
​						int a = 值1
​							将值1存在栈中

​						Integer a = 值1调用的是Integer.valueOf()方法
​							当值1在-128（Integer . low）~127（Integer . high）**之间**时，不会创建Integer对象
​							当值1在-128~127**之外**时，会调用new  Integer（）创建对象

​						Integer a = new Integer(值1)
​							**不管**值1 是否在-128~127范围内，都直接创建Integer对象

​			2.equals先比较类型是否相同，再比较值是否相同
​				包装类 . equals(基础类)
​					先将基础类封装，再比较类型是否相同，最后比较值的大小。

# String类的创建剖析

---

## 方法：

​				intern（）：返回常量池中与调用者内容相同的对象。如果没有，就先创建，再返回

​				format(String，……，……)：通过占位符对字符串进行格式规定
​					占位符：%s（字符串） , %d（整数） , %0.nf (保留 n 位小数) ， %c（字符）

​					如：String strFormat = “你的名字是%S，分数是%0.2f”;
​							String  str = String . format(strFormat,"wangkang",23.3333);

## 分类：

### 				1.使用字符串创建String对象（String  str="……"）

​					步骤：先在**字符串常量池**里面寻找是否有该字符串对象
​										有：直接将 str 指向常量池里的现有对象
​										无：在字符串常量池里创建一个该字符串对象，然后让  str  指向它

### 			     2.使用构造器创建字符串对象（String  str  =  new  String  (……)）

​					步骤：直接在堆中创建对象，该对象维护了一个类型为char[]  的value 属性。
​								当对象中的内容在常量池中存在的时，就让该属性指向常量池中的该字符串的地址
​								如果该内容在常量池中不存在，就在常量池中创建该字符串对象，然后让value指向
​					**注意：**
​								**String 对象的内存地址**和它**其中的属性所指向的地址**是不一样的

### 				3.使用两个字符串常量相加创建一个新的字符串对象（String  str  =  "abc"+"bcd"）

​					剖析：编译器在创建对象时，不会创建“abc”和“bcd”这两个对象，而是直接在常量池里								创建“abcbcd”对象，**创建的对象在常量池中**

### 				4.使用两个String类型的变量创建一个新的String对象

### 				（String  a = "abc"    String  b = "bcd"    String  c = a + b）

​					剖析：创建新对象时，先创建一个StringBuilder对象，将两个字符串拼接起来，然后通								过String的构造器将StringBuilder中的value属性作为参数传递
​								return  new  String(value, 0, count);
​								所以**创建的对象在堆中**

### 				5.使用一个String类型变量和一个字符串常量创建一个新的String对象

​					剖析：在查看源码时，发现该方式与  4 方法相同，所以**创建的对象也在堆中**



# StringBuffer类（线程安全）

---

## 方法：

​				append（）：将字符串拼接到当前字符串上
​										注意：当字符串为null 时，将null转化为 ‘n’, ‘u’, ‘l’, ‘l’,，
​													但是调用str . length()时会产生空指针异常

​				delete（int  start, int  end）:将index 为 start到 end-1的子串删除

​				insert（int index，String str）：将str 插入到index位置上

​					

# StringBuilder（线程不安全，但是效率高）

---

方法：与上面StringBuff几乎一致

# String，Stringbuilder，StringBuffer比较

---

1.
		String是不可变字符串，效率低，但是代码复用性高
		StringBuffer是可变字符串，效率高，支持多线程
		StringBuilder时可变字符串，效率高，线程不安全
2.
		存在大量修改操作时就用StringBuilder或StringBuffer
		多线程用StringBuffer，单线程用StringBuilder



# 常用工具类

---

## Math（数学工具类）

### 			方法：

​					Random():随机获取 [ 0 ,1）之间任意一个数

​					floor():对数进行向下取整

​					ceil():对数进行向上取整

​					round():对数进行四舍五入

## Arrays（数组工具类）

### 			方法：

​					sort():对数组进行排序
​						分类：
​								自然排序：

```Java
Arrays.sort(arr);
```


​								自定义排序：

```Java
//匿名内部类+动态绑定
Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1-o2;//这里决定排序的顺序是（由小到大，还是由大到小）
            }
        });
```

​					注意：前面 - 后面是由小到大，后面 - 前面是由大到小

​					binarySearch(Object[]  a，Object  target):对**有序数组**进行二分查找
​							如果target存在，return  index；
​							**如果target不存在，return  -（low+1）**

​					copyOf（arr ，length）：新建一个类型相同，长度为length的数组，将arr拷贝到新数组中并返回
​																该方法底层使用System.arraycopy()

​							情况分类：
​											length<0：报错
​											length<arr.length：将arr中前length个元素复制到新数组中，并返回
​											length==arr.length：将arr完整复制到新数组中并返回
​											length>arr.length：将arr复制到新数组前arr.length个元素中，后面空出，一般用于数组扩容

​					fill（arr，obj）:使用obj去填充arr数组，可以理解为将所有元素替换为obj

​					equals（arr1，arr2）：两数组元素完全一致返回true，否则false

​					asList（）：将一组值转化为List集合

```Java
List  asList = Arrays.asList(1,2,3,5,6,9);
//编译类型为List接口
//运行类型为ArrayList
```



## System类（系统类）：

### 			方法：

​					exit（0）：退出程序,0表示状态值

​					arraycopy（src，srcPos，dest，destPos，length）：复制数组

​							参数：

​									src：the  source  array(待拷贝数组)

​									srcPos：starting  position  of  the  source  array(开始拷贝的位置)

​									dest：the  distination  array(拷贝数组的目的地)

​									destPos：starting  position  of  the  destination  array(开始接收拷贝的位置)

​									length：从srcPos开始拷贝的长度

​							注意：要保证两个数组的类型相同（包装类行和对应的基本类型不相同）

​					currentTimeMillis（）：获取（当前-1970.1.1）毫秒数

​					gc（）：垃圾回收机制

## BigInteger/BigDecimal（大数类）

​						先用字符串处理，再转成相应对象

### 							构造方法：

​									示例：BigInteger  bi = new BigInteger("123444562771617617671");

### 							注意：

​									不能直接使用 运算符 进行加减乘除，应当使用方法.
​									其中数据应当为相同的大数类型

### 							方法（）：

​									加  add（）
​									减 subtract（）
​									乘 multiply（）
​									除 divide（）
​											注意：对于BigDecimal类型来说，可能会返回一个无限循环小数，抛出异常
​														**可以在调用方法时指定精度**
​														示例：

```java
	 BigDecimal 1.divide(BigDecimal 2，BigDecimal.ROUND_CEILING)//保留与分子(被除数)相同的精度
```



### 							适用范围：

​									当整型数据过大时，使用BigInteger
​									当要求精度够大时（小数点后多位小数），使用BigDecimal

## Date类（第一代日期类）

### 				方法：

​						1.日期格式：
​						

```Java
SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd  hh:mm:ss E")
//y:年  M：月  dd：日  hh：mm：dd ：时分秒  E星期
String s=sdf.format(Date d);//将日期格式转化为设定的格式
String s=sdf.parse("……");//将指定格式的日期还原为默认格式
```



## Calendar类（第二代日期类）

​			Calendar是一个抽象类，通过静态方法getInstance（）获取对象，用过get（）获取年,月,日

### 				方法：

​						get():获取Calendar类里的静态字段

```java
c.get(Calendar.Year)
c.get(Calendar.MONTH+1)//Calendar里面的Month以0开始
c.get(Calendar.DAY_OF_MONTH)//获取日期
c.get(Calendar.HOUR)//获取12进制日期
c.get(Calendar.HOUR_DAY)//获取24进制日期
```

​			Calendar没有专门的格式化方法，靠程序员自己组合

## LocalDate（日期），LocalTime（时分秒），LocalDateTime（都有）（第三代日期类）

### 			前两代日期类弊病：

​							1.可变性：日期时间应该不可变

​							2.偏移性：Date年份从1900年开始，而月份都从0开始

​							3.格式化：Calendar没有专门格式化

​							4.线程不安全，不能处理闰秒（每两天多一秒）

### 			方法：

​							now（）：获取当前日期时间的对象

​							getYear（）

​							getMonth（）：获取英文的月，如MARCH

​							getMonthValue（）：获取数字月

​							getDayOfMonth（）：

​							……

### 			格式化：

​							

```java
DateTimeFormatter  dtf = new DateTimeFormatter（格式）;
String s = dtf.format(str);
```





# 控制流程

---

## if语句

### 注意：

​		if（语句A）中是判断语句A的类型是否为 true或 false
​		语句A为赋值语句如：A=……时返回的值如果不是boolean类型的值，就会报错

#### 		示例：

​				if(a=1)//报错
​				if（flag=true）//不会报错，将flag赋值为true后，再执行{ }内的代码块



## for循环的执行顺序

​			for（表达式1；表达式2；表达式3）{
​					循环体；
​			}

​			第一步：循环开始执行一次表达式1（表达式1只在循环开始时执行，剩下的循环都从第二步判断开始）
​			第二步：执行表达式2进行判断
​			第三步：进入循环**执行循环体**
​			第四步：执行表达式3进行迭代

## switch括号内的类型

​			switch（x）：
​				x的类型可以为byte，short，int，char及其包装类，**不能为long，float，double，boolean**

# 方法参数

---

## 如何传递参数？

​			Java中使用创建对象引用的副本来传递参数。

## Java对方法参数能做什么和不能做什么？

​			1.方法不能修改基本数据类型的参数
​			2.方法可以修改对象参数的状态。
​			3.方法不能让对象参数引用一个新对象

# 代码块（初始化块）

---



## 适用时机

​					作为属性初始化、构造器的延续。当构造器中出现重复语句时，就可以**使用代码块抽象出构造器中重复语句**

## 分类

### 静态代码块：

​					用static修饰，只能调用静态成员（静态方法和静态属性）
​					只在类加载时调用，所以**只执行一次**

### 普通代码块：

​					无修饰，可以调用任意成员
​					在类创建对象实例时调用，所以**每次创建一个对象就执行一次**

 

## { }内可以填入语句：

​					任何逻辑语句：输入、输出、方法调用、判断、循环

## 调用时间：

​					在类加载时（静态代码块），或者创建类的实例对象时（普通代码块）调用

## 创建对象时的调用顺序：

### 一个类中：

#### 规则：

​			1.优先级相同时，按照在类中定义的顺序调用
​			2.优先级：
​							静态属性初始化 = 静态代码块
​							非静态属性初始化 = 普通代码块
​							静态  >  普通
​			3.静态和普通执行完之后，再执行构造器

### 类存在继承关系：

#### 			只看普通：

​			pubilc AAA{
​				public AAA(){
​					1.先调用super（）构造器
​					2.再调用普通代码块和非静态属性初始化
​					3.再调用构造器主体
​				}
​			}

​			所以调用一个子类构造器时，会先进行父类构造器的调用，父类构造器也会满足上面的执行顺序调用本地的
​			super（）构造器、普通代码块、构造器主体等等，直到Object类

### 			包含静态：

​				通过extends关键字先进行父类加载，再进行子类加载，故先进行父类静态，再进行子类静态

​				1.**调用父类静态**代码块和静态属性初始化
​				2.**调用子类静态**代码快和静态属性初始化

---

​				分割线下面和只看普通一致

​				3.**调用父类普通**代码块和非静态属性初始化
​				4.**调用父类构造器**主体
​				5.**调用子类普通**代码块和非静态属性初始化
​				6.**调用子类构造器**主体

# 方法重载与方法重写

---



## 方法重写

### 概念:

​			重写是**子类对父类的<u>*允许访问的方法*</u>的实现过程进行重新编写**, 返回值和形参都不能改变。
​			即外壳不变，核心重写！（必须是父类中有的方法）

### 规则：

​			1.重写的方法的访问权限不能比父类中被重写的方法的访问权限低，也就是private的方法不能被重写
​			2.参数列表，返回值，方法名必须完全相同
​			3.声明为**final**的方法不能被重写。声明为**static**的方法不能被重写，但是能再次声明
​			4.重写的方法能够抛出任何非强制性异常，但不能抛出**新的强制性异常**
​			5.对于不能继承的方法，就不能重写该方法
​			6.笔者总觉得对抽象方法实现是一种特殊的重写

### 运行时：

​			先找到两个类中都有的方法，然后执行时看子类的具体实现

## 方法重载

### 概念：

​			重载是在一个类里面，方法名相同，参数不同，返回值可以相同也可以不同

### 规则：

​			1.被重载的方法可以改变返回类型；
​			2.被重载的方法可以改变访问修饰符；
​			3.被重载的方法可以声明新的或更广的检查异常；
​			4.方法能够在同一个类中或者在一个子类中被重载。
​			5.无法以返回值类型作为重载函数的区分标准。

## 注意：

​				方法重写时，子类方法的访问权限必须大于等于父类方法的访问权限



# 向上转型和向下转型

---

## 向上转型

### 概念：

​			父类引用指向子类对象

### 特性：

​			向上转型就是把子类对象直接赋给父类引用，不用强制转换。使用向上转型可以**调用父类类型中的所有成			员，不能调用子类类型中特有成员，最终运行效果看子类的具体实现**。



## 向下转型

### 概念：

​			子类对象指向父类引用

### 注意：

​			如果**父类引用对象指向的是子类对象**，那么在向下转型的过程中是安全的，也就是编译是不会出错误。
​			但是如果**父类引用对象是父类本身**，那么在向下转型的过程中是不安全的，编译不会出错，但是**运行时会出现我们			开始提到的 Java 强制类型转换异常**，一般使用 **instanceof** 运算符（**比较运行时类型，而不是静态类型**）来避免			出此类错误。



# 动态分派和静态分派

---

## 静态分派

### 特性：

​			静态分派只会涉及重载，而重载是在编译期间确定的，那么静态分派自然是一个静态的过程

​			静态分派的最直接的解释是**在重载的时候是通过参数的静态类型而不是实际类型作为判断依据的**。

​			原因在于**静态类型的变化仅仅在使用时发生，变量本省的类型不会发生变化**。

### 理解:

​			由于只涉及重载，当一个方法需要传递参数时，只关注参数本身的静态类型，而不是它所指向的实际类型

### 示例：

​				B extend A，当一个方法的参数为B类的对象时，即使将B类进行向上转型，使A类引用指向B类对象，也不				能将该引用传递给该方法当参数，理解为只看静态类型。不过参数为A类型的对象时，可以将B类型的对象				当参数传递。

## 动态分派

一个最直接的例子就是方法重写



# 抽象类和接口区别

---



| **Java7的特性** |         抽象类         |                   接口                   |
| :-------------: | :--------------------: | :--------------------------------------: |
|    构造方法     |           ✓            |                    ✕                     |
|  普通成员变量   |           ✓            |                    ✕                     |
|    普通方法     |           ✓            |                    ✕                     |
|    访问类型     |     public,protect     |               public(默认)               |
|    静态方法     |           ✓            |  ✕（自Java8之后就可以有静态和默认方法）  |
|  静态成员变量   |           ✓            |      ✓（默认为public static final）      |
|    类的实现     |        继承一个        |                 实现多个                 |
|    使用方向     | 代码实现，可以重复使用 | 系统架构设计，用于定义模块之间的通信契约 |



| **Java8的特性** | 抽象类                 | 接口                                                         |
| --------------- | ---------------------- | ------------------------------------------------------------ |
| 构造方法        | ✓                      | ✕                                                            |
| 普通成员变量    | ✓                      | ✕                                                            |
| 普通方法        | ✓                      | ✕                                                            |
| 访问类型        | public,protect         | public(默认)                                                 |
| 静态方法        | ✓                      | ✓（可以有默认方法default修饰和静态方法<br />     【都可以有方法体】） |
| 静态成员变量    | ✓                      | ✓（默认为public static final）                               |
| 类的实现        | 继承一个               | 实现多个                                                     |
| 使用方向        | 代码实现，可以重复使用 | 系统架构设计，用于定义模块之间的通信契约                     |
| 继承其他同类型  | ✓                      | ✓                                                            |



# Object中的重要方法

## == 和 equals

---

### ==

#### 判断对象类型：

既可以是基本类型，也可以是引用类型

基本类型：判断值是否相等

引用类型：判断地址是否相同，即判断指向对象是否相同

#### 注意：当两个对象类型都不相同时，产生编译错误，



### equals

#### 判断对象类型

只能是引用类型

默认判断地址是否相等，一般可以子类重写判断内容是否相等。比如Integer，String



## hashocde方法

---

### 结论：

​			1.提高具有哈希结构的容器的效率

​			2.两个引用，如果指向的是同一个对象，则哈希值肯定是一样的

​			3.两个引用，如果指向的是不同对象，则哈希值是不一样的（在范围较大时，可能会产生碰撞）

​			4.哈希值主要是通过地址计算的，但不能完全等价

​			5.在集合中，如果有需要的话，也会重写

## finalize方法（新版Java已经弃用该方法）

---

### 对象回收：

​				当某个对象没有引用指向它时，系统就会认为该对象是一个垃圾，会使用垃圾回收机制来销毁该对象。
​				在销毁该对象前，会调用该方法。

### 调用时间：

​				当对象被回收时，系统自动调用finalize方法，子类可以重写该方法，进行资源释放操作

### 垃圾回收机制的调用：

​				由系统决定（系统有自己的GC算法），也可以通过System.gc（）来主动触发GC机制

### 注意：

​				在实际开发中，一般不会使用finalize方法（系统并不是时刻监控，一产生垃圾就回收），但是必须了解

# 用户自定义类

---

## 访问控制符

|      | 访问级别 | 访问控制修饰符 | 同类 | 同包   | 子类 | 不同包 |
| ---- | -------- | -------------- | ---- | ------ | ---- | ------ |
| 1    | 公开     | public         | 可以 | 可以   | 可以 | 可以   |
| 2    | 受保护   | protected      | 可以 | 可以   | 可以 | 不可以 |
| 3    | 默认     | 没有修饰符     | 可以 | 可以   | 没有 | 不可以 |
| 4    | 私有     | private        | 可以 | 不可以 | 没有 | 不可以 |

### 注意：

​			一般不用private修饰类



## final实例字段

### 特性：

​			用final关键字修饰**字段**的一旦在初始化完成后就不能再改变它的值
​			用final关键字修饰的对象引用的地址不能改变，但是可以改变其中的值，
​				如：数组中的值可以改变，但是不能改变数组的地址，如不能让该引用指向另一个数组

### 初始化：

​			用final声明的字段必须要在构造对象时完成初始化（在构造器执行完成时必须完成初始化）
​	——final字段初始化可以在
​												1.定义时
​												2.代码块
​												3.构造器
​			完成初始化

### 注意细节：

​			1.被final修饰的类不能被继承，其中的方法自然也不能被重写
​			2.被final修饰的方法只能被子类继承，不能被子类重写
​			3.被final修饰的类的属性或局部变量不能再修改它的值
​			4.被final修饰的方法可以进行重载**（创建了方法签名不同的方法）**，
​				但是不能进行重写**（本身方法签名不能更改）**

## static实例字段

### 特性：

​			可以用于类的属性和方法上，被static修饰的方法属于类方法和类变量，可以由类名调用

### 初始化：

​			1.定义时
​			2.静态代码块
​			

### 注意：

​			1.不能在构造器中完成初始化
​			2.可以进行重载，重载是编译时多态
​			3.不能进行重写，重写时运行时多态

## 对象构造



### 默认字块初始化

​			在类中声明的字段当没有在构造器中显式地初始化时，就会被自动地赋为默认值。
​			数值为0，布尔类型为false，对象引用为null

### 			注意：

​					**方法中的局部变量**必须明确地初始化，但是在类中声明的字段没有初始化就会被赋为默认值。

### 初始化块

​			在一个类的声明中可以包含任意多个代码块，这些代码块可以在这些类的对象构造时执行

### 调用构造器的具体处理步骤

​			1.如果构造器的第一行调用另一个构造器，则根据提供的参数执行另一个构造器。
​			2.否则:
​						所有数据字段初始化为其默认值
​						按照在类声明中出现顺序，执行所有字段初始化方法和初始化块。
​			3.执行构造器主体代码

### 静态代码块

​			会在类第一次加载时执行，也只执行一次。后面不管声明多少对象，都不会再执行

### 静态字段初始化

​			可以使用一个静态的代码块初始化静态字段

## 抽象类

​			只能用来修饰类和方法

### 特点：

​			1.抽象类中不一定有抽象方法（也可以什么方法也没有）
​			2.有抽象方法一定是抽象类，要声明为abstract
​			3.抽象方法不能有方法体
​			4.抽象方法不能由private,final,static来修饰，因为这些关键字与重写相违背
​			5.可以对抽象方法进行重载，重写（主要）
​			**6.任何与抽象方法相违背的关键字都不能修饰抽象类和抽象方法**，如private,static,final
​			**7.抽象类可以有任意成员，但是不能实例化**
​			**8.一个类继承抽象类，则必须实现抽象类中所有抽象方法，否则也要声明为抽象类**

## 接口

### 继承与接口价值区别：

​			继承：解决代码复用性和可维护性

​			接口：通过【接口规范性和动态绑定机制】设计好各种规范，让其他类去实现这些方法，即更加灵活

### 特点（主要针对JDK 8）：

​			1.接口不能实例化
​			2.接口中的方法是由public  abstract修饰，可以直接简写为void  方法名（）
​			3.接口中属性都是由public static final 修饰的，属性声明可以简写为 ：数据类型 变量名
​			4.实现接口就必须将接口中所有抽象方法都实现
​			5.抽象类实现接口时，可以不实现抽象方法（觉得和抽象类中特点 8相似）
​			**6.一个类可以实现多个接口**
​			**7.接口不能继承其他类（抽象类也不行，试验过全部抽象方法的抽象类也不行），但是可以继承多个其他接口**
​			**8.接口的修饰符只能是public 和 default**（JDK 8后面的版本有）

### 接口多态：

​			使用接口类型传递参数可以对实现了该接口的类进行方法调用。**哪个实现接口的类对象传进来，使使用哪个实现**
​			**依然可以使用 instanceOf来判断运行类型**

### 接口多态传递：

​			interface A , interface B extends A , class M implements B
​			=>B b=new M()    A a=new M()

## 内部类：

### 		分类：

​			定义在外部类的局部位置上（如:方法中）
​					局部内部类（有类名）
​					匿名内部类（没有类名）

​			定义在外部类的成员位置上
​					成员内部类（不用static修饰）
​					静态内部类（用static修饰）

### 		类的五大成员：

​			属性、方法、构造器、代码块、内部类

### 		注意：

#### 			局部内部类：

​			**作用域：方法/代码块**

​				1.可以直接访问外部类所有成员
​				2.内部类不能用访问修饰符、static修饰（理解为一个局部变量，局部变量不能用访问修饰符，static修饰）
​					但是可以用final修饰
​				3.外部类访问局部内部类成员=》**在作用域中创建内部类对象**进行访问
​				**4.作用域在方法 / 代码块中**
​					a）如果局部内部类中有和外部类重名的方法，满足就近原则
​					b)  要访问外部类成员同名成员
​							外部类非静态成员：Outer . this . 成员名（this表示调用内部类所在方法的对象）
​							外部类静态成员：Outer . 成员名

#### 			匿名内部类：

​				**可以用来作为方法的参数传递**

##### 				针对接口的匿名内部类：

​					在实现接口时，有时并不想对临时只使用一次的情况专门定义一个实现类，
​					就可以在需要接口实现类的方法中定义一个匿名内部类。
​					
​					Interface  A{……}
​					
​					void method{
​						A  a = new A(这里不能有参数){
​							对A接口中抽象方法的实现（单纯只有抽象方法实现）
​						}
​					}

###### 							注意：

​							1.编译类型 A，运行类型 匿名内部类
​							2.系统会自动以  外部类名$数字 这样的方式对匿名内部类赋一个系统名称
​							3.匿名内部类只是单纯用来创建一个以接口实现类为模板的实例，并把地址返回给a。
​								**在实例创建完成后（使用一次），匿名内部类这个模板就不能再使用了**

##### 				针对类的匿名内部类：

​					理解为一种只想临时使用一次的对父类的继承，但凡继承可以用到的特性它都可以用到，
​					如：对父类方法的重写和定义自己独有的成员

​					class Father{}

​					void f1(){
​						Father f = new Father(构造器传参){
​							//定义自己独有成员
​							//重写父类方法
​						}
​						f . 成员方法（）； 
​					}

###### 					注意：

​					1.系统会自动给他一个系统名称和内部类命名方式相同
​					**2.括号内传递的参数是构造器传参，赋值给从父类继承来的成员变量**
​					（**用的是父类的构造器，不能自己定义构造器样式**）
​					**3.对抽象类来说，里面的抽象方法全部要实现**
​					**4.由于成员变量不遵循动态绑定机制，用父类引用调用的都是父类有的成员变量**
​						**但是可以定义自己的成员变量，然后通过方法获取这些变量的值**									



#### 成员内部类：

​			理解为外部类的成员变量

##### 		注意：

​			1.可以直接使用外部类的成员
​			2.可以使用访问修饰符如：public，protected，private
​			3.通过创建成员内部类对象可以直接访问内部类中所有成员（实在不懂为什么可以通过内部类对象访问私有成员）
​					获取两种方式：
​							1.Outter . Inner  in = outter . new Inner();
​							2.在Outter类中定义一个方法用来返回创建的Inner对象，再用Outter对象实例调用	
​			4.如果局部内部类中有和外部类重名的方法，满足就近原则
​			5.要访问外部类成员同名成员
​					外部类非静态成员：Outer . this . 成员名（this表示调用内部类所在方法的对象）
​					外部类静态成员：Outer . 成员名					 	

#### 静态内部类：

​			理解为外部类的静态成员，用static修饰

##### 注意：

​			1.可以访问外部类的所有静态成员，不能访问外部类的非静态成员
​			2.可以用任意访问修饰符修饰
​			3.作用域：同其他内部类一致，为整个类体
​			4.外部类访问内部类：创建内部类对象
​			5.外部其他类访问(注意满足访问权限，如使用private修饰不能直接类名调用): 
​				 Outter . Inner  in=new Outter . Inner() 
​			6.用外部类中方法返回Inner对象 
​			7.如果内部类有静态成员与外部类中静态成员一致，会遵循就近原则。
​				调用外部类中静态成员可以用 外部类名  . 变量名调用

## 枚举：

### 注意：

​			1.用enum替换class
​			2.使用**变量名（构造器传参）**替换成员变量
​			3.将枚举对象写在枚举类的行首
​			4.如果使用无参构造器，参数列表和小括号都可以省略
​			5.当有多个枚举对象时，用 ，隔开，最后一个用 ；结尾
​			6.**使用enum关键字时，会隐式地继承Enum类（不能继承其他类，但是可以实现接口），就可以使用Enum方法**
​				枚举对象名 . name（）方法：返回枚举对象的名称
​				枚举对象名 . ordinal（）方法：返回枚举对象顺序编号
​				枚举类 . valueOf（参数）方法：**按照传递的参数寻找枚举对象。如果没找到，就报错。**
​				枚举类 . values（）方法：返回一个枚举对象数组。
​				枚举对象 a . compareTo（参数：枚举对象 b）方法：**比较两个枚举对象编号,返回两个编号之间的差值** 
​					=》a.ordinal() - b.ordinal()。

## 注解：

### 			@Overrid ：

​							方法重写，不是方法重写会报编译错误

### 			@Deprecated

​							表名该 **构造器，属性，局部变量，参数，类型，方法**是过时的	

### 			@SuppressWarnings（{  " 警告类型" }）

​							压制警告

#### 							警告类型有：

​												// all，抑制所有警告 // boxing，抑制与封装/拆装作业相关的警告 // //cast，抑制与强制转型												作业相关的警告 // //dep-ann，抑制与淘汰注释相关的警告 // //deprecation，抑制与淘汰的												相关警告 // //fallthrough，抑制与 switch 陈述式中遗漏 break 相关的警告 // //finally，抑制与												未传回 finally 区块相关的警告 // //hiding，抑制与隐藏变数的区域变数相关的警告 // 												//incomplete-switch，抑制与 switch 陈述式(enum case)中遗漏项目相关的警告 // 												//javadoc，抑制与 javadoc 相关的警告 韩顺平循序渐进学 Java 零基础 第 497页 // //nls，												抑制与非 nls 字串文字相关的警告 // //null，抑制与空值分析相关的警告 // //rawtypes，抑制												与使用 raw 类型相关的警告 // //resource，抑制与使用 Closeable 类型的资源相关的警告 // 												//restriction，抑制与使用不建议或禁止参照相关的警告 // //serial，抑制与可序列化的类别遗												漏 serialVersionUID 栏位相关的警告 // //static-access，抑制与静态存取不正确相关的警告 												// //static-method，抑制与可能宣告为 static 的方法相关的警告 // //super，抑制与置换方法												相关但不含 super 呼叫的警告 // //synthetic-access，抑制与内部类别的存取未最佳化相关												的警告 // //sync-override，抑制因为置换同步方法而遗漏同步化的警告 // //unchecked，抑												制与未检查的作业相关的警告 // //unqualified-field-access，抑制与栏位存取不合格相关的												警告 // //unused，抑制与未用的程式码及停用的程式码相关的警告	

#### 							抑制位置：

​												在main方法上或者类上		

​						

```
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings {
    String[] value();
    //value()用来传递参数给注解，如{"rawtypes","unchecked"}
}
```

### 				四种元注解：

#### 						@Retention  (RetentionPolicy=SOURCE/CLASS/RUNTIME)

​										**将注解保留到哪个阶段**（RetentionPolicy . 选项）

​						选项：SOURCE（保留注解到源代码/编辑器阶段）
​									CLASS	(保留注解到class文件阶段)
​									RUNTIME（保留注解到JVM运行阶段）	

#### 					@Target（value={ CONSTRUCTOR,TYPE.....}）

​										**定义注解作用位置**（方法上，类上，变量上）

#### 					@Documented

​										指定被该元注解修饰的注解会在javadoc生成文档时，也生成文档保留。

#### 					@Inherited

​										被该元注解修饰的注解在子类继承自该类时，同时也会继承该注解

## 异常：

​				程序执行过程中发生的不正常情况（语法错误和逻辑错误不算）
​				

### 				分类：

​						ERROR：JVM无法解决的错误。发生ERROR，程序会崩溃

​						Exception：其他的因编程错误或外来因素引起的一般性错误，可以使用针对性的代码进行处理

​										分类：
​												**运行时异常**：程序运行时发生的异常，编辑器不强制要求处理的异常，一般是指编程时的逻																		辑错误
​												**编译时异常**：编程时，编辑器检测出的异常，要求必须处理

​						快捷键：ctrl + alt + t   对选中的代码进行包裹（要关闭QQ！）

### 			处理的两种方式：

​				1. try {可能产生异常的代码} 
​					catch {系统将异常信息封装为异常对象，传递给catch} 
​					finally{通常为关闭资源语句}：

​					在程序中捕获，程序员自行处理

​				2.throws 异常类（JVM调用main方法，main方法中调用其他方法）：
​					将异常抛出，由调用者处理。最高级处理者为JVM（直接输出异常信息，然后中断程序）
​					注意：没有try  catch环绕也没有throws抛出，main默认throws  Exception

# Collection集合

---

​				子接口：
​							List
​									实现类：ArrayList，vector，LinkedList

​							Set
​									实现类：HashTable，HashMap，properties

​				方法：
​						常见方法：
​									get（int  index）：
​									add(Object  o)
​									emove（int  index/Object  o）:
​									contains（Object  o）:
​									size（）:返回集合中**非空元素**个数
​									addAll（Collection  c）:添加一整个c中的元素
​									removeAll（Collection  c）：如果原来集合中有c集合中的元素，就删除
​									containsAll（Collection  c）：c集合是否是原集合的子集	
​						
​						获取迭代器：
​									iterator（）：获取迭代器																				

```java
//迭代器遍历集合
Iterator iterator=list.itrator();
//快捷键itit
//显示所有快捷键：ctrl + j
while (iterator.hasNext()) {
   Object next = iterator.next();
   System.out.println(next);
} 
//要再次遍历要重新获取迭代器
```



​						增强for循环：简化版的迭代器，原理一致



# List接口

---

​				实现子类：ArrayList，Vector，LinkedList

![image-20220419203852330](C:\Users\木木\AppData\Roaming\Typora\typora-user-images\image-20220419203852330.png)

​				可以通过**向上转型**创建List对象

## 			方法：

​							add（）：

​							add（int  index，Object  obj）：

​							remove（int  index/Object  obj）:

​							set(int  index,Object  objj):

​							sub(int  startIndex,  int  endIndex) : 将集合的一部分 [ startIndex,endIndex）返回
​								**注意：对返回的集合进行操作同时也影响原来的集合**

# ArrayList（线程不安全）

## 			

## 				注意：

​								1.ArrayList可以添加空值（add（null）），并且多个
​								2.ArrayList是由数组实现数据存储的
​								3.ArrayList基本等同于Vector，但是ArrayList是线程不安全的（但是效率也相对来说更高），
​									而Vector是线程安全的

## 				源码分析：

​								1.ArrayList中维护了一个transient  Object[ ]  elementData
​									transient表示瞬间的，短暂的，。表示该属性不会被序列化
​								2.使用ArrayList无参构造器时，初始容量应该置为 0。
​									第一次添加时，容量置为  10.
​									然后每次容量满后增加为当前容量的1.5倍
​								3.使用ArrayList（int  size）带参构造器时，初始化容量置为 size。
​									然后每次容量满后增加为当前容量的1.5倍

# Vector（线程安全）

Vector与ArrayList基本相同，但由于Vector支持多线程，建议用Vector。在单线程条件下建议用ArrayList，效率高

## 构造器：

​								Vector（）：默认容量为10，然后每次容量满后增加为当前容量的 2 倍

​								Vector（int  size）：设置初始容量 size，然后每次容量满后增加为当前容量的 2 倍
​																（默认capacityIncrement值为 0，通过三元运算符添加一个size的容量）

```java
int newCapacity = oldCapacity + ((capacityIncrement > 0) ?
                                 capacityIncrement : oldCapacity);
```

​								Vector（int  size  ，int capacityIncrement）：设置初始容量为  size，然后每次容量满后增加大小为																											capacityIncrement的容量



# LinkedList（线程不安全）

## 		源代码

​							add（）：添加元素

```java
 public boolean add(E e) {
        linkLast(e);
        return true;
    }

//在链表末尾添加元素 e
 void linkLast(E e) {
     final Node<E> l = last;
     final Node<E> newNode = new Node<>(l, e, null);//将pre指向last指向的尾结点，next指向null
     last = newNode;
     if (l == null)//让first指向第一个结点
         first = newNode;
     else
         l.next = newNode;
     size++;
     modCount++;
 }
```

​							remove（Object  e）：删除元素

```java
public boolean remove(Object o) {
    //寻找内容为o的结点,将其分为两类：null 和 非null
    if (o == null) {
        for (Node<E> x = first; x != null; x = x.next) {
            if (x.item == null) {
                unlink(x);
                return true;
            }
        }
    } 
    else {
        for (Node<E> x = first; x != null; x = x.next) {
            if (o.equals(x.item)) {
                unlink(x);
                return true;
            }
        }
    }
    return false;
}

//将结点 x 从链表中删除
E unlink(Node<E> x) {
        // assert x != null;
        final E element = x.item;
        final Node<E> next = x.next;
        final Node<E> prev = x.prev;
//主要是移除元素时先考虑是否为头，尾结点这两种边界情况
        if (prev == null) {
            first = next;//prev为空，说明当前元素为first。当前元素也要移除，让first指向下一个元素
        } else {
            prev.next = next;
            x.prev = null;
			//这里想了很久，prev只是一个引用，让引用置为null不会对对象本身产生影响，引用只能改变对象中的值
            //当对象没有任何引用指向时，才会被垃圾回收机制回收，这里有上面局部变量指向
        }

        if (next == null) {
            last = prev;//next为空，说明当前元素为last。当前元素也要移除，让last指向上一个元素
        } else {
            next.prev = prev;
            x.next = null;
        }

 //最终将内容也置为null，彻底清空该结点
        x.item = null;
        size--;
        modCount++;
        return element;
    }
```



# ArrayList和LinkedList比较



|            | 底层结构             | 增删效率 | 改查效率 |
| ---------- | -------------------- | -------- | -------- |
| ArrayList  | 可变数组（数组扩容） | 较低     | 较高     |
| LinkedList | 双向列表             | 较高     | 较低     |

在项目中一般使用查询较多，所以使用最多的是ArrayList

当然在不同模块中根据情况使用







# Set接口

---

实现Set接口的实现类对象 以下均称 Set接口对象

实现子类：HashSet，LinkedHashSet，TreeSet

![image-20220419203707512](C:\Users\木木\AppData\Roaming\Typora\typora-user-images\image-20220419203707512.png)

## 注意：

​			1.Set接口对象存和取数据的顺序不一定一致，但位置固定后就不会再改变
​			2.**Set接口对象是没有索引的**，也就不可能使用 index 获取和操作数据，只能指定元素进行操作
​			3.**Set接口对象是不允许重复的**，只允许放一个null
​			4.由于继承 Iterable接口所以可以进行遍历



# HashSet

**底层是一个HashMap**（而HashMap的底层机制是 数组+链表+红黑树）

## 注意：

​			1.不保证存取顺序一致
​			2.可以存放null，但是只能存放一个

## 底层机制：

​			HashSet底层是一个HashMap

​			添加一个元素时，会通过得到该元素 hash值，然后转化为索引值

​			找到存储数据表 table，看该索引的位置是否已经有元素
​				没有，添加该元素到该位置；
​				有，   先顺着该索引位置上的链表遍历，通过**equals（）方法**
​	 	**（当有equals（）方法重写时，就按照重写的方法）**看是否有相同的元素，没有就添加到最后，有就不添加

```java
set.add(new String("hsp"));
set.add(new String("hsp"));
//String重写了equals（）方法，所以认定它们为相同元素

set.add(new Dog("lucy"));
set.add(new Dog("lucy"));
//Dog类没有重写equals（）方法，所以认定它们为不相同元素
```



​			**在JDK 8中，当某一条链表长度 >= 8 时**，
​				**如果table数组的长度小于 64，就会进行扩容接点数组一次（每次扩容一次变为原来两倍）**
​			    **如果table数组的长度大于 64然后table转化为红黑树**



## add方法底层机制

```java
private static final Object PRESENT = new Object();//就是一个占位的变量
transient Node<K,V>[] table;//存放节点数组

public boolean add(E e) {
    return map.put(e, PRESENT)==null;//返回空时就会输出true，否则输出false
}

public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }

static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    //key为null时输出零，否则输出一种以hashCode为基础的编码key.hashCode() ^ (h >>> 16)来唯一标记一个key值
    }

final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab;//将tab指向table所指的数组对象
   	 	Node<K,V> p; //定义一个结点用来存放表的某个索引上的首结点
    	int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)//看该表是否为null，或者长度为0
            n = (tab = resize()).length;//将表扩容
        if ((p = tab[i = (n - 1) & hash]) == null)//根据得到的索引值找到位置后，如果没有存放元素（头结点）
            tab[i] = newNode(hash, key, value, null);//创建一个新的节点存放在在这个位置
        else {////根据得到的索引值找到位置后，如果已经存放了元素
            Node<K,V> e; //用来暂存一个结点
            K k;//用来存放一个结点的key值
            if (p.hash == hash &&
                ((k = p.key) == key 
                 //判断值类型
                 //(是同一个对象)
                 //第一个结点的hash值和当前key的hash值相同 并且 key值也相同（避免hash偶然碰撞）
                 
                 || (key != null && key.equals(k))))
                //判断引用类型
                //上面判断不要求key对象一定不为null，当时此处要调用equals方法
                //(不是同一个对象但是内容相同)
               //key不为null（null不能调用equals（）方法） 并且 内容相同（通过动态绑定判断）
                
                e = p;//是相同的就将e指向p这个首结点
            else if (p instanceof TreeNode)//p 后面是否已经被转化为一颗红黑树
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
           		 //调用树的添加方法添加该值
            else { //如果后面接的是一个链表，就使用for循环遍历
                for (int binCount = 0; ; ++binCount) {//一个死循环
                    if ((e = p.next) == null) {//遍历到尾结点;e一直指向p.next
                        p.next = newNode(hash, key, value, null);
                        //所有的结点都与它不相同，就将它插入到链表尾部
                        
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            //TREEIFY_THRESHOLD=8
                            //当把元素添加到链表末尾后，是否达到8个元素，达到后
                            //先进行判断，当数组长度没有到达64时，会先进行数组扩容；已经到达时，就树化
                            treeifyBin(tab, hash);
                        break; //所有都与它不相同，到达尾部，就break
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;//有相同的，也break
                    p = e;//让p往下一个结点移动，继续循环
                }
            }
            //说明已经存在该元素，就返回该元素
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            //很重要：这条语句表示不论是增加到一个空的数组位置，还是增加到链表尾部，都会越来越接近临界值
            //只要是增加了一个就算size+1
            resize();
        afterNodeInsertion(evict);
        return null;
    }

//返回一个“扩容后”新的结点数组，每次扩容为上次的两倍	
final Node<K,V>[] resize() {
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
        if (oldCap > 0) {
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        else if (oldThr > 0) // initial capacity was placed in threshold
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            newCap = DEFAULT_INITIAL_CAPACITY;
            //static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
            //（加载因子）DEFAULT_LOAD_FACTOR=0.75，所以占大小的75%
            //设置一个临界值，当超过这个值时就扩容，而不是超过数组大小时才扩容
        }
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
```



# Map接口

---

## 注意：

​			1.Map中存放的是具有映射关系的键值对 Key--Value
​			2.Map中的 Key和Value 可以是任何引用类型的数据，会被封装到HashMap$Node对象中
​			**3.Map中的Key值不能重复，而Value值可以重复。当出现Key重复时，会将Value替换为新的value**
​			4.Map中的Key最多只能由一个null，而Value可以有多个null
​			5.Map中Key不能重复的底层机制相同
​			6.Map中可以添加Object类的任何子类对象。**当添加基本类型时，会自动装箱为包装类**
​			7.可以通过Key获取Value值

```java
public V put(K key, V value) {//这就是Map的put方法底层
    return putVal(hash(key), key, value, false, true);
}

//Value替换的底层机制
if (e != null) { // existing mapping for key，这里的e指向Key值相同的键值对元素
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;//将新的value值赋给e.value 
                afterNodeAccess(e);
                return oldValue;
            }
```
