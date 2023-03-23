[TOC]



# Junit单元测试

*测试分类*

白盒测试：需要写代码，关注程序的具体流程

黑盒测试：不需要写代码，给出输入值，看程序是否能够给出期望的输出值

*Junit的使用*：白盒测试

*步骤：*

​				1：定义一个测试类（测试用例）

​							建议：测试类名 为 被测试类Test     CalcultorTest

​										包名为 xxx.xxx.test

​				2：定义测试方法：==可独立运行==

​							建议：方法名为test测试方法名    	testAdd

​									   参数   空参

​									   返回值 void

​				3：给方法加==@Test==

​				4：导入junit依赖环境

判定结果：

​				控制台下面字体颜色；看正常与否

​				一般使用==断言==操作处理结果：

​				==Assert.assertEquals(a,b)==//a是期望值，b是实际值

补充：

​	*==@Before==*:修饰的方法会在测试方法之前被执行

​	==*@After*==：修饰的方法会在测试方法之后被执行

# 反射

定义：简单的来说，反射机制指的是程序在**运行时**能够获取自身的信息。在java中，只要给定完整的类名（包名+类名）、或根据类的一个对象的引用,就可以通过反射机制来获得类的所有信息。

1.反射机制允许程序在执行期借助于ReflectionAPI取得任何类的内部信息(比如成员变量，构造器，成员方法等等)，并能操作对象的属性及方法。反射在设计模式和框架底层都会用到
2.加载完类之后，在堆中就产生了一个Class类型的对象(一个类只有一个Class对象) ,这个对象包含了类的完整结构信息。通过这个对象得
到类的结构。这个Class对象就像一面镜子，透过这个镜子看到类的结构，所以，形象的称之为:反射

[参考]: https://blog.csdn.net/gislaozhang/article/details/78758245

反射可以完成：

1.在运行时判断任意一个对象所属的类
2.在运行时构造任意一个类的对象
3.在运行时得到任意一个类所具有的成员变量和方法
4.在运行时调用任意一个对象的成员变量和方法
5.生成动态代理

反射优缺点：

1.优点:可以动态的创建和使用对象(也是框架底层核心)，使用灵活，没有反射机制，框架技术就失去底层支撑。
2.缺点:使用反射基本是解释执行，对执行速度有影响.

相关方法：

Class类：

1. getName:获取全类名
2. getSimpleName:获取简单类名
3. getFields:获取所有public修饰的属性， 包含本类以及父类的
4. getDeclaredFields:获取本类中所有属性
5. getMethods:获取所有public修饰的方法，包含本类以及父类的
6. getDeclaredMethods:获取本类中所有方法
7. getConstructors:获取本类所有public修饰的构造器
8. getDeclaredConstructors:获取本类中所有构造器
9. getPackage:以Package形式返回包信息
10. getSuperClass:以Class形式返回父类信息
11. getInterfaces:以Class[]形式返回接口信息
12. getAnnotations:以Annotation[]形式返回注解信息

Method类：

1. getModifiers:以int形式返回修饰符
    [说明:默认修饰符是0，public 是1 , private是2，protected是4,
    static是8 , final 是16]
2. getReturnType:以Class形式获取 返回类型
3. getName:返回方法名
4. getParameterTypes:以Class[]返回参数类型数组

Field类：

1. getModifiers:以int形式返回修饰符
    [说明:默认修饰符是0，public 是1 , private是2 , protected是4,
    static是8 , final 是16] , public(1) + static (8) = 9
2. getType:以Class形式返回类型
3. getName:返回属性名

Constructor类：

​	getModifiers:以int形式返回修饰符

​	getName:返回构造器名(全类名)

​	getParameterTypes:以Class[]返回参数类型数组

获取类方式：

```
Class c1 = Code.class; 这说明任何一个类都有一个隐含的静态成员变量class，这种方式是通过获取类的静态成员变量class得到的
Class c2 = code1.getClass(); code1是Code的一个对象，这种方式是通过一个类的对象的getClass()方法获得的 
Class c3 = Class.forName("com.example.gislaozhang.Code"); 这种方法是Class类调用forName方法，通过一个类的全量限定名获得
ClassLoader c4 =对象.getClass().getClassLoader(;
Class clazz4 = c4.loadClass( "类的全类名”);
```



获取方法：

```

// 获取所有方法
Method[] allMethods = studentClass.getMethods();
Method allMethod;
// 获取特定方法
try {
    allMethod = studentClass.getMethod("answer");
} catch (NoSuchMethodException e) {
    throw e;
}

// 获取所有本类定义的方法
Method[] methods = studentClass.getDeclaredMethods();
Method method;
try {
    method = studentClass.getDeclaredMethod("answer");
} catch (NoSuchMethodException e) {
    throw e;
}
```

获取属性：

```
// 获取所有字段
Field[] allFields = studentClass.getFields();
Field allField;
try {
    allField = studentClass.getField("name");
} catch (NoSuchFieldException e) {
    throw e;
}

// 获取本类定义的字段
Field[] fields = studentClass.getDeclaredFields();
Field field;
try {
    field = studentClass.getDeclaredField("age");
} catch (NoSuchFieldException e) {
    throw e;
}
```

获取构造方法：

```
// 获取特定构造器
Constructor allConstructor;
try {
    allConstructor = studentClass.getConstructor(String.class, int.class, int.class);
} catch (NoSuchMethodException e) {
    throw e;
}

// 获取所有构造器
Constructor[] constructors = studentClass.getDeclaredConstructors();
// 获取特定构造器
Constructor constructor;
try {
     constructor = studentClass.getDeclaredConstructor(String.class);
} catch (NoSuchMethodException e) {
    throw e;
}

```

暴力（关闭访问调查）：

1. Method和Field、 Constructor对象都有setAccessible(方法
2. setAccessible作用是启动和禁用访问安全检查的开关
3. 参数值为true表示反射的对象在使用时取消访问检查，提高反射的效率。参数值为false则表示反射的对象执行访问检查

```tsx
1.根据属性名获取Field对象
Field f = clazz对象.getDeclaredField(属性名);
2.暴破: f.setAccessible(true); //f是Field
3.访问
f.set(o,值); /。表示对象
syso(f.get(o));//o表示对象
4.
注意:如果是静态属性，则set和get中的参数o,可以写成null
constructor.setAccessible(true);   暴力反射，设置获取私有成员变量方法
Object obj = constructor.newInstance("lkxiaolou");
// 执行方法
String str = (String) method.invoke(obj);


public class ReflecAccessProperty {
public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InstantiationException, NoSuchFieldException {
//1. 得到 Student 类对应的 Class 对象
Class<?> stuClass = Class.forName("com.hspedu.reflection.Student");
//2. 创建对象
Object o = stuClass.newInstance();//o 的运行类型就是 Student
System.out.println(o.getClass());//Student
韩顺平循序渐进学 Java 零基础
第 951页
//3. 使用反射得到 age 属性对象
Field age = stuClass.getField("age");
age.set(o, 88);//通过反射来操作属性
System.out.println(o);//
System.out.println(age.get(o));//返回 age 属性的值
//4. 使用反射操作 name 属性
Field name = stuClass.getDeclaredField("name");
//对 name 进行暴破, 可以操作 private 属性
name.setAccessible(true);
//name.set(o, "老韩");
name.set(null, "老韩~");//因为 name 是 static 属性，因此 o 也可以写出 null
System.out.println(o);
System.out.println(name.get(o)); //
System.out.println(name.get(null));//获取属性值, 要求 name 是 static
}
}
class Student {//类
public int age;
private static String name;
public Student() {//构造器
}
韩顺平循序渐进学 Java 零基础
第 952页
public String toString() {
return "Student [age=" + age + ", name=" + name + "]";
}
}


```

**反射应用**

写框架（配置文件+反射）

测试类：

```
//1、加载配置文件
        //1.1、创建对象
        Properties p =new Properties();
        //1.2、加载配置文件，转换为一个集合
        //1.2.1、获取class目录下的配置文件
        ClassLoader classLoader = ReflectTest.class.getClassLoader();//使用类加载器找到配置文件（路径）
        InputStream is = classLoader.getResourceAsStream("cn/itcast/pro.properties");  //获取配置文件字节流
        p.load(is);
//2、获取配置文件中定义的数据
        String classname=p.getProperty("classname");
        String method=p.getProperty("method");
        //3、加载类进内存
        Class cls=Class.forName(classname);
        //4、创建对象
        Object obj=cls.newInstance();
        //5、获取方法对象
        Method mth = cls.getMethod(method);
        //6、执行方法
        mth.invoke(obj);
```

配置文件pro.properties

```tex
classname=cn.itcast.reflect.Student
method=sleep
```

# 注解

定义：注解（Annotation），也叫元数据。一种代码级别的说明。它是JDK1.5及以后版本引入的一个特性，与类、接口、枚举是在同一个层次。它可以声明在包、类、字段、方法、局部变量、方法参数等的前面，用来对这些元素进行说明，注释。

作用分类：

①编写文档：通过代码里标识的元数据生成文档【生成文档doc文档】

② 代码分析：通过代码里标识的元数据对代码进行分析【使用反射】

③编译检查：通过代码里标识的元数据让编译器能够实现基本的编译检查【Override】

***JDK中常用注解***

​	@Override:检测被该注解标记的方法是否继承父类（接口）的

​	@Deprecated：该注解标识的内容表示已过时

​	@Suppresswarning:压制警告    			一般为@Suppresswarning（“all")

***自定义注解***

​	*格式*：

​		元注解

​		public @interface 注解名称{

​				属性列表

​			}

​	*本质*：本质就是一个接口，该接口默认继承Annotation接口

​	*属性*：接口中的抽象方法

​				要求：

​							1、属性的返回值类型有一下取值

​									*基本数据类型*

​									*String*

​									*枚举*

​									*注解*

​									*以上数据类型的数组*

​							2、定义了属性，在使用时需要给属性赋值

​									*定义属性时使用了default赋初始值，则使用注解时不需要赋值*

​									*只需给一个属性赋值时，并且属性名称时value，则可以省略名称，直接赋值*

​									*给数组赋值时要加{}，若只有一个值，可省略*

​	*元注解*：用于描述注解的注解

​			@Target：描述注解能够作用的位置      @Target（ElementType.METHOD）作用于方法上，.Type,类，.Field,成员变量

​			@Retention：描述注解被保留的阶段 		@Retention(RetentionPolicy.RUNTIME) 表示该注解可保留到class字节码中被jvm读取

​			@Documented：描述该注解是否被抽到api文档中

​			@Inherited：描述注解是否被子类继承

​	使用注解：获取注解中定义的属性值             可用于替代配置文件

​			获取注解定义的位置的对象

​			获取指定注解

​			调用注解中的抽象方法	获取配置的属性值

```java
/**
 * 使用注解来代替配置文件
 */
@ReflectAnnot(classname = "cn.itcast.annotation.ReflectDemo",method = "sleep")
public class ReflectTest {
    public static void main(String[] args) throws Exception {
        //1、解析注解
        //1.1、获取该类字节码文件对象
        Class<ReflectTest> reflectTest=ReflectTest.class;
        //2、获取该类上方注解对象
        //其实是在内存中生成一个子类来实现注释接口
        ReflectAnnot an = reflectTest.getAnnotation(ReflectAnnot.class);
        //3、调用其中的抽象方法获取返回值
        String classname=an.classname();
        String method=an.method();
        // 加载类进内存
        Class cls=Class.forName(classname);
        //4、创建对象
        Object obj=cls.newInstance();
        //5、获取方法对象
        Method mth = cls.getMethod(method);
        //6、执行方法
        mth.invoke(obj);
    }
}
```



# 数据库（mysql)

数据库的基本概念

	1. 数据库的英文单词： DataBase 简称 ： DB
	2. 什么数据库？
		* 用于存储和管理数据的仓库。
	
	3. 数据库的特点：
		1. 持久化存储数据的。其实数据库就是一个文件系统
		2. 方便存储和管理数据
		3. 使用了统一的方式操作数据库 -- SQL

MySQL数据库软件

	1. 安装
		* 参见《MySQL基础.pdf》
	2. 卸载
		1. 去mysql的安装目录找到my.ini文件
			* 复制 datadir="C:/ProgramData/MySQL/MySQL Server 5.5/Data/"
		2. 卸载MySQL
		3. 删除C:/ProgramData目录下的MySQL文件夹。
		
	3. 配置
		* MySQL服务启动
			1. 手动。
			2. cmd--> services.msc 打开服务的窗口
			3. 使用管理员打开cmd
				* net start mysql : 启动mysql的服务
				* net stop mysql:关闭mysql服务
		* MySQL登录
			1. mysql -uroot -p密码
			2. mysql -hip -uroot -p连接目标的密码
			3. mysql --host=ip --user=root --password=连接目标的密码
			连接到Mysql服务(Mysq|数据库)的指令
				mysql -h主机IP -P端口-u用户名-p密码
			老师提醒:
			(1)-p密码不要有空格
			(2)-p后面没有写密码，回车会要求输入密码
			(3)如果没有写-h主机，默认就是本机
			(4)如果没有写-P端口，默认就是3306
			(5)在实际工作中,3306一般修改
		* MySQL退出
			1. exit
			2. quit
	
		* MySQL目录结构
			1. MySQL安装目录：basedir="D:/develop/MySQL/"
				* 配置文件 my.ini
			2. MySQL数据目录：datadir="C:/ProgramData/MySQL/MySQL Server 5.5/Data/"
				* 几个概念
					* 数据库：文件夹
					* 表：文件
					* 数据：数据

## SQL

1.什么是SQL？
	Structured Query Language：结构化查询语言
	其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。
	
2.SQL通用语法

	1. SQL 语句可以单行或多行书写，以分号结尾。
	2. 可使用空格和缩进来增强语句的可读性。
	3. MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写。
	4. **3 种注释**
		* **单行注释: -- 注释内容 或 # 注释内容(mysql 特有)** 
		* **多行注释: /* 注释 */**

3. SQL分类
	1) DDL(Data Definition Language)数据定义语言
		用来定义数据库对象：数据库，表，列等。关键字：create, drop,alter 等
	2) DML(Data Manipulation Language)数据操作语言
		用来对数据库中表的数据进行增删改。关键字：insert, delete, update 等
	3) DQL(Data Query Language)数据查询语言
		用来查询数据库中表的记录(数据)。关键字：select, where 等
	4) DCL(Data Control Language)数据控制语言(了解)
		用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT， REVOKE 等



## 常用数据类型

在满足需求的条件下尽量选择占用空间小的 	

| 分类             | 数据类型                     | 说明                                                         |
| :--------------- | ---------------------------- | ------------------------------------------------------------ |
| 数值类型[]       | BIT(M)                       | 位类型。M指定位数，默认值1，范围1-64                         |
| 数值类型         | TINYINT[UNSIGNED]占1个字节   | 带符号的范围是-128到127。无符号0到255。默认是有符号          |
| 数值类型         | SMALLINT[UNSIGNED]占2个字节  | 带符号是负的2^15到2^15-1 ,无符号0到2^16 -1                   |
| 数值类型         | MEDIUMINT[UNSIGNED]占3个字节 | 带符号是负的2^23到2^23-1无符号0到2^24-1                      |
| 数值类型         | INT[UNSIGINED]占4个字节      | 带符号是负的2^31 到2^31-1，无符号0到2^32 -1                  |
| 数值类型         | BIGINT[UNDIGNED]占8个字节    | 带符号是负的2^63到2^63-1，无符号0到2^64-1                    |
| 数值类型         | FLOAT[UNSIGNED]              | 占用空间4个字节                                              |
| 数值类型         | DOUBLE[UNSIGNED]             | 表示比float精度更大的小数，占用空间8个字节                   |
| 数值类型         | DECIMAL(M,D)[UNSIGNED]       | 定点数M指定长度，D表示小数点的位数，                         |
| 文本、二进制类型 | CHAR(size)  char(20)         | 固定长度字符串最大255                                        |
| 文本、二进制类型 | VARCHAR(size) varchar(20)    | 可变长度字符串0~65535 [即: 2^16-1]                           |
| 文本、二进制类型 | BLOB      LONGBLOB           | 二进制数据BLOB 0~2^16-1 LONGBLOB 0~2^32-1                    |
| 文本、二进制类型 | TEXT        LONGTEXT         | 文本Text 0~2^16 LONGTEXT 0~2^32                              |
| 日期类型         | DATE/DATETIME/TimeStamp      | 日期类型(YYYY-MM-DD) (YYYY-MM-DD HH:MM:SS),TimeStamp表示时间戳，它可用于自动记录insert、update操作的时间 |

使用细节：

**数值型(bit)的使用**
1.基本使用
mysq|> create table t05 (num bit(8));
mysql> insert into t05 (1, 3);
mysql> insert into t05 values(2, 65);
2.细节说明bit.sql
bit字段显示时，按照位的方式显示.
查询的时候仍然可以用使用添加的数值
**如果一个值只有0, 1可以考虑使用bit(1) ,可以节约空间**
位类型。M指定位数，默认值1,范围1-64
使用不多.

 **数值型(小数)的基本使用**

1. FLOAT/DOUBLE [UNSIGNED]
    CREATE TABLE t3 (ml FLOAT ，n2 DOUBLE ，n3 DECIMAL (30, 20);
    INSERT INTO t3
    VALUES 188 .12345678912345，88 .12345678912345，88 .123456781
    Float单精度精度，Double 双精度.
    SELECT . FROM t3:

2. DECIMAL[M,D] [UNSIGNED]
可以支持更加精确的小数位。M是小数位数(精度)的总数，D是小数点(标度)后面的位数。
**如果D是0，则值没有小数点或分数部分。M最大65。D最大是30。如果D被省略，默认是0。 如果M被省略，默认是10。**
建议:如果**希望小数的精度高，推荐使用decimal**



 **字符串的基本使用**

CHAR(size)
固定长度字符串最大255字符
VARCHAR(size) 0~65535
可变长度字符串最大65532字节[utf8编码最大21844字符 1-3个字节用于记录大小]

char(4) //这个4表示字符数(最大255), 不是字节数,不管是中文还是字母**都是放四个**,按字符计算.
varchar(4)//这个4表示字符数,不管是字母还是中文都以定义好的表的编码来存放数据不管是中文还是英文字母，都是**最多存放4个**，是按照字符来存放的.

char(4)是定长(固定的大小)，就是说，即使你插入'aa' ,也会占用分配的4个字符的空间.
varchar(4)是变长(变化的大小)，就是说，如果你插入了'aa',实际占用空间大小并不是4个字符，而是按照实际占用空间来分配(老韩说明:
varchar本身还需要占用1-3个字节来记录存放内容长度) L(实际数据大小)(1-3)字节

**什么时候使用 char ,什么时候使用varchar**
1.如果数据是定长，推荐使用char,比如md5的密码,邮编，手机号，身份证号码等. char(32)
2.如果个字段的长度是不确定，我们使用varchar，比如留言文章
查询速度: char > varchar

在存放文本时，也可以使用Text数据类型.可以将TEXT列视为VARCHAR列，注意Text不能有默认值.大小0-2^16字节
如果希望存放更多字符，可以选择MEDIUMTEXT 0-2^24或者LONGTEXT 0~2^32



 **日期类型的基本使用**

```
#演示时间相关的类型
#创建一张表, date , datetime , timestamp
CREATE TABLE t14 (
birthday DATE , -- 生日
job_time DATETIME, -- 记录年月日 时分秒
login_time TIMESTAMP
NOT NULL DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP); -- 登录时间, 如果希望 login_time 列自动更新, 需要配置
SELECT * FROM t14;
INSERT INTO t14(birthday, job_time)
VALUES('2022-11-11','2022-11-11 10:10:10'); -- 如果我们更新 t14 表的某条记录，login_time 列会自动的以当前时间进行更新
```

## 常用函数

### 窗口函数

窗口函数又名开窗函数，属于分析函数的一种。用于解决复杂报表统计需求的功能强大的函数。窗口函数用于计算基于组的某种聚合值，它和聚合函数的不同之处是：对于每个组返回多行，而聚合函数对于每个组只返回一行。
开窗函数指定了分析函数工作的数据窗口大小，这个数据窗口大小可能会随着行的变化而变化。

```text
<窗口函数> over (partition by <用于分组的列名>
                order by <用于排序的列名>)
```

<窗口函数>的位置，可以放以下两种函数：

1） 专用窗口函数，比如rank, dense_rank, row_number等

2） 聚合函数，如sum. avg, count, max, min等

**2.窗口函数有以下功能：**

1）同时具有分组（partition by）和排序（order by）的功能

2）不减少原表的行数，所以经常用来在每组内排名

**3.注意事项**

窗口函数原则上只能写在select子句中

**4.窗口函数使用场景**

1）业务需求“**在每组内排名”**，比如：

> 排名问题：每个部门按业绩来排名
> topN问题：找出每个部门排名前N的员工进行奖励



**Count返回行的总数**

Select count (*) | count (列名) from table_ name
[WHERE where defini tion]

**Sum函数返回满足where条件的行的和-一般使用在数值列**
Select sum(列名) { ,sum (列名...} from tablename
[WHERE where definition]

**AVG函数返回满足where条件的一列的平均值**
Select avg(列名) {,avg(列名...} from tablename
[WHERE where defini tion]

**Max/min函数返回满足where条件的一列的最大/最小值**
Select max (列名)
from tablename
[WHERE where defini tion]

### **字符串相关函数**

CHARSET(str)		返回字串字符集
CONCAT (string2 [... ])	连接字串
INSTR (string ,substring )	返回substring在string中出现的位置，没有返回0
UCASE (string2 )	转换成大写
LCASE (string2 )	转换成小写
LEFT (string2 ,length )	从string2中的左边起取length个字符
LENGTH (string )	string长度[按照字节]
REPLACE (str ,search_ str,replace_ str )	在str中用replace_ str 替换search_ _str
STRCMP (string1 ,string2 )	逐字符比较两字串大小，
SUBSTRING (str ，position [,length]	从str的position开始[从1开始计算] ,取length个字符

substring_index(FIELD, sep, n)可以将字段FIELD按照sep分隔：

​	(1).当n大于0时取第n个分隔符(n从1开始)左边的全部内容；

​	(2).当n小于0时取倒数第n个分隔符(n从-1开始)右边的全部内容

LTRIM (string2 ) RTRIM (string2 )	去除前端空格或后端空格
trim

### **数学相关函数**

ABS(uum)	绝对值
BIN (decimal_ number )	十进制转二进制
CEILING (number2 )	向上取整，得到比num2大的最小整数
CONV(number2,from_ base,to_ base)	进制转换
FLOOR (number2 )	向下取整，得到比num2小的最大整数
FORMAT (number,decimal places )	保留小数位数
HEX (DecimalNumber )	转十六进制
LEAST (number , number2 [..])	求最小值
MOD (numerator ,denominator )	求余
RAND([seed])	RAND([seed])其范围为0≤vS1.0 

### **时间日期相关函数**  dual 虚拟表

CURRENT_ DATE ( )	当前日期
CURRENT_ TIME ( )	当前时间
CURRENT TIMESTAMP( )	当前时间戳
DATE (datetime )	返回datetime的日期部分
DATE_ ADD (date2，INTERVAL d_ _value d_ type )	在date2中加上口期或时间
DATE SUB (date2 , INTERVAL d_ value d_ type )	在date2上减去-一个时间
DATEDIFF (date1 ,date2 )	两个日期差(结果是天)
TIMEDIFF(date1,date2)	两个时间差(多少小时多少分钟多少秒)
NOW()	当前时间
YEAR|Month IDAY (datetime )	年月日
FROM_ UNIXTIME( )  select unix timestamp( (返回1 970-1-1到现在的秒数): from unixtime

### **加密和系统函数**

USER(）查询用户
DATABASE()	数据库名称
MD5(str)	为字符串算出一个MD5 32的字符串，(用户密码)加密
PASSWORD(str)	从原文密码str计算并返回密码字符串,通常用于对mysql数据库的用户密码加密
select * from mysql.user \G

### **流程控制函数**（注意）

IF(expr1,expr2,expr3)	如果expr1为True，则返回expr2否则返回expr3
IFNULL(expr1,expr2) 如果expr1不为空NULL则返回expr1,否则返回expr2 
SELECT CASE WHEN expr1 THEN expr2 WHEN expr3 THEN expr4 ELSE expr5 END; [类似多重分支.] 	如果expr1为TRUE,则返回expr2,如果expr2 为t,返回expr4,否则返回expr5

```
CASE函数
是一种多分支的函数，可以根据条件列表的值返回多个可能的结果表达式中的一个。
可用在任何允许使用表达式的地方，但不能单独作为一个语句执行。
分为：
简单CASE函数
搜索CASE函数

简单 CASE函数
CASE 测试表达式
WHEN 简单表达式1 THEN 结果表达式1
WHEN 简单表达式2 THEN 结果表达式2 …
WHEN 简单表达式n THEN 结果表达式n
[ ELSE 结果表达式n+1 ]
END
计算测试表达式，按从上到下的书写顺序将测试表达式的值与每个WHEN子句的简单表达式进行比较。
如果某个简单表达式的值与测试表达式的值相等，则返回第一个与之匹配的WHEN子句所对应的结果表达式的值。
如果所有简单表达式的值与测试表达式的值都不相等，
若指定了ELSE子句,则返回ELSE子句中指定的结果表达式的值；
若没有指定ELSE子句，则返回NULL。

例48. 查询班级表中的学生的班号、班名、系号和班主任号，并对系号作如下处理：
当系号为1时，显示 “计算机系”；
当系号为2时，显示 “软件工程系”；
当系号为3时，显示 “物联网系”。

SELECT 班号 ,班名,
CASE 系号
WHEN 1 THEN '软件工程系'
WHEN 2 THEN '计算机系'
WHEN 3 THEN '物联网系'
END AS 系号,班主任号
FROM 班级表
搜索CASE函数

CASE
WHEN 布尔表达式1 THEN 结果表达式1
WHEN 布尔表达式2 THEN 结果表达式2 …
WHEN 布尔表达式n THEN 结果表达式n
[ ELSE 结果表达式n+1 ]
END
按从上到下的书写顺序计算每个WHEN子句的布尔表达式。
返回第一个取值为TRUE的布尔表达式所对应的结果表达式的值。
如果没有取值为TRUE的布尔表达式，
则当指定了ELSE子句时,返回ELSE子句中指定的结果；
如果没有指定ELSE子句，则返回NULL。

SELECT 班号 ,班名,
CASE
WHEN 系号=1 THEN '软件工程系'
WHEN 系号=2 THEN '计算机系'
WHEN 系号=3 THEN '物联网系'
END AS 系号,班主任号
FROM 班级表

将case查询的结果作为一个新表
```



## DDL:操作数据库、表

```mysql
1. 操作数据库：CRUD
	1. C(Create):创建
		* 创建数据库：
			* create database 数据库名称;
		* 创建数据库，判断不存在，再创建：
			* create database if not exists 数据库名称;
		* 创建数据库，并指定字符集
			* create database 数据库名称 character set 字符集名;
			#创建一个使用 utf8 字符集，并带校对规则的 hsp_db03 数据库
			CREATE DATABASE hsp_db03 CHARACTER SET utf8 COLLATE utf8_bin
			#校对规则 utf8_bin 区分大小 默认 utf8_general_ci 不区分大小写

		* 练习： 创建db4数据库，判断是否存在，并制定字符集为gbk
			* create database if not exists db4 character set gbk;
	2. R(Retrieve)：查询
		* 查询所有数据库的名称:
			* show databases;
		* 查询某个数据库的字符集:查询某个数据库的创建语句
			* show create database 数据库名称;
	3. U(Update):修改
		* 修改数据库的字符集
			* alter database 数据库名称 character set 字符集名称;
	4. D(Delete):删除
		* 删除数据库
			* drop database 数据库名称;
		* 判断数据库存在，存在再删除
			* drop database if exists 数据库名称;
	5. 使用数据库
		* 查询当前正在使用的数据库名称
			* select database();
		* 使用数据库xs  oo
			* use 数据库名称;
	6.备份还原数据库
	30
	
		#备份, 要在 Dos 下执行 mysqldump 指令其实在 mysql 安装目录\bin
		#这个备份的文件，就是对应的 sql 语句
		mysqldump -u root -p -B hsp_db02 hsp_db03 > d:\\bak.sql
		#恢复数据库(注意：进入 Mysql 命令行再执行)
		source d:\\bak.sql
	7.备份数据库表
	mysqldump -u用户名-p密码数据库表1表2表n > d:\文件名.sqI
```

```mysql
2. 操作表
    1. C(Create):创建
        1. 语法：
            create table 表名(
            	列名1 数据类型1,
            	列名2 数据类型2,
            	....
            	列名n 数据类型n
            );  )character set字符集 collate校对规则engine存储引擎
			character set :如不指定则为所在数据库字符集
			collate:如不指定则为所在数据库校对规则
			engine:引擎(这个涉及内容较多，后面单独讲解)
			
            * 注意：最后一列，不需要加逗号（,）
            * 数据库类型：
                1. int：整数类型
                    * age int,
                2. double:小数类型
                    * score double(5,2)
                3. date:日期，只包含年月日，yyyy-MM-dd
                4. datetime:日期，包含年月日时分秒	 yyyy-MM-dd HH:mm:ss
                5. timestamp:时间错类型	包含年月日时分秒	 yyyy-MM-dd HH:mm:ss	
                    * 如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值

                6. varchar：字符串
                    * name varchar(20):姓名最大20个字符
                    * zhangsan 8个字符  张三 2个字符

  * 创建表
    		create table student(
    			id int,
    			name varchar(32),
    			age int ,
    			score double(4,1),
    			birthday date,
    			insert_time timestamp
    		);

     * 复制表：
         * create table 表名 like 被复制的表名;	  	
     * 复制记录
        先把 emp 表的记录复制到 my_tab01
		INSERT INTO my_tab01
		(id, `name`, sal, job,deptno)
		SELECT empno, ename, sal, job, deptno FROM emp;

    2. R(Retrieve)：查询
        * 查询某个数据库中所有的表名称
            * show tables;
        * 查询表结构
            * desc 表名;
    3. U(Update):修改
        1. 修改表名
            alter table 表名 rename to 新的表名;
        2. 修改表的字符集
            alter table 表名 character set 字符集名称;
        3. 添加一列
            alter table 表名 add 列名 数据类型 [not null default '']; 不为空，默认空串
        4. 修改列名称 类型
            alter table 表名 change column 列名 新列名 新数据类型;
            **alter table 表名 modify 列名 新数据类型;**
        5. 删除列
            alter table 表名 drop 列名;
    4. D(Delete):删除
        * drop table 表名;
        * drop table  if exists 表名 ;
```


## DML：增删改表中数据

```mysql
1. 添加数据：
	* 语法：
		* insert into 表名(列名1,列名2,...列名n) values(值1,值2,...值n)[,(值1,值2,...值n),(值1,值2,...值n)];
	* 注意：
		1. 列名和值要一一对应。
		2. 如果表名后，不定义列名，则默认给所有列添加值
			insert into 表名 values(值1,值2,...值n);
		3. 除了数字类型，其他类型需要使用引号(单双都可以)引起来
2. 删除数据：
	* 语法：
		* delete from 表名 [where 条件]
	* 注意：
		1. 如果不加条件，则删除表中所有记录。
		2. 如果要删除所有记录
			1. delete from 表名; -- 不推荐使用。有多少条记录就会执行多少次删除操作
			2. TRUNCATE TABLE 表名; -- 推荐使用，效率更高 先删除表，然后再创建一张一样的表。
3. 修改数据：
	* 语法：
		* update 表名 set 列名1 = 值1, 列名2 = 值2,... [where 条件];

	* 注意：
		1. 如果不加任何条件，则会将表中所有记录全部修改。
```



## DQL：查询表中的记录

```mysql
* select * from 表名;

1. 语法：
    select
    	字段列表
    from
    	表名列表
    where
    	条件列表
    group by
    	分组字段
    having
    	分组之后的条件
    order by
    	排序
    limit 起始位置，条数
    	分页限定
    limit:
    LIMIT 子句可以被用于强制 SELECT 语句返回指定的记录数。
	LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。
如果只给定一个参数，它表示返回最大的记录行数目。
如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。
为了检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数为 -1。
初始记录行的偏移量是 0(而不是 1)。
    select device_id from user_profile limit 0,2---运行效率更高

	select device_id from user_profile limit 2 ---运行效率低

	也可结合 limit offset： 一起使用时，limit表示要取的数量，offset表示跳过的数量

	select device_id from user_profile limit 2 offset 0 // 跳过0条，从第一条数据开始取，取两条数据 ---运行效率

2. 基础查询
    1. 多个字段的查询
        select 字段名1，字段名2... from 表名；
        * 注意：
            * 如果查询所有字段，则可以使用*来替代字段列表。
    2. 去除重复：
        * distinct
    3. 计算列
        * 一般可以使用四则运算计算一些列的值。（一般只会进行数值型的计算）
        * ifnull(表达式1,表达式2)：null参与的运算，计算结果都为null
            * 表达式1：哪个字段需要判断是否为null
            * 如果该字段为null后的替换值。
    4. 起别名：
        * as：as也可以省略

3. 条件查询

    1. where子句后跟条件

    2. 运算符

        * > 、< 、<= 、>= 、= 、<>

        * BETWEEN...AND  

        * IN( 集合)  not in

        * LIKE：模糊查询

            * 占位符：
                * _:单个任意字符
                * %：多个任意字符

        * IS NULL  

        * and  或 &&

        * or  或 || 

        * not  或 !

            -- 查询年龄大于20岁

            SELECT * FROM student WHERE age > 20;

            SELECT * FROM student WHERE age >= 20;

            -- 查询年龄等于20岁
            SELECT * FROM student WHERE age = 20;

            -- 查询年龄不等于20岁
            SELECT * FROM student WHERE age != 20;
            SELECT * FROM student WHERE age <> 20;

            -- 查询年龄大于等于20 小于等于30

            SELECT * FROM student WHERE age >= 20 &&  age <=30;
            SELECT * FROM student WHERE age >= 20 AND  age <=30;
            SELECT * FROM student WHERE age BETWEEN 20 AND 30;

            -- 查询年龄22岁，18岁，25岁的信息
            SELECT * FROM student WHERE age = 22 OR age = 18 OR age = 25
            SELECT * FROM student WHERE age IN (22,18,25);

            -- 查询英语成绩为null
            SELECT * FROM student WHERE english = NULL; -- 不对的。null值不能使用 = （!=） 判断

            SELECT * FROM student WHERE english IS NULL;

            -- 查询英语成绩不为null
            SELECT * FROM student WHERE english  IS NOT NULL;
            
			-- 查询姓马的有哪些？ like
			SELECT * FROM student WHERE NAME LIKE '马%';
			-- 查询姓名第二个字是化的人
			
			SELECT * FROM student WHERE NAME LIKE "_化%";
			
 		    -- 查询姓名是3个字的人
			SELECT * FROM student WHERE NAME LIKE '___';

			-- 查询姓名中包含德的人
			SELECT * FROM student WHERE NAME LIKE '%德%';
			

```

## DQL:查询语句

```mysql
1. 排序查询
    * 语法：order by 子句
        * order by 排序字段1 排序方式1 ，  排序字段2 排序方式2...

    * 排序方式：
        * ASC：升序，默认的。
        * DESC：降序。

    * 注意：
        * 如果有多个排序条件，则当前边的条件值一样时，才会判断第二条件。

2. 聚合函数：将一列数据作为一个整体，进行纵向的计算。
    1. count：计算个数
        1. 一般选择非空的列：主键
        2. count(*)
    2. max：计算最大值
    3. min：计算最小值
    4. sum：计算和
    5. avg：计算平均值

 * 注意：聚合函数的计算，排除null值。
    	解决方案：
      		1. 选择不包含非空的列进行计算
            	2. IFNULL函数

3. 分组查询:

    1. 语法：group by 分组字段；

    2. 注意：

        1. 分组之后查询的字段：分组字段、聚合函数
        2. where 和 having 的区别？
            1. where 在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
            2. where 后不可以跟聚合函数，having可以进行聚合函数的判断。

        -- 按照性别分组。分别查询男、女同学的平均分

        SELECT sex , AVG(math) FROM student GROUP BY sex;

        -- 按照性别分组。分别查询男、女同学的平均分,人数

        SELECT sex , AVG(math),COUNT(id) FROM student GROUP BY sex;

        --  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组
        SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex;

        --  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组,分组之后。人数要大于2个人
        SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;

        SELECT sex , AVG(math),COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex HAVING 人数 > 2;


			

4. 分页查询

    1. 语法：limit 开始的索引,每页查询的条数;

    2. 公式：开始的索引 = （当前的页码 - 1） * 每页显示的条数
        -- 每页显示3条记录 

        SELECT * FROM student LIMIT 0,3; -- 第1页

        SELECT * FROM student LIMIT 3,3; -- 第2页

        SELECT * FROM student LIMIT 6,3; -- 第3页

    3. limit 是一个MySQL"方言"
```



## 约束

* ```mysql
    * 概念： 对表中的数据进行限定，保证数据的正确性、有效性和完整性。	
    * 分类：
        1. 主键约束：primary key
        2. 非空约束：not null
        3. 唯一约束：unique
        4. 外键约束：foreign key
        5.check:
        	用于强制行数据必须满足的条件,假定在sal列上定义了check约束,并
    		要求sal列值在1000 ~ 2000之间如果不再1000 ~ 2000之间就会提示出错。
    		 oracle 和sql server均支持check ,但是mysql5.7目前还不支持check ,只做语法校验，但不会生效。
    		 基本语法:列名类型 check (check条件)
    		user表
    		id, name, sex(man,woman), sal(大于100小于900)
    		在mysql中实现check的功能，- 般是在程序中控制，或者通过触发器完成。
    * 主键约束：primary key。
        1. 注意：
            1. 含义：非空且唯一
            2. 一张表只能有一个字段为主键
            3. 主键就是表中记录的唯一标识
    
        2. 在创建表时，添加主键约束
            create table stu(
            	id int primary key,-- 给id添加主键约束
            	name varchar(20)
                或者 primary key(id)
            );
    
        3. 删除主键
            -- 错误 alter table stu modify id int ;
            ALTER TABLE stu DROP PRIMARY KEY;
    
        4. 创建完表后，添加主键
            ALTER TABLE stu MODIFY id INT PRIMARY KEY;
    
        5. 自动增长：
            1.  概念：如果某一列是数值类型的，使用 auto_increment 可以来完成值得自动增长
    				修改自增长，改变从默认值1开的增长  alter table 表名 auto_increment = 新开始的值
            2.  在创建表时，添加主键约束，并且完成主键自增长
                create table stu(
                id int primary key auto_increment,-- 给id添加主键约束
                name varchar(20)
                );
    * 非空约束：not null，值不能为null
        1. 创建表时添加约束
            CREATE TABLE stu(
            	id INT,
            	NAME VARCHAR(20) NOT NULL -- name为非空
            );
        2. 创建表完后，添加非空约束
            ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;
    
        3. 删除name的非空约束
            ALTER TABLE stu MODIFY NAME VARCHAR(20);
    
    
    			
    
      		3. 删除自动增长
           	ALTER TABLE stu MODIFY id INT;
            	4. 添加自动增长
                ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;
    
    
    	
    
    * 唯一约束：unique，值不能重复
    
        1. 创建表时，添加唯一约束
            CREATE TABLE stu(
            	id INT,
            	phone_number VARCHAR(20) UNIQUE -- 添加了唯一约束
    
            );
    
            * 注意mysql中，唯一约束限定的列的值可以有多个null
    
    
    		
    
     2. 删除唯一约束
    
        	ALTER TABLE stu DROP INDEX phone_number;
    
        3. 在创建表后，添加唯一约束
            ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;
    
    * 外键约束：foreign key,让表于表产生关系，从而保证数据的正确性。
        1. 在创建表时，可以添加外键
            * 语法：
                create table 表名(
                	....
                	外键列
                	[constraint 外键名称 ]foreign key (外键列名称) references 主表名称(主表列名称)
                );
    
        2. 删除外键
            ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
    
        3. 创建表之后，添加外键
            ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
    
    
    ​		
    
     	4. 级联操作
          	1. 添加级联操作
              	语法：ALTER TABLE 表名 ADD CONSTRAINT 外键名称 
              			FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE  ;
              2. 分类：
                  1. 级联更新：ON UPDATE CASCADE 
                  2. 级联删除：ON DELETE CASCADE 
    ```

## 索引（优化数据库）

说起提高数据库性能，索引是最物美价廉的东西了。不用加内存，不用改程序，不用调sql,查询速度就可能提高百倍干倍。

**索引的原理**
没有索引为什么会慢?因为全表扫描.
使用索引为什么会快?形成一个索引的数据结构，比如二叉树
索引的代价
I. 磁盘占用
I. 对dml(update delete insert)语句的效率影响
老师告诉你， 在我们项目中，select[90%] 多还是update,delete,insert[10%]操作多?
**索引的类型**

1. 主键索引，主键自动的为主索引(类型Primary key)
2. 唯一索引(UNIQUE)
3. 普通索引(INDEX)
4. 全文索引(FULLTEXT) [适用于MyISAM]
    一般开发，不使用mysqI自带的全文索引，而是使用:全文搜索
    Solr和ElasticSearch (ES)
    create table t1 (
    id int primary key, --主键，同时也是索引，称为主键索引
    name varchar(32));
    create table t2(
    id int unique, - id是唯一 的，同时也是索引，称为unique索引.

**索引的使用**

1.添加索引(建小表测试id,name ) index use.sql
create [UNIQUE] index index name on tbl name
(col name [(length)
[ASC | DESC] , ....
alter table table name ADD INDEX [index name] (index col name...
2.
添加主键(索引) ALTER TABLE表名ADD PRIMARY KEY(列名.);
3.
删除索引
DROP INDEX index name ON tbl name;
alter table table name drop index index name;
4.删除主键索引 比较特别: alter table tb drop primary key;
5.查询索引(三种方式)
show index(es) from table name;
show keys from table name;
desc table Name;

**索引的适用**

如果某列的值，是不会重复的，则优先考虑使用 unique 索引, 否则使用普通索引

1.
较频繁的作为查询条件字段应该创建索引
select * from emp where empno = 1
2.
唯一性太差的字段不适合单独创建索引，即使频繁作为查询条件
select * from emp where sex = '男
3.
更新非常频繁的字段不适合创建索引
select * from emp where logincount = 1
4.
不会出现在WHERE子句中字段不该创建索引

```
-- 演示 mysql 的索引的使用
-- 创建索引
CREATE TABLE t25 (
id INT , `name` VARCHAR(32)); -- 查询表是否有索引
SHOW INDEXES FROM t25; -- 添加索引
-- 添加唯一索引
CREATE UNIQUE INDEX id_index ON t25 (id); -- 添加普通索引方式 1
CREATE INDEX id_index ON t25 (id); -- 如何选择

-- 1. 如果某列的值，是不会重复的，则优先考虑使用 unique 索引, 否则使用普通索引
-- 添加普通索引方式 2
ALTER TABLE t25 ADD INDEX id_index (id)
-- 添加主键索引
CREATE TABLE t26 (
id INT , `name` VARCHAR(32));
ALTER TABLE t26 ADD PRIMARY KEY (id)
SHOW INDEX FROM t25
-- 删除索引
DROP INDEX id_index ON t25
-- 删除主键索引
ALTER TABLE t26 DROP PRIMARY KEY
-- 修改索引 ， 先删除，在添加新的索引
-- 查询索引
-- 1. 方式
SHOW INDEX FROM t25
-- 2. 方式
SHOW INDEXES FROM t25
-- 3. 方式

SHOW KEYS FROM t25
-- 4 方式
DESC t2
```

## 数据库引擎

1. MySQL的表类型由存储引擎(Storage Engines)决定，主要包括MyISAM、
innoDB、Memory等。
2. MySQL 数据表主要支持六种类型，分别是: CSV、Memory, ARCHIVE、
MRG MYISAM、MYISAM、InnoBDB。
3. 这六种又分为两类，一类是”事务安全型”(transaction-safe),比如:
    InnoDB;其余都属于第二类，称为”非事务安全型”(non-transaction-
    safe)[mysiam和memory].

三种主要引擎：

1. MyISAM**不支持事务、也不支持外键，但其访问速度快，对事务完整性没有要求**

2. InnoDB存储引擎提供 了**具有提交、回滚和崩溃恢复能力的事务安全**。但是比起
    MyISAM存储引擎，InnoDB写的**处理效率差一些并且会占用更多的磁盘空间**以保留
    数据和索引。

3. MEMORY存储引擎**使用存在内存中的内容来创建表**。 每个MEMORY表只实际对应
    t个磁盘文件。MEMORY类型的表**访问非常得快**，因为它的数据是放在内存中的，
    并且**默认使用HASH索引**。但是**一旦MySQL服务关闭，表中的数据就会丢失掉，表的**
    **结构还在。**

  ```
  -- 表类型和存储引擎
  -- 查看所有的存储引擎
  SHOW ENGINES
  -- innodb 存储引擎，是前面使用过. -- 1. 支持事务 2. 支持外键 3. 支持行级锁
  -- myisam 存储引擎
  CREATE TABLE t28 (
  id INT, `name` VARCHAR(32)) ENGINE MYISAM
  -- 1. 添加速度快 2. 不支持外键和事务 3. 支持表级锁
  START TRANSACTION;
  SAVEPOINT t1
  
  INSERT INTO t28 VALUES(1, 'jack');
  SELECT * FROM t28;
  ROLLBACK TO t1
  -- memory 存储引擎
  -- 1. 数据存储在内存中[关闭了 Mysql 服务，数据丢失, 但是表结构还在]
  -- 2. 执行速度很快(没有 IO 读写) 3. 默认支持索引(hash 表)
  CREATE TABLE t29 (
  id INT, `name` VARCHAR(32)) ENGINE MEMORY
  DESC t29
  INSERT INTO t29
  VALUES(1,'tom'), (2,'jack'), (3, 'hsp');
  SELECT * FROM t29
  -- 指令修改存储引擎
  ALTER TABLE `t29` ENGINE = INNOD
  ```

  **引擎选择**

  1.如果你的应用不需要事务，处理的只是基本的CRUD操作，那么MyISAM
  是不二选择,速度快
  2.如果需要支持事务，选择InnoDB。

  3.Memory 存储引擎就是将数据存储在内存中，由于没有磁盘I./O的等待，
  速度极快。但由于是内存存储引擎，所做的任何修改在服务器重启后都将
  消失。(经典用法用户的在线状态().)

  **修改引擎**

  ALTER TABLE表名ENGINE =储存引擎;

## 视图

视图是一-个虚拟表，其内容由查询定义。同真实的表样，视图包含列,其数据来自对应的真实表(基表)

**视图的基本使用**
1.
create view视图名as select语句
2.
alter view视图名as select语句-更新成新的视图
3.
SHOW CREATE VIEW视图名
4.
drop view视图名1.视图名2

```
-- 视图的使用
-- 创建一个视图 emp_view01，只能查询 emp 表的(empno、ename, job 和 deptno ) 信息
-- 创建视图
CREATE VIEW emp_view01
AS

SELECT empno, ename, job, deptno FROM emp;
-- 查看视图
DESC emp_view01

SELECT * FROM emp_view01;
SELECT empno, job FROM emp_view01;
-- 查看创建视图的指令
SHOW CREATE VIEW emp_view01
-- 删除视图
DROP VIEW emp_view01;
-- 视图的细节
-- 1. 创建视图后，到数据库去看，对应视图只有一个视图结构文件(形式: 视图名.frm)
-- 2. 视图的数据变化会影响到基表，基表的数据变化也会影响到视图[insert update delete ]
-- 修改视图 会影响到基表
UPDATE emp_view01
SET job = 'MANAGER' WHERE empno = 7369
SELECT * FROM emp; -- 查询基表

SELECT * FROM emp_view01
-- 修改基本表， 会影响到视图
UPDATE emp
SET job = 'SALESMAN' WHERE empno = 7369
-- 3. 视图中可以再使用视图 , 比如从 emp_view01 视图中，选出 empno,和 ename 做出新视图
DESC emp_view01
CREATE VIEW emp_view02
AS
SELECT empno, ename FROM emp_view01
SELECT * FROM emp_view02
```

**视图作用**

1. 安全。一些数据表有着重要的信息。有些字段是保密的，不能让用户直接看到。这
    时就可以创建一个视图，在这张视图中只**保留一部分字段**。这样，用户就可以查询
    自己需要的字段，不能查看保密的字段。
2. 性能。关系数据库的数据常常会分表存储，使用外键建立这些表的之间关系。这时，
    数据库查询通常会用到连接JOIN)。这样做不但麻烦，效率相对也比较低。如果
    建立一个视图，将相关的表和字段组合在一起，就可以**避免使用JOIN查询数据**。
3. 灵活。如果系统中有一张旧的表，这张表由于设计的问题，即将被废弃。然而，很
    多应用都是基于这张表，不易修改。这时就可以建立一-张视图， 视图中的**数据直接**
    **映射到新建的表**。这样，就可以少做很多改动，也达到了**升级数据表**的目的。


## 数据库的设计

```mysql
1. 多表之间的关系
	1. 分类：
		1. 一对一(了解)：
			* 如：人和身份证
			* 分析：一个人只有一个身份证，一个身份证只能对应一个人
		2. 一对多(多对一)：
			* 如：部门和员工
			* 分析：一个部门有多个员工，一个员工只能对应一个部门
		3. 多对多：
			* 如：学生和课程
			* 分析：一个学生可以选择很多门课程，一个课程也可以被很多学生选择
	2. 实现关系：
		1. 一对多(多对一)：
			* 如：部门和员工
			* 实现方式：在多的一方建立外键，指向一的一方的主键。
		2. 多对多：
			* 如：学生和课程
			* 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键
		3. 一对一(了解)：
			* 如：人和身份证
			* 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。

	3. 案例
		-- 创建旅游线路分类表 tab_category
		-- cid 旅游线路分类主键，自动增长
		-- cname 旅游线路分类名称非空，唯一，字符串 100
		CREATE TABLE tab_category (
			cid INT PRIMARY KEY AUTO_INCREMENT,
			cname VARCHAR(100) NOT NULL UNIQUE
		);
		
		-- 创建旅游线路表 tab_route
		/*
		rid 旅游线路主键，自动增长
		rname 旅游线路名称非空，唯一，字符串 100
		price 价格
		rdate 上架时间，日期类型
		cid 外键，所属分类
		*/
		CREATE TABLE tab_route(
			rid INT PRIMARY KEY AUTO_INCREMENT,
			rname VARCHAR(100) NOT NULL UNIQUE,
			price DOUBLE,
			rdate DATE,
			cid INT,
			FOREIGN KEY (cid) REFERENCES	tab_category(cid)
		);
		
		/*创建用户表 tab_user
		uid 用户主键，自增长
		username 用户名长度 100，唯一，非空
		password 密码长度 30，非空
		name 真实姓名长度 100
		birthday 生日
		sex 性别，定长字符串 1
		telephone 手机号，字符串 11
		email 邮箱，字符串长度 100
		*/
		CREATE TABLE tab_user (
			uid INT PRIMARY KEY AUTO_INCREMENT,
			username VARCHAR(100) UNIQUE NOT NULL,
			PASSWORD VARCHAR(30) NOT NULL,
			NAME VARCHAR(100),
			birthday DATE,
			sex CHAR(1) DEFAULT '男',
			telephone VARCHAR(11),
			email VARCHAR(100)
		);
		
		/*
		创建收藏表 tab_favorite
		rid 旅游线路 id，外键
		date 收藏时间
		uid 用户 id，外键
		rid 和 uid 不能重复，设置复合主键，同一个用户不能收藏同一个线路两次
		*/
		CREATE TABLE tab_favorite (
			rid INT, -- 线路id
			DATE DATETIME,
			uid INT, -- 用户id
			-- 创建复合主键
			PRIMARY KEY(rid,uid), -- 联合主键
			FOREIGN KEY (rid) REFERENCES tab_route(rid),
			FOREIGN KEY(uid) REFERENCES tab_user(uid)
		);
```


​		

2. 数据库设计的范式
	* 概念：设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求

		设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。
		目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。

	* 分类：
		1. 第一范式（1NF）：**每一列都是不可分割的原子数据项**
		2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于码（**在1NF基础上消除非主属性对主码的部分函数依赖**）
			* 几个概念：
				1. 函数依赖：A-->B,如果通过A属性(属性组)的值，可以确定唯一B属性的值。则称B依赖于A
					例如：学号-->姓名。  （学号，课程名称） --> 分数
				2. 完全函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定需要依赖于A属性组中所有的属性值。
					例如：（学号，课程名称） --> 分数
				3. 部分函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定只需要依赖于A属性组中某一些值即可。
					例如：（学号，课程名称） -- > 姓名
				4. 传递函数依赖：A-->B, B -- >C . 如果通过A属性(属性组)的值，可以确定唯一B属性的值，在通过B属性（属性组）的值可以确定唯一C属性的值，则称 C 传递函数依赖于A
					例如：学号-->系名，系名-->系主任
				5. 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码
					例如：该表中码为：（学号，课程名称）
					* 主属性：码属性组中的所有属性
					* 非主属性：除过码属性组的属性
			
		3. 第三范式（3NF）：在2NF基础上，任何非主属性不依赖于其它非主属性（**在2NF基础上消除传递依赖**）


## 数据库的备份和还原

1. 命令行：
	* 语法：
		* 备份： mysqldump -u用户名 -p密码 数据库名称 > 保存的路径(D:/a.sql)
		* 还原：
			1. 登录数据库  mysql -u用户名 -p密码
			2. 创建数据库    create database 数据库名称
			3. 使用数据库    use  数据库名称
			4. 执行文件        source 文件路径(D:/a.sql)
2. 图形化工具


## 多表查询

* ```mysql
	* 查询语法：
	    select
	    	列名列表
	    from
	    	表名列表
	    where....
	
	* 准备sql
	
	    # 创建部门表
	
	    CREATE TABLE dept(
	    	id INT PRIMARY KEY AUTO_INCREMENT,
	    	NAME VARCHAR(20)
	    );
	    INSERT INTO dept (NAME) VALUES ('开发部'),('市场部'),('财务部');
	
	    # 创建员工表
	
	    CREATE TABLE emp (
	    	id INT PRIMARY KEY AUTO_INCREMENT,
	    	NAME VARCHAR(10),
	    	gender CHAR(1), -- 性别
	    	salary DOUBLE, -- 工资
	    	join_date DATE, -- 入职日期
	    	dept_id INT,
	    	FOREIGN KEY (dept_id) REFERENCES dept(id) -- 外键，关联部门表(部门表的主键)
	    );
	    INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('孙悟空','男',7200,'2013-02-24',1);
	    INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('猪八戒','男',3600,'2010-12-02',2);
	    INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('唐僧','男',9000,'2008-08-08',2);
	    INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('白骨精','女',5000,'2015-10-07',3);
	    INSERT INTO emp(NAME,gender,salary,join_date,dept_id) VALUES('蜘蛛精','女',4500,'2011-03-14',1);
	
	* 笛卡尔积：
	
	    * 有两个集合A,B .取这两个集合的所有组成情况。
	    * 要完成多表查询，需要消除无用的数据
	
	* 多表查询的分类：
	
	    1. 内连接查询：
	
	        1. 隐式内连接：使用where条件消除无用数据
	
	            * 例子：
	                -- 查询所有员工信息和对应的部门信息
	
	            SELECT * FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
	
	            -- 查询员工表的名称，性别。部门表的名称
	            SELECT emp.name,emp.gender,dept.name FROM emp,dept WHERE emp.`dept_id` = dept.`id`;
	
	            SELECT 
	            	t1.name, -- 员工表的姓名
	            	t1.gender,-- 员工表的性别
	            	t2.name -- 部门表的名称
	            FROM
	            	emp t1,
	            	dept t2
	            WHERE 
	            	t1.`dept_id` = t2.`id`;
	
	
	​	
	
	  2. 显式内连接：
	
	       * 语法： select 字段列表 from 表名1 [inner] join 表名2 on 条件
	
	          * 例如：
	              * SELECT * FROM emp INNER JOIN dept ON emp.`dept_id` = dept.`id`;	
	                 * SELECT * FROM emp JOIN dept ON emp.`dept_id` = dept.`id`;	
	
	         3. 内连接查询：
	             1. 从哪些表中查询数据
	             2. 条件是什么
	             3. 查询哪些字段
	
	     2. 外链接查询：
	
	         1. 左外连接：
	             * 语法：select 字段列表 from 表1 left [outer] join 表2 on 条件；
	             * 查询的是左表所有数据以及其交集部分。
	             * 例子：
	                 -- 查询所有员工信息，如果员工有部门，则查询部门名称，没有部门，则不显示部门名称
	                 SELECT 	t1.*,t2.`name` FROM emp t1 LEFT JOIN dept t2 ON t1.`dept_id` = t2.`id`;
	         2. 右外连接：
	             * 语法：select 字段列表 from 表1 right [outer] join 表2 on 条件；
	             * 查询的是右表所有数据以及其交集部分。
	             * 例子：
	                 SELECT 	* FROM dept t2 RIGHT JOIN emp t1 ON t1.`dept_id` = t2.`id`;
	
	     3. 子查询：
	
	         * 概念：查询中嵌套查询，称嵌套查询为子查询。
	             -- 查询工资最高的员工信息
	             -- 1 查询最高的工资是多少 9000
	             SELECT MAX(salary) FROM emp;
	
	             -- 2 查询员工信息，并且工资等于9000的
	             SELECT * FROM emp WHERE emp.`salary` = 9000;
	
	             -- 一条sql就完成这个操作。子查询
	             SELECT * FROM emp WHERE emp.`salary` = (SELECT MAX(salary) FROM emp);
	
	         * 子查询不同情况
	
	             1. 子查询的结果是单行单列的：
	
	                 * 子查询可以作为条件，使用运算符去判断。 运算符： > >= < <= =
	                 * -- 查询员工工资小于平均工资的人
	                     SELECT * FROM emp WHERE emp.salary < (SELECT AVG(salary) FROM emp);
	
	             2. 子查询的结果是多行单列的：
	
	                 * 子查询可以作为条件，使用运算符in来判断
	                     -- 查询'财务部'和'市场部'所有的员工信息
	                     SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部';
	                     SELECT * FROM emp WHERE dept_id = 3 OR dept_id = 2;
	                     -- 子查询
	                     SELECT * FROM emp WHERE dept_id IN (SELECT id FROM dept WHERE NAME = '财务部' OR NAME = '市场部');
	
	             3. 子查询的结果是多行多列的：
	
	                 * 子查询可以作为一张虚拟表参与查询
	                     -- 查询员工入职日期是2011-11-11日之后的员工信息和部门信息
	                     -- 子查询
	                     SELECT * FROM dept t1 ,(SELECT * FROM emp WHERE emp.`join_date` > '2011-11-11') t2
	                     WHERE t1.id = t2.dept_id;
	
	                 -- 普通内连接
	                 SELECT * FROM emp t1,dept t2 WHERE t1.`dept_id` = t2.`id` AND t1.`join_date` >  '2011-11-11'
	                 
	                 
	 增强查询
	多表
	select ename, sal, grade
	from emp , salgrade
	where sal between losal and hisal;
	
	自连接
	-- 自连接的特点 1. 把同一张表当做两张表使用
	-- 2. 需要给表取别名 表名 表别名
	-- 3. 列名不明确，可以指定列的别名 列名 as 列的别名
	SELECT worker.ename AS '职员名' , boss.ename AS '上级名' FROM emp worker, emp boss
	WHERE worker.mgr = boss.empno
	
	多行子查询（where 后面一般用关键字 in/all/any)
	如何显示工资比部门 30 的其中一个员工的工资高的员工的姓名、工资和部门号
	SELECT ename, sal, deptno
	FROM emp
	WHERE sal > any(
	SELECT sal
	FROM emp
	WHERE deptno = 30
	)
	
	多列子查询
	SELECT *
	FROM emp
	WHERE (deptno , job) = (
	SELECT deptno , job
	FROM emp
	WHERE ename = 'ALLEN' ) AND ename
	
	在 from 子句中使用子查询
	做一张临时表
	select goods_id, ecs_goods.cat_id, goods_name, shop_price
	from (
	SELECT cat_id , MAX(shop_price) as max_price
	FROM ecs_goods
	GROUP BY cat_id
	) temp , ecs_goods
	where temp.cat_id = ecs_goods.cat_id
	and temp.max_price = ecs_goods.shop_price
	
	SELECT tmp.* , dname, loc
	FROM dept, (
	SELECT COUNT(*) AS per_num, deptno
	FROM emp
	GROUP BY deptno
	) tmp
	WHERE tmp.deptno = dept.deptno
	
	合并查询（合并多个select语句的结果）
	 union all 就是将两个查询结果合并，不会去重
	  union 就是将两个查询结果合并，会去重
	  
	SELECT ename,sal,job FROM emp WHERE sal>2500 -- 5
	UNION
	SELECT ename,sal,job FROM emp WHERE job='MANAGER' -- 3
	```
	
	


## 事务

1. 事务的基本介绍
	1. 概念：
		*  如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
		*  事务用于保证数据的一致性，它由组相关的dml语句组成该组的dml语句要么全部成功，要么全部失败。如:转账就要用事务来处理，用以保证数据的一致性。
		
	2. 操作：
		1. 开启事务： start transaction;
		2. 设置保存点：savepoint 保存点名
		3. 回退事务：rollback to  保存点名
		4. 回退全部事务：rollback
		5. 提交事务: commit
	3. 例子：
		CREATE TABLE account (
			id INT PRIMARY KEY AUTO_INCREMENT,
			NAME VARCHAR(10),
			balance DOUBLE
		);
		-- 添加数据
		INSERT INTO account (NAME, balance) VALUES ('zhangsan', 1000), ('lisi', 1000);


​			

​		SELECT * FROM account;
​		UPDATE account SET balance = 1000;
​		-- 张三给李四转账 500 元
​		
​		-- 0. 开启事务
​		START TRANSACTION;
​		-- 1. 张三账户 -500
​		
​		UPDATE account SET balance = balance - 500 WHERE NAME = 'zhangsan';
​		-- 2. 李四账户 +500
​		-- 出错了...
​		UPDATE account SET balance = balance + 500 WHERE NAME = 'lisi';
​		
​		-- 发现执行没有问题，提交事务
​		COMMIT;
​		
​		-- 发现出问题了，回滚事务
​		ROLLBACK;

1.如果不开始事务，默认情况下，dml操作是自动提交的，不能回滚
2.如果开始一个事务，你没有创建保存点.你可以执行rollback,默认就是回退到你事务开始的状态.
3.你也可以在这个事务中(还没有提交时)，创建多个保存点比如: savepoint aaa;
执行dml，savepoint bbb;
4.你可以在事务没有提交前，选择回退到哪个保存点.

5.mysql的事务机制需要**innodb的存储引擎**才可以使用,myisam不好使.
6.开始一个事务start transaction, set autocommit=off;

	4. MySQL数据库中事务默认自动提交
		
		* 事务提交的两种方式：
			* 自动提交：
				* mysql就是自动提交的
				* 一条DML(增删改)语句会自动提交一次事务。
			* 手动提交：
				* Oracle 数据库默认是手动提交事务
				* 需要先开启事务，再提交
		* 修改事务的默认提交方式：
			* 查看事务的默认提交方式：SELECT @@autocommit; -- 1 代表自动提交  0 代表手动提交
			* 修改默认提交方式： set @@autocommit = 0;

2. 事务ACID的四大特征：

  原子性：事务中的操作要么全部成功，要么全部失败。比如在同一个事务中的SQL语句，要么全部执行成功，要么全部执行失败。

  一致性：事务必须使数据库从一个一致性状态变换到另外一个一致性状态。

  隔离性：多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。

  持久性：持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响。

3. 事务的隔离级别（了解）
  * 概念：多个事务之间隔离的，相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题。

  * 存在问题：

  	1. 脏读：一个事务，读取到另一个事务中没有提交的数据
  	2. 不可重复读(虚读)：在同一个事务中，两次读(修改或删除）取到的数据不一样。
  	3. 幻读：一个事务操作(DML)数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改。

  * 隔离级别：
    1. read uncommitted：读未提交
    	* 产生的问题：脏读、不可重复读、幻读
    2. read committed：读已提交 （Oracle）
    	* 产生的问题：不可重复读、幻读
    3. repeatable read：可重复读 （MySQL默认）
    	* 产生的问题：幻读
    4. serializable：串行化
    	* 可以解决所有的问题

    * 注意：隔离级别从小到大安全性越来越高，但是效率越来越低
    * 数据库查询隔离级别：
    1. 查看当前会话隔离级别 
    select @@transaction_isolation;
    2.查看系统当前隔离级别
    select @@global.tx isolation;
    3.设置当前会话隔离级别
    set session transaction isolation level repeatable read;
    4.设置系统当前隔离级别
    set global transaction isolation level repeatable read;
    5. mysql 默认的事务隔离级别是repeatable read ,一般情况下，没有特殊
    要求，没有必要修改(因为该级别可以满足绝大部分项目需求)

  * 演示：

  	set global transaction isolation level read uncommitted;
  	start transaction;
  	-- 转账操作
  	update account set balance = balance - 500 where id = 1;
  	update account set balance = balance + 500 where id = 2;

  




## DCL（管理用户，授权）

	* SQL分类：
		1. DDL：操作数据库和表
		2. DML：增删改表中数据
		3. DQL：查询表中数据
		4. DCL：管理用户，授权
	
	* DBA：数据库管理员
	
	mysql 中user表的重要字段说明:
	1. host:允许登录的“位置”，localhost表示该用户只允许本机登录，也可以指定ip地址，比如:192.168.1.100
	2.user:用户名;
	3. authentication string: 密码，是通过mysql的password(函数加密之后的密码。
	
	* DCL：管理用户，授权
		1. 管理用户
			1. 添加用户同时指定密码：
				* 语法：CREATE USER '用户名'@'主机名'（允许登录的位置）【 IDENTIFIED BY '密码'】;
			2. 删除用户：
				* 语法：DROP USER '用户名'@'主机名'（允许登录的位置）;
			3. 修改用户密码：
				
				UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
				UPDATE USER SET PASSWORD = PASSWORD('abc') WHERE USER = 'lisi';
				
				SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');
				SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123');
	
				* mysql中忘记了root用户的密码？
					1. cmd -- > net stop mysql 停止mysql服务
						* 需要管理员运行该cmd
	
					2. 使用无验证方式启动mysql服务： mysqld --skip-grant-tables
					3. 打开新的cmd窗口,直接输入mysql命令，敲回车。就可以登录成功
					4. use mysql;
					5. update user set password = password('你的新密码') where user = 'root';
					6. 关闭两个窗口
					7. 打开任务管理器，手动结束mysqld.exe 的进程
					8. 启动mysql服务
					9. 使用新密码登录。
			4. 查询用户：
				-- 1. 切换到mysql数据库
				USE myql;
				-- 2. 查询user表
				SELECT * FROM USER;
				
				* 通配符： % 表示可以在任意主机使用用户登录数据库
	
		2. 权限管理：
			1. 查询权限：
				-- 查询权限
				SHOW GRANTS FOR '用户名'@'主机名';
				SHOW GRANTS FOR 'lisi'@'%';
	
			2. 授予权限：
				-- 授予权限
				grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';
				grant select,delete,create on ...(多个权限用逗号隔开)
				grant all[privileges] on..。 赋予该对象所有权限
				
				特别说明
				*.* :代表本系统中的所有数据库的所有对象(表， 视图，存储过程)
				库.* :表示某个数据库中的所有数据对象(表，视图，存储过程等)
				 identified by可以省略，也可以写出.
					(1)如果用户存在，就是修改该用户的密码。
					(2)如果该用户不存在，就是创建该用户!
				-- 给张三用户授予所有权限，在任意数据库任意表上
				
				GRANT ALL ON *.* TO 'zhangsan'@'localhost';
			3. 撤销权限：
				-- 撤销权限：
				revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';
				REVOKE UPDATE ON db3.`account` FROM 'lisi'@'%';
				
			如果权限没有生效，可以执行下面命令.
			基本语法:FLUSH PRIVILEGES;


​			
			1.在创建用户的时候，如果不指定Host,则为%，%表示表示所有IP都有连接权限
				create user XXX;
			2.你也可以这样指定
				create user 'xxx @' 192.1 68.1.%表示xxx用户在192.168. 1.*的ip可以登录mysql
			3.在删除用户的时候，如果host不是%,需要明确指定'用户'@'host值'


# JDBC


## JDBC

	1. 概念：Java DataBase Connectivity  Java 数据库连接， Java语言操作数据库
		* JDBC本质：其实是官方（sun公司）定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口（JDBC）编程，真正执行的代码是驱动jar包中的实现类。
	
	2. 快速入门：
		* 步骤：
			1. 导入驱动jar包 mysql-connector-java-5.1.37-bin.jar
				1.复制mysql-connector-java-5.1.37-bin.jar到项目的libs目录下
				2.右键-->Add As Library
			2. 注册驱动
			3. 获取数据库连接对象 Connection
			4. 定义sql
			5. 获取执行sql语句的对象 Statement
			6. 执行sql，接受返回结果
			7. 处理结果
			8. 释放资源
	
		* 代码实现：
		  	//1. 导入驱动jar包
	        //2.注册驱动
	        Class.forName("com.mysql.cj.jdbc.Driver");
	        //3.获取数据库连接对象
	        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db3", "root", "root");
	        //4.定义sql语句
	        String sql = "update account set balance = 500 where id = 1";
	        //5.获取执行sql的对象 Statement
	        Statement stmt = conn.createStatement();
	        //6.执行sql
	        int count = stmt.executeUpdate(sql);
	        //7.处理结果
	        System.out.println(count);
	        //8.释放资源
	        stmt.close();
	        conn.close();
	
	3. 详解各个对象：
		1. DriverManager：驱动管理对象
			* 功能：
				1. 注册驱动：告诉程序该使用哪一个数据库驱动jar
					static void registerDriver(Driver driver) :注册与给定的驱动程序 DriverManager 。 
					写代码使用：  Class.forName("com.mysql.jdbc.Driver");
					通过查看源码发现：在com.mysql.jdbc.Driver类中存在静态代码块
					 static {
					        try {
					            java.sql.DriverManager.registerDriver(new Driver());
					        } catch (SQLException E) {
					            throw new RuntimeException("Can't register driver!");
					        }
						}
	
					注意：mysql5之后的驱动jar包可以省略注册驱动的步骤。
				2. 获取数据库连接：
					* 方法：static Connection getConnection(String url, String user, String password) 
					* 参数：
						* url：指定连接的路径
							* 语法：jdbc:mysql://ip地址(域名):端口号/数据库名称
							* 例子：jdbc:mysql://localhost:3306/db3
							* 细节：如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以简写为：jdbc:mysql:///数据库名称
						* user：用户名
						* password：密码 
		2. Connection：数据库连接对象
			1. 功能：
				1. 获取执行sql 的对象
					* Statement createStatement()
					* PreparedStatement prepareStatement(String sql)  
				2. 管理事务：
					* 开启事务：setAutoCommit(boolean autoCommit) ：调用该方法设置参数为false，即开启事务
					* 提交事务：commit() 
					* 回滚事务：rollback() 
		3. Statement：执行sql的对象
			1. 执行sql
				1. boolean execute(String sql) ：可以执行任意的sql 了解 
				2. int executeUpdate(String sql) ：执行DML（insert、update、delete）语句、DDL(create，alter、drop)语句
					* 返回值：影响的行数，可以通过这个影响的行数判断DML语句是否执行成功 返回值>0的则执行成功，反之，则失败。
				3. ResultSet executeQuery(String sql)  ：执行DQL（select)语句


​				
​		4. ResultSet：结果集对象,封装查询结果
​			* boolean next(): 游标向下移动一行，判断当前行是否是最后一行末尾(是否有数据)，如果是，则返回false，如果不是则返回true
​			* getXxx(参数):获取数据
​				* Xxx：代表数据类型   如： int getInt() ,	String getString()
​				* 参数：
​					1. int：代表列的编号,从1开始   如： getString(1)
​					2. String：代表列名称。 如： getDouble("balance")
​			
​			* 注意：
​				* 使用步骤：
​					1. 游标向下移动一行
​					2. 判断是否有数据
​					3. 获取数据
​	
​				   //循环判断游标是否是最后一行末尾。
​		            while(rs.next()){
​		                //获取数据
​		                //6.2 获取数据
​		                int id = rs.getInt(1);
​		                String name = rs.getString("name");
​		                double balance = rs.getDouble(3);
​		
​		                System.out.println(id + "---" + name + "---" + balance);
​		            }
​	
​			* 练习：
​				* 定义一个方法，查询emp表的数据将其封装为对象，然后装载集合，返回。
​					1. 定义Emp类
​					2. 定义方法 public List<Emp> findAll(){}
​					3. 实现方法 select * from emp;
​						
​		5. PreparedStatement：执行sql的对象
​			1. SQL注入问题：在拼接sql时，有一些sql的特殊关键字参与字符串的拼接。会造成安全性问题
​				1. 输入用户随便，输入密码：a' or 'a' = 'a
​				2. sql：select * from user where username = 'fhdsjkf' and password = 'a' or 'a' = 'a' 
​	
​			2. 解决sql注入问题：使用PreparedStatement对象来解决
​			3. 预编译的SQL：参数使用?作为占位符
​			4. 步骤：
​				1. 导入驱动jar包 mysql-connector-java-5.1.37-bin.jar
​				2. 注册驱动
​				3. 获取数据库连接对象 Connection
​				4. 定义sql
​					* 注意：sql的参数使用？作为占位符。 如：select * from user where username = ? and password = ?;
​				5. 获取执行sql语句的对象 PreparedStatement  Connection.prepareStatement(String sql) 
​				6. 给？赋值：
​					* 方法： setXxx(参数1,参数2)
​						* 参数1：？的位置编号 从1 开始
​						* 参数2：？的值
​				7. 执行sql，接受返回结果，不需要传递sql语句
​				8. 处理结果
​				9. 释放资源
​	
​			5. 注意：后期都会使用PreparedStatement来完成增删改查的所有操作
​				1. 可以防止SQL注入
​				2. 效率更高

## 抽取JDBC工具类 ： JDBCUtils

* ```java
    * 目的：简化书写
    * 分析：
        1. 注册驱动也抽取
        2. 抽取一个方法获取连接对象
            * 需求：不想传递参数（麻烦），还得保证工具类的通用性。
            * 解决：配置文件
                jdbc.properties
                	url=
                	user=
                	password=
    
     	3. 抽取一个方法释放资源
    
    * 代码实现：
        public class JDBCUtils {
          private static String url;
          private static String user;
          private static String password;
          private static String driver;
          /**
    
           * 文件的读取，只需要读取一次即可拿到这些值。使用静态代码块
             */
               static{
             //读取资源文件，获取值。
    
             try {
                 //1. 创建Properties集合类。
                 Properties pro = new Properties();
             ​    //获取src路径下的文件的方式--->ClassLoader 类加载器
             ​    ClassLoader classLoader = JDBCUtils.class.getClassLoader();
    		InputStream resourceAsStream = classLoader.getResourceAsStream("cn/itcast/jdbc/jdbc.properties");
             ​    //2. 加载文件
    			  pro.load(resourceAsStream);
    
             ​    //3. 获取数据，赋值
             ​    url = pro.getProperty("url");
             ​    user = pro.getProperty("user");
             ​    password = pro.getProperty("password");
             ​    driver = pro.getProperty("driver");
             ​    //4. 注册驱动
             ​    Class.forName(driver);
             } catch (IOException e) {
             ​    e.printStackTrace();
             } catch (ClassNotFoundException e) {
             ​    e.printStackTrace();
             }
               }
    
    
    ​	
    
    ​    /**
    
       * 获取连接
          @return 连接对象
              */
             public static Connection getConnection() throws SQLException {
    
         return DriverManager.getConnection(url, user, password);
             }
    
    ​    /**
    
       * 释放资源
          @param stmt
    
            * @param conn
              /
                  public static void close(Statement stmt,Connection conn){
              if( stmt != null){
                  try {
              stmt.close();
                  } catch (SQLException e) {
              e.printStackTrace();
                  }
              }
    
         if( conn != null){
             try {
                 conn.close();
             } catch (SQLException e) {
                 e.printStackTrace();
             }
         }
             }
    
    
    ​	
    
    ​    /**
    
       * 释放资源
          @param stmt
    
            * @param conn
              /
                  public static void close(ResultSet rs,Statement stmt, Connection conn){
              if( rs != null){
                  try {
              rs.close();
                  } catch (SQLException e) {
              e.printStackTrace();
                  }
              }
    
         if( stmt != null){
             try {
                 stmt.close();
             } catch (SQLException e) {
                 e.printStackTrace();
             }
         }
    
         if( conn != null){
             try {
                 conn.close();
             } catch (SQLException e) {
                 e.printStackTrace();
             }
         }
             }
    
    }
    
    * 练习：
    
        * 需求：
    
            1. 通过键盘录入用户名和密码
            2. 判断用户是否登录成功
                * select * from user where username = "" and password = "";
                * 如果这个sql有查询结果，则成功，反之，则失败
    
        * 步骤：
    
            1. 创建数据库表 user
                CREATE TABLE USER(
                	id INT PRIMARY KEY AUTO_INCREMENT,
                	username VARCHAR(32),
                	PASSWORD VARCHAR(32)
    
                );
    
                INSERT INTO USER VALUES(NULL,'zhangsan','123');
                INSERT INTO USER VALUES(NULL,'lisi','234');
    
            2. 代码实现：
                public class JDBCDemo9 {
    
                ​    public static void main(String[] args) {
                ​        //1.键盘录入，接受用户名和密码
                ​        Scanner sc = new Scanner(System.in);
                ​        System.out.println("请输入用户名：");
                ​        String username = sc.nextLine();
                ​        System.out.println("请输入密码：");
                ​        String password = sc.nextLine();
                ​        //2.调用方法
                ​        boolean flag = new JDBCDemo9().login(username, password);
                ​        //3.判断结果，输出不同语句
                ​        if(flag){
                ​            //登录成功
                ​            System.out.println("登录成功！");
                ​        }else{
                ​            System.out.println("用户名或密码错误！");
                ​        }
    
    
    ​				
    
    ​			    }
    
    
    ​				
    ​				
    
    ​			    /**
    
       * 登录方法
         		     */
         		    public boolean login(String username ,String password){
         		        if(username == null || password == null){
         		            return false;
         		        }
         		        //连接数据库判断是否登录成功
         		        Connection conn = null;
         		        Statement stmt =  null;
         		        ResultSet rs = null;
         		        //1.获取连接
         		        try {
         		            conn =  JDBCUtils.getConnection();
         		            //2.定义sql
         		            String sql = "select * from user where username = '"+username+"' and password = '"+password+"' ";
         		            //3.获取执行sql的对象
         		            stmt = conn.createStatement();
         		            //4.执行查询
         		            rs = stmt.executeQuery(sql);
         		            //5.判断
         		           /* if(rs.next()){//如果有下一行，则返回true
         		                return true;
         		            }else{
         		                return false;
         		            }*/
         		           return rs.next();//如果有下一行，则返回true
         		
         		        } catch (SQLException e) {
         		            e.printStackTrace();
         		        }finally {
         		            JDBCUtils.close(rs,stmt,conn);
         		        }
    ​			        return false;
    ​			    }
    ​			}
    ```

    


## JDBC控制事务

```java
1. 事务：一个包含多个步骤的业务操作。如果这个业务操作被事务管理，则这多个步骤要么同时成功，要么同时失败。
2. 操作：
	1. 开启事务
	2. 提交事务
	3. 回滚事务
3. 使用Connection对象来管理事务
	* 开启事务：setAutoCommit(boolean autoCommit) ：调用该方法设置参数为false，即开启事务
		* 在执行sql之前开启事务
	* 提交事务：commit() 
		* 当所有sql都执行完提交事务
	* 回滚事务：rollback() 
		* 在catch中回滚事务

4. 代码：
	public class JDBCDemo10 {

	    public static void main(String[] args) {
	        Connection conn = null;
	        PreparedStatement pstmt1 = null;
	        PreparedStatement pstmt2 = null;
	
	        try {
	            //1.获取连接
	            conn = JDBCUtils.getConnection();
	            //开启事务
	            conn.setAutoCommit(false);
	
	            //2.定义sql
	            //2.1 张三 - 500
	            String sql1 = "update account set balance = balance - ? where id = ?";
	            //2.2 李四 + 500
	            String sql2 = "update account set balance = balance + ? where id = ?";
	            //3.获取执行sql对象
	            pstmt1 = conn.prepareStatement(sql1);
	            pstmt2 = conn.prepareStatement(sql2);
	            //4. 设置参数
	            pstmt1.setDouble(1,500);
	            pstmt1.setInt(2,1);
	
	            pstmt2.setDouble(1,500);
	            pstmt2.setInt(2,2);
	            //5.执行sql
	            pstmt1.executeUpdate();
	            // 手动制造异常
	            int i = 3/0;
	
	            pstmt2.executeUpdate();
	            //提交事务
	            conn.commit();
	        } catch (Exception e) {
	            //事务回滚
	            try {
	                if(conn != null) {
	                    conn.rollback();
	                }
	            } catch (SQLException e1) {
	                e1.printStackTrace();
	            }
	            e.printStackTrace();
	        }finally {
	            JDBCUtils.close(pstmt1,conn);
	            JDBCUtils.close(pstmt2,null);
	        }
	   }
}
```


​		

## 数据库连接池

```java
1. 概念：其实就是一个容器(集合)，存放数据库连接的容器。
        当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问完之后，会将连接对象归还给容器。

2. 好处：
    1. 节约资源
    2. 用户访问高效

3. 实现：
    1. 标准接口：DataSource   javax.sql包下的
        1. 方法：
            * 获取连接：getConnection()
            * 归还连接：Connection.close()。如果连接对象Connection是从连接池中获取的，那么调用Connection.close()方法，则不会再关闭连接了。而是归还连接

    2. 一般我们不去实现它，有数据库厂商来实现
        1. C3P0：数据库连接池技术
        2. Druid：数据库连接池实现技术，由阿里巴巴提供的

4. C3P0：数据库连接池技术

    * 步骤：
        1. 导入jar包 (两个) c3p0-0.9.5.2.jar mchange-commons-java-0.2.12.jar ，
            * 不要忘记导入数据库驱动jar包
        2. 定义配置文件：
            * 名称： c3p0.properties 或者 c3p0-config.xml
            * 路径：直接将文件放在src目录下即可。

        3. 创建核心对象 数据库连接池对象 ComboPooledDataSource
        4. 获取连接： getConnection
    * 代码：
        //1.创建数据库连接池对象
          DataSource ds  = new ComboPooledDataSource();
          //2. 获取连接对象
          Connection conn = ds.getConnection();

5. Druid：数据库连接池实现技术，由阿里巴巴提供的

    1. 步骤：
        1. 导入jar包 druid-1.0.9.jar
        2. 定义配置文件：
            * 是properties形式的
            * 可以叫任意名称，可以放在任意目录下
        3. 加载配置文件。Properties
        4. 获取数据库连接池对象：通过工厂来来获取  DruidDataSourceFactory
        5. 获取连接：getConnection

    * 代码：
        //3.加载配置文件
          Properties pro = new Properties();
          InputStream is = DruidDemo.class.getClassLoader().getResourceAsStream("druid.properties");
          pro.load(is);
          //4.获取连接池对象
          DataSource ds = DruidDataSourceFactory.createDataSource(pro);
          //5.获取连接
          Connection conn = ds.getConnection();

    2. 定义工具类
        1. 定义一个类 JDBCUtils
        2. 提供静态代码块加载配置文件，初始化连接池对象
        3. 提供方法
            1. 获取连接方法：通过数据库连接池获取连接
            2. 释放资源
            3. 获取连接池的方法

 * 代码：
    	public class JDBCUtils {

    ​	    //1.定义成员变量 DataSource
    ​	    private static DataSource ds ;
    ​	
    ​	    static{
    ​	        try {
    ​	            //1.加载配置文件
    ​	            Properties pro = new Properties();
    ​	            pro.load(JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
    ​	            //2.获取DataSource
    ​	            ds = DruidDataSourceFactory.createDataSource(pro);
    ​	        } catch (IOException e) {
    ​	            e.printStackTrace();
    ​	        } catch (Exception e) {
    ​	            e.printStackTrace();
    ​	        }
    ​	    }
    ​	
    ​	    /**

       * 获取连接
              */
             public static Connection getConnection() throws SQLException {
                 return ds.getConnection();
             }

         ​    /**

            * 释放资源
              /
                  public static void close(Statement stmt,Connection conn){
              /* if(stmt != null){
                   try {
                       stmt.close();
                   } catch (SQLException e) {
                       e.printStackTrace();
                   }
               }

               if(conn != null){
                   try {
                       conn.close();//归还连接
                   } catch (SQLException e) {
                       e.printStackTrace();
                   }
               }*/

              close(null,stmt,conn);
                  }

​		    public static void close(ResultSet rs , Statement stmt, Connection conn){

​		        if(rs != null){
​		            try {
​		                rs.close();
​		            } catch (SQLException e) {
​		                e.printStackTrace();
​		            }
​		        }

​		        if(stmt != null){
​		            try {
​		                stmt.close();
​		            } catch (SQLException e) {
​		                e.printStackTrace();
​		            }
​		        }
​		
​		        if(conn != null){
​		            try {
​		                conn.close();//归还连接
​		            } catch (SQLException e) {
​		                e.printStackTrace();
​		            }
​		        }
​		    }
​		
​		    /**

   * 获取连接池方法
     	     */
     	
     	    public static DataSource getDataSource(){
     	        return  ds;
     	    }
     	
     	}
```



## Spring JDBC

```java
* Spring框架对JDBC的简单封装。提供了一个JDBCTemplate对象简化JDBC的开发

* 步骤：

    1. 导入jar包

    2. 创建JdbcTemplate对象。依赖于数据源DataSource

        * JdbcTemplate template = new JdbcTemplate(ds);

    3. 调用JdbcTemplate的方法来完成CRUD的操作

        * update():执行DML语句。增、删、改语句
        * queryForMap():查询结果将结果集封装为map集合，将列名作为key，将值作为value 将这条记录封装为一个map集合
            * 注意：这个方法查询的结果集长度只能是1
        * queryForList():查询结果将结果集封装为list集合
            * 注意：将每一条记录封装为一个Map集合，再将Map集合装载到List集合中
        * query():查询结果，将结果封装为JavaBean对象
            * query的参数：RowMapper
                * 一般我们使用BeanPropertyRowMapper实现类。可以完成数据到JavaBean的自动封装
                * new BeanPropertyRowMapper<类型>(类型.class)
        * queryForObject：查询结果，将结果封装为对象
            * 一般用于聚合函数的查询

    4. 练习：

        * 需求：

            1. 修改1号数据的 salary 为 10000
            2. 添加一条记录
            3. 删除刚才添加的记录
            4. 查询id为1的记录，将其封装为Map集合
            5. 查询所有记录，将其封装为List
            6. 查询所有记录，将其封装为Emp对象的List集合
            7. 查询总记录数

        * 代码：

            import cn.itcast.domain.Emp;
            import cn.itcast.utils.JDBCUtils;
            import org.junit.Test;
            import org.springframework.jdbc.core.BeanPropertyRowMapper;
            import org.springframework.jdbc.core.JdbcTemplate;
            import org.springframework.jdbc.core.RowMapper;

            import java.sql.Date;
            import java.sql.ResultSet;
            import java.sql.SQLException;
            import java.util.List;
            import java.util.Map;

            public class JdbcTemplateDemo2 {

            ​    //Junit单元测试，可以让方法独立执行


​				

​			    //1. 获取JDBCTemplate对象
​			    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
​			    /**

   * 1. 修改1号数据的 salary 为 10000
             */
         	    @Test
         	    public void test1(){
         	
         	        //2. 定义sql
         	        String sql = "update emp set salary = 10000 where id = 1001";
         	        //3. 执行sql
         	        int count = template.update(sql);
         	        System.out.println(count);
         	    }
         	
         	    /**

            * 2. 添加一条记录
                  */
                  @Test
                  public void test2(){
                      String sql = "insert into emp(id,ename,dept_id) values(?,?,?)";
                      int count = template.update(sql, 1015, "郭靖", 10);
                      System.out.println(count);

                  }

                  /**

                   * 3.删除刚才添加的记录
                      */
                      @Test
                      public void test3(){
                      String sql = "delete from emp where id = ?";
                      int count = template.update(sql, 1015);
                      System.out.println(count);
                      }

                  /**

                   * 4.查询id为1001的记录，将其封装为Map集合
                   * 注意：这个方法查询的结果集长度只能是1
                      */
                      @Test
                      public void test4(){
                      String sql = "select * from emp where id = ? or id = ?";
                      Map<String, Object> map = template.queryForMap(sql, 1001,1002);
                      System.out.println(map);
                      //{id=1001, ename=孙悟空, job_id=4, mgr=1004, joindate=2000-12-17, salary=10000.00, bonus=null, dept_id=20}

                  }

                  /**

                   * 5. 查询所有记录，将其封装为List
                          */
                          @Test
                          public void test5(){
                            String sql = "select * from emp";
                            List<Map<String, Object>> list = template.queryForList(sql);

                        for (Map<String, Object> stringObjectMap : list) {
                            System.out.println(stringObjectMap);
                        }
                      }

                  /**

                   * 6. 查询所有记录，将其封装为Emp对象的List集合
                          */

                  @Test
                  public void test6(){
                      String sql = "select * from emp";
                      List<Emp> list = template.query(sql, new RowMapper<Emp>() {

                  ​        @Override
                  ​        public Emp mapRow(ResultSet rs, int i) throws SQLException {
                  ​            Emp emp = new Emp();
                  ​            int id = rs.getInt("id");
                  ​            String ename = rs.getString("ename");
                  ​            int job_id = rs.getInt("job_id");
                  ​            int mgr = rs.getInt("mgr");
                  ​            Date joindate = rs.getDate("joindate");
                  ​            double salary = rs.getDouble("salary");
                  ​            double bonus = rs.getDouble("bonus");
                  ​            int dept_id = rs.getInt("dept_id");

                  ​            emp.setId(id);
                  ​            emp.setEname(ename);
                  ​            emp.setJob_id(job_id);
                  ​            emp.setMgr(mgr);
                  ​            emp.setJoindate(joindate);
                  ​            emp.setSalary(salary);
                  ​            emp.setBonus(bonus);
                  ​            emp.setDept_id(dept_id);

                  ​            return emp;
                  ​        }
                  ​    });


​				

​			        for (Emp emp : list) {
​			            System.out.println(emp);
​			        }
​			    }
​			
​			    /**

   * 6. 查询所有记录，将其封装为Emp对象的List集合
             */
         	
         	    @Test
         	    public void test6_2(){
         	        String sql = "select * from emp";
         	        List<Emp> list = template.query(sql, new BeanPropertyRowMapper<Emp>(Emp.class));
         	        for (Emp emp : list) {
         	            System.out.println(emp);
         	        }
         	    }
         	
         	    /**

            * 7. 查询总记录数
                  */

                  @Test
                  public void test7(){
                      String sql = "select count(id) from emp";
                      Long total = template.queryForObject(sql, Long.class);
                      System.out.println(total);
                  }

              }
```

# web

## 概念概述

* JavaWeb：
	
* 使用Java语言开发基于互联网的项目
	
* 软件架构：
	1. C/S: Client/Server 客户端/服务器端
		* 在用户本地有一个客户端程序，在远程有一个服务器端程序
		* 如：QQ，迅雷...
		* 优点：
			1. 用户体验好
		* 缺点：
			1. 开发、安装，部署，维护 麻烦
	2. B/S: Browser/Server 浏览器/服务器端
		* 只需要一个浏览器，用户通过不同的网址(URL)，客户访问不同的服务器端程序
		* 优点：
			1. 开发、安装，部署，维护 简单
		* 缺点：
			1. 如果应用过大，用户的体验可能会受到影响
			2. 对硬件要求过高

* B/S架构详解
	* 资源分类：
		1. 静态资源：
			* 使用静态网页开发技术发布的资源。
			* 特点：
				* 所有用户访问，得到的结果是一样的。
				* 如：文本，图片，音频、视频, HTML,CSS,JavaScript
				* 如果用户请求的是静态资源，那么服务器会直接将静态资源发送给浏览器。浏览器中内置了静态资源的解析引擎，可以展示静态资源
		2. 动态资源：
			* 使用动态网页及时发布的资源。
			* 特点：
				* 所有用户访问，得到的结果可能不一样。
				* 如：jsp/servlet,php,asp...
				* 如果用户请求的是动态资源，那么服务器会执行动态资源，转换为静态资源，再发送给浏览器

		* 我们要学习动态资源，必须先学习静态资源！
	
		* 静态资源：
			* HTML：用于搭建基础网页，展示页面的内容
			* CSS：用于美化页面，布局页面
			* JavaScript：控制页面的元素，让页面有一些动态的效果



## HTML

### 概念：是最基础的网页开发语言

* Hyper Text Markup Language 超文本标记语言
	* 超文本:
		* 超文本是用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本.
	* 标记语言:
		* 由标签构成的语言。<标签名称> 如 html，xml
		* 标记语言不是编程语言

2. 快速入门：
	* 语法：
		1. html文档后缀名 .html 或者 .htm
		2. 标签分为
			1. 围堵标签：有开始标签和结束标签。如 <html> </html>
			2. 自闭和标签：开始标签和结束标签在一起。如 <br/>

		3. 标签可以嵌套：
			需要正确嵌套，不能你中有我，我中有你
			错误：<b></b>
			正确：<b></b>

		4. 在开始标签中可以定义属性。属性是由键值对构成，值需要用引号(单双都可)引起来
		5. html的标签不区分大小写，但是建议使用小写。

	* 代码：
		
		```
		<html>
		
			<head>
				<title>title</title>
			</head>
		
		
		
		​	<body>
		​		<FONT color='red'>Hello World</font><br/>
	​		
		​		<font color='green'>Hello World</font>
	​	
		​	</body>
		
		</html>
		```

### 文件标签：构成html最基本的标签

* ```html
  * html:html文档的根标签
  
      * head：头标签。用于指定html文档的一些属性。引入外部的资源
  
      * title：标题标签。
  
      * body：体标签
  
      * <!DOCTYPE html>：html5中定义该文档是html文档
  ```

### 文本标签：和文本有关的标签

* ```html
	* 注释：<!-- 注释内容 -->
	
	    * <h1> to <h6>：标题标签
	        * h1~h6:字体大小逐渐递减
	
	    * <p>：段落标签
	
	    * <br>：换行标签
	
	    * <hr>：展示一条水平线
	        * 属性：
	        	* color：颜色
	        	* width：宽度
	        	* size：高度
	        	* align：对其方式
	        		* center：居中
	        		* left：左对齐
	        		* right：右对齐
	
	    * <b>：字体加粗
	
    * <i>：字体斜体
	
	    * <font>:字体标签
	
	    * <center>:文本居中
	        * 属性：
	        	* color：颜色
	        	* size：大小
	        	* face：字体

	    * 属性定义：
	
	        * color：
	            1. 英文单词：red,green,blue
	            2. rgb(值1，值2，值3)：值的范围：0~255  如  rgb(0,0,255)
	            3. #值1值2值3：值的范围：00~FF之间。如： #FF00FF
	        * width：
	            1. 数值：width='20' ,数值的单位，默认是 px(像素)
	            2. 数值%：占比相对于父元素的比例
	
	    * 案例：公司简介
	
	        <!DOCTYPE html>
	        <html lang="ch">
	        <head>
	            <meta charset="UTF-8">
	            <title>黑马程序员简介</title>
	        </head>
	        <body>
	
	
	        <h1>
	            公司简介
	        </h1>
	        <hr color="#ffd700">
	
	
	        <p>
	        <font color="#FF0000">"中关村黑马程序员训练营"</font>是由<b><i>传智播客</i></b>联合中关村软件园、CSDN， 并委托传智播客进行教学实施的软件开发高端培训机构，致力于服务各大软件企业，解决当前软件开发技术飞速发展， 而企业招不到优秀人才的困扰。
	        </p>
	
	
	        <p>
	        目前，“中关村黑马程序员训练营”已成长为行业“学员质量好、课程内容深、企业满意”的移动开发高端训练基地， 并被评为中关村软件园重点扶持人才企业。
	        </p>
	
	
	        <p>
	
	
	        黑马程序员的学员多为大学毕业后，有理想、有梦想，想从事IT行业，而没有环境和机遇改变自己命运的年轻人。 黑马程序员的学员筛选制度，远比现在90%以上的企业招聘流程更为严格。任何一名学员想成功入学“黑马程序员”， 必须经历长达2个月的面试流程，这些流程中不仅包括严格的技术测试、自学能力测试，还包括性格测试、压力测试、 品德测试等等测试。毫不夸张地说，黑马程序员训练营所有学员都是精挑细选出来的。百里挑一的残酷筛选制度确 保学员质量，并降低企业的用人风险。
	        中关村黑马程序员训练营不仅着重培养学员的基础理论知识，更注重培养项目实施管理能力，并密切关注技术革新， 不断引入先进的技术，研发更新技术课程，确保学员进入企业后不仅能独立从事开发工作，更能给企业带来新的技术体系和理念。
	        </p>
	
	        <p>
	
	
	        一直以来，黑马程序员以技术视角关注IT产业发展，以深度分享推进产业技术成长，致力于弘扬技术创新，倡导分享、 开放和协作，努力打造高质量的IT人才服务平台。
	        </p>
	
	        <hr color="#ffd700">
	
	        <font color="gray" size="2">
	
	            <center>
	                江苏传智播客教育科技股份有限公司<br>
	                版权所有Copyright 2006-2018&copy;, All Rights Reserved 苏ICP备16007882
	            </center>
	
	        </font>
	
	</body>
			</html>
	```

### 图片标签

```html

* img：展示图片

    * 属性：

        * src：指定图片的位置

    * 代码：
        <!--展示一张图片 img-->

         <img src="image/jingxuan_2.jpg" align="right" alt="古镇" width="500" height="500"/>

         <!--
             相对路径

           * 以.开头的路径
             * ./：代表当前目录  ./image/1.jpg
             * ../:代表上一级目录
                 -->

         <img src="./image/jiangwai_1.jpg">

         <img src="../image/jiangwai_1.jpg">
```

### 列表标签

* * ```html
	    有序列表：
	    
	    * ol:
	        * li:
	    * 无序列表：
	        * ul:
	        * li:
	    ```
	
	    

### 链接标签

* ```html
		* a:定义一个超链接
	
	    * 属性：
	
	        * href：指定访问资源的URL(统一资源定位符)
            * target：指定打开资源的方式
	                * _self:默认值，在当前页面打开
	                * _blank：在空白页面打开

	    * 代码：
	        <!--超链接  a-->
	
	         <a href="http://www.itcast.cn">点我</a>
	         <br>
	
	         <a href="http://www.itcast.cn" target="_self">点我</a>
	         <br>
	         <a href="http://www.itcast.cn" target="_blank">点我</a>
	
	         <br>
	
	         <a href="./5_列表标签.html">列表标签</a><br>
	         <a href="mailto:itcast@itcast.cn">联系我们</a>
	
	         <br>
	         <a href="http://www.itcast.cn"><img src="image/jiangwai_1.jpg"></a>
	
	
	```

### div块级标签和span内联标签

* * ```
	    div:每一个div占满一整行。
	    
	    * span：文本信息在一行展示，行内标签 
	    ```

### 语义化标签：html5中为了提高程序的可读性，提供了一些标签。

		1. <header>：页眉
		2. <footer>：页脚
### 表格标签

* * ```html
		    table：定义表格
	    
	    * width：宽度
	        * border：边框
	        * cellpadding：定义内容和单元格的距离
	        * cellspacing：定义单元格之间的距离。如果指定为0，则单元格的线会合为一条、
	        * bgcolor：背景色
	        * align：对齐方式
	    * tr：定义行
	        * bgcolor：背景色
	        * align：对齐方式
	    * td：定义单元格
	        * colspan：合并列
	        * rowspan：合并行
	    * th：定义表头单元格
	    * <caption>：表格标题
	    * <thead>：表示表格的头部分
	    * <tbody>：表示表格的体部分
	    * <tfoot>：表示表格的脚部分
	  ```
	
	    

### 表单标签

* 表单：
    * 概念：用于采集用户输入的数据的。用于和服务器进行交互。
    * form：用于定义表单的。可以定义一个范围，范围代表采集用户数据的范围
           * 属性：
             * action：指定提交数据的URL
             * method:指定提交方式
                 * 分类：一共7种，2种比较常用
                     * get：
                         1. 请求参数会在地址栏中显示。会封装到请求行中(HTTP协议后讲解)。
                         2. 请求参数大小是有限制的。
                         3. 不太安全。
                     * post：
                         2. 请求参数不会再地址栏中显示。会封装在请求体中(HTTP协议后讲解)
                         3. 请求参数的大小没有限制。
                         4. 较为安全。

       ​      * 表单项中的数据要想被提交：必须指定其name属性


​		

 * 表单项标签：
     * input：可以通过type属性值，改变元素展示的样式
         * type属性：
             * text：文本输入框，默认值
                 * placeholder：指定输入框的提示信息，当输入框的内容发生变化，会自动清空提示信息	
                * password：密码输入框
                * radio:单选框
                    * 注意：
                        1. 要想让多个单选框实现单选的效果，则多个单选框的name属性值必须一样。
                        2. 一般会给每一个单选框提供value属性，指定其被选中后提交的值
                        3. checked属性，可以指定默认值
                * checkbox：复选框
                    * 注意：
                        1. 一般会给每一个单选框提供value属性，指定其被选中后提交的值
                        2. checked属性，可以指定默认值

                * file：文件选择框
                * hidden：隐藏域，用于提交一些信息。
                * 按钮：
                    * submit：提交按钮。可以提交表单
                    * button：普通按钮
                    * image：图片提交按钮
                        * src属性指定图片的路径	

            * label：指定输入项的文字描述信息
                * 注意：
                    * label的for属性一般会和 input 的 id属性值 对应。如果对应了，则点击label区域，会让input输入框获取焦点。
        * select: 下拉列表
            * 子元素：option，指定列表项

        * textarea：文本域
            * cols：指定列数，每一行有多少个字符
            * rows：默认多少行。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表单标签</title>
</head>
<body>

<form action="#" method="get">

    <label for="username"> 用户名 </label>：<input type="text" name="username" placeholder="请输入用户名" id="username"><br>
    密码：<input type="password" name="password" placeholder="请输入密码"><br>
    性别：<input type="radio" name="gender" value="male" >  男
         <input type="radio" name="gender" value="female" checked>  女
            <br>
    爱好：<input type="checkbox" name="hobby" value="shopping"> 逛街
        <input type="checkbox" name="hobby" value="java"  checked> Java
        <input type="checkbox" name="hobby" value="game"> 游戏<br>

    图片：<input type="file" name="file"><br>
    隐藏域：<input type="hidden" name="id" value="aaa"> <br>

    取色器：<input type="color" name="color"><br>
    生日：<input type="date" name="birthday"> <br>
    生日：<input type="datetime-local" name="birthday"> <br>
    邮箱：<input type="email" name="email"> <br>
    年龄：<input type="number" name="age"> <br>

    省份：<select name="province">
            <option value="">--请选择--</option>
            <option value="1">北京</option>
            <option value="2">上海</option>
            <option value="3" selected>陕西</option>
         </select><br>

    自我描述：
        <textarea cols="20" rows="5" name="des"></textarea>

    <br>
    <input type="submit" value="登录" >
    <input type="button" value="一个按钮" ><br>
    <input type="image" src="img/regbtn.jpg">


</form>

</body>
</html>
```

## CSS：页面美化和布局控制

1. 概念： Cascading Style Sheets 层叠样式表
	
* 层叠：多个样式可以作用在同一个html的元素上，同时生效
	
2. 好处：
	1. 功能强大
	2. 将内容展示和样式控制分离
		* 降低耦合度。解耦
		* 让分工协作更容易
		* 提高开发效率

3. CSS的使用：CSS与html结合方式
	1. 内联样式
		 * 在标签内使用style属性指定css代码
		 * 如：<div style="color:red;">hello css</div>
	2. 内部样式
		* 在head标签内，定义style标签，style标签的标签体内容就是css代码
		* 如：
			<style>
		        div{
		            color:blue;
		        }
		
		    </style>
			
			<div>hello css</div>
	3. 外部样式
		1. 定义css资源文件。
		2. 在head标签内，定义link标签，引入外部的资源文件
   	* 如：
	
	 		* a.css文件：
	 			div{
	 			    color:green;
	 			}
	 		<link rel="stylesheet" href="css/a.css">
	 		<div>hello css</div>
	 	<div>hello css</div>
	
	* 注意：
		* 1,2,3种方式 css作用范围越来越大
		* 1方式不常用，后期常用2,3
		* 3种格式可以写为：
			<style>
		        @import "css/a.css";
	    </style>
	
4. css语法：
	* 格式：
		选择器 {
			属性名1:属性值1;
			属性名2:属性值2;
			...
		}
	* 选择器:筛选具有相似特征的元素
	* 注意：
		* 每一对属性需要使用；隔开，最后一对属性可以不加；

选择器：筛选具有相似特征的元素
- * 分类：
    	1. 基础选择器
    		1. id选择器：选择具体的id属性值的元素.建议在一个html页面中id值唯一
    	        * 语法：#id属性值{}
    	    2. 元素选择器：选择具有相同标签名称的元素
    	        * 语法： 标签名称{}
    	        * 注意：id选择器优先级高于元素选择器
    	    3. 类选择器：选择具有相同的class属性值的元素。
    	        * 语法：.class属性值{}
    	        * 注意：类选择器选择器优先级高于元素选择器
    	2. 扩展选择器：
    		1. 选择所有元素：
    			* 语法： *{}
    		2. 并集选择器：
    			* 选择器1,选择器2{}
    		
    		3. 子选择器：筛选选择器1元素下的选择器2元素
    			* 语法：  选择器1 选择器2{}
    		4. 父选择器：筛选选择器2的父元素选择器1
    			* 语法：  选择器1 > 选择器2{}
			
    		5. 属性选择器：选择元素名称，属性名=属性值的元素
    			* 语法：  元素名称[属性名="属性值"]{}
			
    		6. 伪类选择器：选择一些元素具有的状态
    			* 语法： 元素:状态{}
    			* 如： <a>
    				* 状态：
    					* link：初始化的状态
    					* visited：被访问过的状态
    					* active：正在访问状态
    					* hover：鼠标悬浮状态

- 属性

- 1. 字体、文本

    	* font-size：字体大小
    	* color：文本颜色
    	* text-align：对其方式
    	* line-height：行高 
    2. 背景

    	* background：
    3. 边框

    	* border：设置边框，符合属性
    4. 尺寸

    	* width：宽度
    	* height：高度
    5. 盒子模型：控制布局

      * margin：外边距
      * padding：内边距
      	* 默认情况下内边距会影响整个盒子的大小
      	* box-sizing: border-box;  设置盒子的属性，让width和height就是最终盒子的大小
      
      * float：浮动
        * left
        * right

    ***案例***

    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>登陆案例</title>
    <!--    外部样式-->
        <link rel="stylesheet" href="../css/demo1.css">
    <!--    内部样式-->
    <!--    <style>
            body{
                background:url("../img/register_bg.png") no-repeat center;
                padding-top: 25px;
            }
            .lg_layout{
                width:900px;
                height: 500px;
                border: 8px solid #eeeeee;
                background-color: white;
                /*外边距*/
                margin: auto;/*水平居中*/
            }
            /*整体布局*/
            .lg_left {
                /*border: 1px solid red;*/
                float: left;
                margin: 15px;
            }
            .lg_center{
                float: left;
                 /*border: 1px solid red;*/
    
            }
    
            .lg_right{
                /*border: 1px solid red;*/
                float: right;
                padding-top: 400px;/*内边距*/
                margin: 15px;
    
            }
            /*左边布局*/
            .lg_left p:first-child{
                color:#FFD026;
                font-size: 20px;
            }
    
            .lg_left p:last-child{
                color:#A6A6A6;
                font-size: 20px;
            }
            .td_left{
                width: 100px;
                text-align: right;
                height: 45px;
            }
            /*中间布局*/
            .lg_form{
                margin: auto;
            }
            #username,#password,#email,#name,#tel,#birthday,#checkcode{
                width: 251px;
                height: 32px;
                border: 1px solid #A6A6A6 ;
                /*设置边框圆角*/
                border-radius: 5px;
                padding-left: 10px;
            }
            #checkcode{
                width: 110px;
            }
            #img_check{
                height: 32px;
                vertical-align: middle;/*垂直居中*/
            }
            #btn_sub{
                width: 150px;
                height: 40px;
                background-color: #FFD026;
                border: 1px solid #FFD026 ;
            }
            /*右边布局*/
            .td_right{
                padding-left: 50px ;
            }
    
            .lg_right > p:first-child{
                font-size: 15px;
    
            }
            .lg_right p a {
                color:pink;
            }
        </style>-->
    </head>
    <body>
        <div class="lg_layout">
            <div class="lg_left">
                <p>新用户注册</p>
                <p>USER REGISTER</p>
            </div>
            <div class="lg_center">
                <div class="lg_form">
                    <form action="#"method="post">
                        <table>
                            <tr>
                                <td class="td_left"><label for="username">用户名</label> </td>
                                <td class="td_right"><input type="text"name="username"id="username"placeholder="请输入用户名"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="password">密码</label></td>
                                <td class="td_right"><input type="password" name="password" id="password"placeholder="请输入密码"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="email">Email</label></td>
                                <td class="td_right"><input type="email" name="email" id="email"placeholder="请输入邮箱"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="name">姓名</label> </td>
                                <td class="td_right"><input type="text"name="name"id="name"placeholder="请输入姓名"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="tel">手机号</label> </td>
                                <td class="td_right"><input type="tel"name="tel"id="tel" placeholder="请输入手机号"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label>性别</label> </td>
                                <td class="td_right">
                                    <input type="radio"name="gender"value="male"checked>男
                                    <input type="radio"name="gender"value="female">女
                                </td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="birthday">出生日期</label> </td>
                                <td class="td_right"><input type="date"name="birthday"id="birthday"placeholder="请输入出生日期"></td>
                            </tr>
                            <tr>
                                <td class="td_left"><label for="checkcode">验证码</label></td>
                                <td class="td_right"><input type="text" name="checkcode" id="checkcode"
                                                            placeholder="请输入验证码">
                                    <img id="img_check" src="../img/verify_code.jpg">
                                </td>
                            </tr>
                            <tr>
                                <td colspan="2"align="center"><input type="submit" id="btn_sub"value="注册"></td>
                            </tr>
                        </table>
                    </form>
            </div>
            </div>
            <div class="lg_right">
                <p>已有账号？<a href="#">立即登录</a> </p>
            </div>
        </div>
    
    </body>
    
    ```


## JavaScript

```
* 概念：	一门客户端脚本语言
	* 运行在客户端浏览器中的。每一个浏览器都有JavaScript的解析引擎
	* 脚本语言：不需要编译，直接就可以被浏览器解析执行了

* 功能：
	* 可以来增强用户和html页面的交互过程，可以来控制html元素，让页面有一些动态的效果，增强用户的体验。

* JavaScript发展史：
	1. 1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为 ： C--	，后来更名为：ScriptEase
	2. 1995年，Netscape(网景)公司，开发了一门客户端脚本语言：LiveScript。后来，请来SUN公司的专家，修改LiveScript，命名为JavaScript
	3. 1996年，微软抄袭JavaScript开发出JScript语言
	4. 1997年，ECMA(欧洲计算机制造商协会)，制定出客户端脚本语言的标准：ECMAScript，就是统一了所有客户端脚本语言的编码方式。

	* JavaScript = ECMAScript + JavaScript自己特有的东西(BOM+DOM)
```

### ECMAScript：客户端脚本语言的标准

```
1. 基本语法：
	1. 与html结合方式
		1. 内部JS：
			* 定义<script>，标签体内容就是js代码
		2. 外部JS：
			* 定义<script>，通过src属性引入外部的js文件

		* 注意：
			1. <script>可以定义在html页面的任何地方。但是定义的位置会影响执行顺序。
			2. <script>可以定义多个。
	2. 注释
		1. 单行注释：//注释内容
		2. 多行注释：/*注释内容*/
	3. 数据类型：
		1. 原始数据类型(基本数据类型)：
			1. number：数字。 整数/小数/NaN(not a number 一个不是数字的数字类型)
			2. string：字符串。 字符串  "abc" "a" 'abc'
			3. boolean: true和false
			4. null：一个对象为空的占位符
			5. undefined：未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined
			
		2. 引用数据类型：对象
		
	4. 变量
		* 变量：一小块存储数据的内存空间
		* Java语言是强类型语言，而JavaScript是弱类型语言。
			* 强类型：在开辟变量存储空间时，定义了空间将来存储的数据的数据类型。只能存储固定类型的数据
			* 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，可以存放任意类型的数据。
		* 语法：
			* var 变量名 = 初始化值;
		
		* typeof运算符：获取变量的类型。
			* 注：null运算后得到的是object
	5. 运算符
		1. 一元运算符：只有一个运算数的运算符
			++，-- ， +(正号)  
			* ++ --: 自增(自减)
				* ++(--) 在前，先自增(自减)，再运算
				* ++(--) 在后，先运算，再自增(自减)
			* +(-)：正负号
		    * 注意：在JS中，如果运算数不是运算符所要求的类型，那么js引擎会自动的将运算数进行类型转换
                * 其他类型转number：
                    * string转number：按照字面值转换。如果字面值不是数字，则转为NaN（不是数字的数字）
                    * boolean转number：true转为1，false转为0
		2. 算数运算符
			+ - * / % ...

		3. 赋值运算符
			= += -+....

		4. 比较运算符
			> < >= <= == ===(全等于)
			* 比较方式
              1. 类型相同：直接比较
                  * 字符串：按照字典顺序比较。按位逐一比较，直到得出大小为止。
              2. 类型不同：先进行类型转换，再比较
                  * ===：全等于。在比较之前，先判断类型，如果类型不一样，则直接返回false
         
	2. 基本对象：
		1. Function：函数(方法)对象
            1. 创建：
                1. var fun = new Function(形式参数列表,方法体);  //忘掉吧
                2. 
                    function 方法名称(形式参数列表){
                        方法体
                    }

                3. 
                   var 方法名 = function(形式参数列表){
                        方法体
                   }
            2. 方法：

            3. 属性：
                length:代表形参的个数
            4. 特点：
                1. 方法定义是，形参的类型不用写,返回值类型也不写。
                2. 方法是一个对象，如果定义名称相同的方法，会覆盖
                3. 在JS中，方法的调用只与方法的名称有关，和参数列表无关
                4. 在方法声明中有一个隐藏的内置对象（数组），arguments,封装所有的实际参数
            5. 调用：
                方法名称(实际参数列表);
		
		2. Array:数组对象
            1. 创建：
                1. var arr = new Array(元素列表);
                2. var arr = new Array(默认长度);
                3. var arr = [元素列表];
            2. 方法
                join(参数):将数组中的元素按照指定的分隔符拼接为字符串
                push()	向数组的末尾添加一个或更多元素，并返回新的长度。
            3. 属性
                length:数组的长度
            4. 特点：
                1. JS中，数组元素的类型可变的。
                2. JS中，数组长度可变的。
		3. Boolean
		4. Date：日期对象
            1. 创建：
                var date = new Date();

            2. 方法：
                toLocaleString()：返回当前date对象对应的时间本地字符串格式
                getTime():获取毫秒值。返回当前如期对象描述的时间到1970年1月1日零点的毫秒值差
		5. Math：数学对象
            1. 创建：
                * 特点：Math对象不用创建，直接使用。  Math.方法名();

            2. 方法：
                random():返回 0 ~ 1 之间的随机数。 含0不含1
                ceil(x)：对数进行上舍入。
                floor(x)：对数进行下舍入。
                round(x)：把数四舍五入为最接近的整数。
            3. 属性：
                PI
		6. Number
		7. String
		8. RegExp：正则表达式对象
			1. 正则表达式：定义字符串的组成规则。
				1. 单个字符:[]
					如： [a] [ab] [a-zA-Z0-9_]
					* 特殊符号代表特殊含义的单个字符:
						\d:单个数字字符 [0-9]
						\w:单个单词字符[a-zA-Z0-9_]
				2. 量词符号：
					?：表示出现0次或1次
					*：表示出现0次或多次
					+：出现1次或多次
					{m,n}:表示 m<= 数量 <= n
						* m如果缺省： {,n}:最多n次
						* n如果缺省：{m,} 最少m次
				3. 开始结束符号
					* ^:开始
					* $:结束
			2. 正则对象：
				1. 创建
					1. var reg = new RegExp("正则表达式");
					2. var reg = /正则表达式/;
				2. 方法	
					1. test(参数):验证指定的字符串是否符合正则定义的规范	
		9. Global
			1. 特点：全局对象，这个Global中封装的方法不需要对象就可以直接调用。  方法名();
			2. 方法：
			    encodeURI():url编码
			    decodeURI():url解码

			    encodeURIComponent():url编码,编码的字符更多
			    decodeURIComponent():url解码

			    parseInt():将字符串转为数字
			        * 逐一判断每一个字符是否是数字，直到不是数字为止，将前边数字部分转为number
			    isNaN():判断一个值是否是NaN
			        * NaN六亲不认，连自己都不认。NaN参与的==比较全部问false

			    eval():将JavaScript 字符串，并把它作为脚本代码来执行。
            3. URL编码
               传智播客 =  %E4%BC%A0%E6%99%BA%E6%92%AD%E5%AE%A2
```
### BOM

```
1. 概念：Browser Object Model 浏览器对象模型
	* 将浏览器的各个组成部分封装成对象。

2. 组成：
	* Window：窗口对象
	* Navigator：浏览器对象
	* Screen：显示器屏幕对象
	* History：历史记录对象
	* Location：地址栏对象

3. Window：窗口对象
    1. 创建
    2. 方法
         1. 与弹出框有关的方法：
            alert()	显示带有一段消息和一个确认按钮的警告框。
            confirm()	显示带有一段消息以及确认按钮和取消按钮的对话框。
                * 如果用户点击确定按钮，则方法返回true
                * 如果用户点击取消按钮，则方法返回false
            prompt()	显示可提示用户输入的对话框。
                * 返回值：获取用户输入的值
         2. 与打开关闭有关的方法：
            close()	关闭浏览器窗口。
                * 谁调用我 ，我关谁
            open()	打开一个新的浏览器窗口
                * 返回新的Window对象
         3. 与定时器有关的方式
            setTimeout()	在指定的毫秒数后调用函数或计算表达式。
                * 参数：
                    1. js代码或者方法对象
                    2. 毫秒值
                * 返回值：唯一标识，用于取消定时器
            clearTimeout()	取消由 setTimeout() 方法设置的 timeout。

            setInterval()	按照指定的周期（以毫秒计）来调用函数或计算表达式。
            clearInterval()	取消由 setInterval() 设置的 timeout。


    3. 属性：
        1. 获取其他BOM对象：
            history
            location
            Navigator
            Screen:
        2. 获取DOM对象
            document
    4. 特点
        * Window对象不需要创建可以直接使用 window使用。 window.方法名();
        * window引用可以省略。  方法名();
4. Location：地址栏对象
	1. 创建(获取)：
		1. window.location
		2. location

	2. 方法：
		* reload()	重新加载当前文档。刷新
	3. 属性
		* href	设置或返回完整的 URL。
5. History：历史记录对象
    1. 创建(获取)：
        1. window.history
        2. history

    2. 方法：
        * back()	加载 history 列表中的前一个 URL。
        * forward()	加载 history 列表中的下一个 URL。
        * go(参数)	加载 history 列表中的某个具体页面。
            * 参数：
                * 正数：前进几个历史记录
                * 负数：后退几个历史记录
    3. 属性：
        * length	返回当前窗口历史列表中的 URL 数量。
```

### DOM

```
* 概念： Document Object Model 文档对象模型
	* 将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对标记语言文档进行CRUD的动态操作

* W3C DOM 标准被分为 3 个不同的部分：

	* 核心 DOM - 针对任何结构化文档的标准模型
		* Document：文档对象
		* Element：元素对象
		* Attribute：属性对象
		* Text：文本对象
		* Comment:注释对象

		* Node：节点对象，其他5个的父对象
	* XML DOM - 针对 XML 文档的标准模型
	* HTML DOM - 针对 HTML 文档的标准模型
* 功能：控制html文档的内容
* 获取页面标签(元素)对象：Element
	* document.getElementById("id值"):通过元素的id获取元素对象

* 操作Element对象：
	1. 修改属性值：
		1. 明确获取的对象是哪一个？
		2. 查看API文档，找其中有哪些属性可以设置
	2. 修改标签体内容：
		* 属性：innerHTML
		1. 获取元素对象
		2. 使用innerHTML属性修改标签体内容
* 核心DOM模型：
	* Document：文档对象
		1. 创建(获取)：在html dom模型中可以使用window对象来获取
			1. window.document
			2. document
		2. 方法：
			1. 获取Element对象：
				1. getElementById()	： 根据id属性值获取元素对象。id属性值一般唯一
				2. getElementsByTagName()：根据元素名称获取元素对象们。返回值是一个数组
				3. getElementsByClassName():根据Class属性值获取元素对象们。返回值是一个数组
				4. getElementsByName(): 根据name属性值获取元素对象们。返回值是一个数组
			2. 创建其他DOM对象：
				createAttribute(name)
            	createComment()
            	createElement()
            	createTextNode()
		3. 属性
	* Element：元素对象
		1. 获取/创建：通过document来获取和创建
		2. 方法：
			1. removeAttribute()：删除属性
			2. setAttribute()：设置属性
	* Node：节点对象，其他5个的父对象
		* 特点：所有dom对象都可以被认为是一个节点
		* 方法：
			* CRUD dom树：
				* appendChild()：向节点的子节点列表的结尾添加新的子节点。
				* removeChild()	：删除（并返回）当前节点的指定子节点。
				* replaceChild()：用新节点替换一个子节点。
		* 属性：
			* parentNode 返回节点的父节点。
* HTML DOM
	1. 标签体的设置和获取：innerHTML
	2. 使用html元素对象的属性
	3. 控制元素样式
		1. 使用元素的style属性来设置
			如：
				 //修改样式方式1
		        div1.style.border = "1px solid red";
		        div1.style.width = "200px";
		        //font-size--> fontSize
		        div1.style.fontSize = "20px";
		2. 提前定义好类选择器的样式，通过元素的className属性来设置其class属性值。
```

### 事件监听机制

* 概念：某些组件被执行了某些操作后，触发某些代码的执行。	
	* 事件：某些操作。如： 单击，双击，键盘按下了，鼠标移动了
	* 事件源：组件。如： 按钮 文本输入框...
	* 监听器：代码。
	* 注册监听：将事件，事件源，监听器结合在一起。 当事件源上发生了某个事件，则触发执行某个监听器代码。

* 功能： 某些组件被执行了某些操作后，触发某些代码的执行。
	* 造句：  xxx被xxx,我就xxx
		* 我方水晶被摧毁后，我就责备对友。
		* 敌方水晶被摧毁后，我就夸奖自己。

* 如何绑定事件
	1. 直接在html标签上，指定事件的属性(操作)，属性值就是js代码
		1. 事件：onclick--- 单击事件

	2. 通过js获取元素对象，指定事件属性，设置一个函数

* 常见的事件：
	1. 点击事件：
		1. onclick：单击事件
		2. ondblclick：双击事件
	2. 焦点事件
		1. onblur：失去焦点
		2. onfocus:元素获得焦点。

	3. 加载事件：
		1. onload：一张页面或一幅图像完成加载。

	4. 鼠标事件：
		1. onmousedown	鼠标按钮被按下。
		2. onmouseup	鼠标按键被松开。
		3. onmousemove	鼠标被移动。
		4. onmouseover	鼠标移到某元素之上。
		5. onmouseout	鼠标从某元素移开。
	
	5. 键盘事件：
		1. onkeydown	某个键盘按键被按下。	
		2. onkeyup		某个键盘按键被松开。
		3. onkeypress	某个键盘按键被按下并松开。
	
	6. 选择和改变
		1. onchange	域的内容被改变。
		2. onselect	文本被选中。
	
	7. 表单事件：
		1. onsubmit	确认按钮被点击。
		2. onreset	重置按钮被点击。

```

	* 代码：
		<body>
			<img id="light" src="img/off.gif"  onclick="fun();">
			<img id="light2" src="img/off.gif">
			
			<script>
			    function fun(){
			        alert('我被点了');
			        alert('我又被点了');
			    }
			
			    function fun2(){
			        alert('咋老点我？');
			    }
			
			    //1.获取light2对象
			    var light2 = document.getElementById("light2");
			    //2.绑定事件
			    light2.onclick = fun2;
			    			</script>
		</body>

* 案例1：电灯开关
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>电灯开关</title>
	
	</head>
	<body>
	
	<img id="light" src="img/off.gif">
	
	<script>
	    /*
	        分析：
	            1.获取图片对象
	            2.绑定单击事件
	            3.每次点击切换图片
	                * 规则：
	                    * 如果灯是开的 on,切换图片为 off
	                    * 如果灯是关的 off,切换图片为 on
	                * 使用标记flag来完成
	
	     */
	
	    //1.获取图片对象
	    var light = document.getElementById("light");
	
	    var flag = false;//代表灯是灭的。 off图片
	
	    //2.绑定单击事件
	    light.onclick = function(){
	        if(flag){//判断如果灯是开的，则灭掉
	            light.src = "img/off.gif";
	            flag = false;
	
	        }else{
	            //如果灯是灭的，则打开
	
	            light.src = "img/on.gif";
	            flag = true;
	        }
	        	    }
	    
	</script>
	</body>
	</html>
```

## Bootstrap框架

1. 概念： 一个前端开发的框架，Bootstrap，来自 Twitter，是目前很受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、JavaScript 的，它简洁灵活，使得 Web 开发更加快捷。
	* 框架:一个半成品软件，开发人员可以在框架基础上，在进行开发，简化编码。
	* 好处：
		1. 定义了很多的css样式和js插件。我们开发人员直接可以使用这些样式和插件得到丰富的页面效果。
		2. 响应式布局。
			* 同一套页面可以兼容不同分辨率的设备。

2. 快速入门
	1. 下载Bootstrap
	
	2. 在项目中将这三个文件夹复制
	
	3. 创建html页面，引入必要的资源文件
	
	    ```
	    2. 1. 
	    
	    	<!DOCTYPE html>
	    	<html lang="zh-CN">
	    	<head>
	    	    <meta charset="utf-8">
	    	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    	    <meta name="viewport" content="width=devaice-width, initial-scale=1">
	    	    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
	    	    <title>Bootstrap HelloWorld</title>
	    
	    ​	    <!-- Bootstrap -->
	    ​	    <link href="css/bootstrap.min.css" rel="stylesheet">
	    
	    ​	    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
	    
	    	    <script src="js/jquery-3.2.1.min.js"></script>
	    
	    ​	    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
	    
	    	    <script src="js/bootstrap.min.js"></script>
	    
	    ​	</head>
	    ​	<body>
	    ```

响应式布局

* 同一套页面可以兼容不同分辨率的设备。
* 实现：依赖于栅格系统：将一行平均分成12个格子，可以指定元素占几个格子
* 步骤：
	1. 定义容器。相当于之前的table、
		* 容器分类：
			1. container：两边留白
			2. container-fluid：每一种设备都是100%宽度
	2. 定义行。相当于之前的tr   样式：row
	3. 定义元素。指定该元素在不同的设备上，所占的格子数目。样式：col-设备代号-格子数目
		* 设备代号：
			1. xs：超小屏幕 手机 (<768px)：col-xs-12
			2. sm：小屏幕 平板 (≥768px)
			3. md：中等屏幕 桌面显示器 (≥992px)
			4. lg：大屏幕 大桌面显示器 (≥1200px)

	* 注意：
		1. 一行中如果格子数目超过12，则超出部分自动换行。
		2. 栅格类属性可以向上兼容。栅格类适用于与屏幕宽度大于或等于分界点大小的设备。
		3. 如果真实设备宽度小于了设置栅格类属性的设备代码的最小值，会一个元素沾满一整行。

CSS样式和JS插件

1. 全局CSS样式：
	* 按钮：class="btn btn-default"
	* 图片：
		*  class="img-responsive"：图片在任意尺寸都占100%
		*  图片形状
			*  <img src="..." alt="..." class="img-rounded">：方形
			*  <img src="..." alt="..." class="img-circle"> ： 圆形
			*  <img src="..." alt="..." class="img-thumbnail"> ：相框
	* 表格
		* table
		* table-bordered
		* table-hover
	* 表单
		* 给表单项添加：class="form-control" 
2. 组件：
	* 导航条
	* 分页条
3. 插件：
	* 轮播图

## XML

1. 概念：Extensible Markup Language 可扩展标记语言
	* 可扩展：标签都是自定义的。 <user>  <student>

	* 功能
		* 存储数据
			1. 配置文件
			2. 在网络中传输
	* xml与html的区别
		1. xml标签都是自定义的，html标签是预定义。
		2. xml的语法严格，html语法松散
		3. xml是存储数据的，html是展示数据

	* w3c:万维网联盟

2. 语法：
  * 基本语法：

  	1. xml文档的后缀名 .xml
  	2. xml第一行必须定义为文档声明
  	3. xml文档中有且仅有一个根标签
  	4. 属性值必须使用引号(单双都可)引起来
  	5. 标签必须正确关闭
  	6. xml标签名称区分大小写

  * 快速入门：

  	```
  	<?xml version='1.0' ?>
  	<users>
  		<user id='1'>
  			<name>zhangsan</name>
  			<age>23</age>
  			<gender>male</gender>
  			<br/>
  		</user>


  	
  		<user id='2'>
  			<name>lisi</name>
  			<age>24</age>
  			<gender>female</gender>
  		</user>
  	
  	</users>
  	```


  	
  	
  * 组成部分：
    1. 文档声明
    	1. 格式：<?xml 属性列表 ?>
    	2. 属性列表：
    		* version：版本号，必须的属性
    		* encoding：编码方式。告知解析引擎当前文档使用的字符集，默认值：ISO-8859-1
    		* standalone：是否独立
    			* 取值：
    				* yes：不依赖其他文件
    				* no：依赖其他文件
    2. 指令(了解)：结合css的
    	* <?xml-stylesheet type="text/css" href="a.css" ?>
    3. 标签：标签名称自定义的
    	* 规则：
    		* 名称可以包含字母、数字以及其他的字符 
    		* 名称不能以数字或者标点符号开始 
    		* 名称不能以字母 xml（或者 XML、Xml 等等）开始 
    		* 名称不能包含空格 

    4. 属性：
    	id属性值唯一
    5. 文本：
    	* CDATA区：在该区域中的数据会被原样展示
    		* 格式：  <![CDATA[ 数据 ]]>
    * 约束：规定xml文档的书写规则
    * 作为框架的使用者(程序员)：
    	1. 能够在xml中引入约束文档
    	2. 能够简单的读懂约束文档

    * 分类：
      1. DTD:一种简单的约束技术
      2. Schema:一种复杂的约束技术
       * * * * ```
                       DTD
                       
                       * 引入dtd文档到xml文档中
                       
                           * 内部dtd：将约束规则定义在xml文档中
                           * 外部dtd：将约束的规则定义在外部的dtd文件中
                               * 本地：<!DOCTYPE 根标签名 SYSTEM "dtd文件的位置">
                               * 网络：<!DOCTYPE 根标签名 PUBLIC "dtd文件名字" "dtd文件的位置URL">
                  ```
                  
                  ​     

               

       * ```
           Schema:
           
           * 引入：
               1.填写xml文档的根元素
               2.引入xsi前缀.  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          3.引入xsd文件命名空间.  xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd"
               4.为每一个xsd约束声明一个前缀,作为标识  xmlns="http://www.itcast.cn/xml" 
           
           <students   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns="http://www.itcast.cn/xml"
               xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd">
          ```
          
           
3. 解析：操作xml文档，将文档中的数据读取到内存中
	* 操作xml文档
		1. 解析(读取)：将文档中的数据读取到内存中
		2. 写入：将内存中的数据保存到xml文档中。持久化的存储

	* 解析xml的方式：
		1. DOM：将标记语言文档一次性加载进内存，在内存中形成一颗dom树
			* 优点：操作方便，可以对文档进行CRUD的所有操作
			* 缺点：占内存
		2. SAX：逐行读取，基于事件驱动的。
			* 优点：不占内存。
			* 缺点：只能读取，不能增删改
    * xml常见的解析器：
        1. JAXP：sun公司提供的解析器，支持dom和sax两种思想
        2. DOM4J：一款非常优秀的解析器
        3. Jsoup：jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可             通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。
        4. PULL：Android操作系统内置的解析器，sax方式的。
    	* Jsoup：jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。
		* 快速入门：
			* ```
				* * 步骤：
				        1. 导入jar包
				        2. 获取Document对象
				        3. 获取对应的标签Element对象
	       		```
		 4. 获取数据
				
	       		* 代码：
	       		
	       		```
	       		    //2.1获取student.xml的path
	       		​     String path = JsoupDemo1.class.getClassLoader().getResource("student.xml").getPath();
				​     //2.2解析xml文档，加载文档进内存，获取dom树--->Document
	       	  ​     Document document = Jsoup.parse(new File(path), "utf-8");
	       		​     //3.获取元素对象 Element
	       		   Elements elements = document.getElementsByTag("name");
	       		
	       		 System.out.println(elements.size());
	       		 //3.1获取第一个name的Element对象
				 Element element = elements.get(0);
		 //3.2获取数据
				 String name = element.text();
				 System.out.println(name);
				```
				
				
				
			
		
	* 对象的使用：
		1. Jsoup：工具类，可以解析html或xml文档，返回Document
			* parse：解析html或xml文档，返回Document
				* parse(File in, String charsetName)：解析xml或html文件的。
				* parse(String html)：解析xml或html字符串
				* parse(URL url, int timeoutMillis)：通过网络路径获取指定的html或xml的文档对象
		2. Document：文档对象。代表内存中的dom树
			* 获取Element对象
				* getElementById(String id)：根据id属性值获取唯一的element对象
				* getElementsByTag(String tagName)：根据标签名称获取元素对象集合
				* getElementsByAttribute(String key)：根据属性名称获取元素对象集合
				* getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合
		3. Elements：元素Element对象的集合。可以当做 ArrayList<Element>来使用
		4. Element：元素对象
		1. 获取子元素对象
				* getElementById(String id)：根据id属性值获取唯一的element对象
				* getElementsByTag(String tagName)：根据标签名称获取元素对象集合
				* getElementsByAttribute(String key)：根据属性名称获取元素对象集合
				* getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合
	
			2. 获取属性值
				* String attr(String key)：根据属性名称获取属性值
			3. 获取文本内容
				* String text():获取文本内容
				* String html():获取标签体的所有内容(包括字标签的字符串内容)
		5. Node：节点对象
			* 是Document和Element的父类
	* 快捷查询方式：
		1. selector:选择器
			* 使用的方法：Elements	select(String cssQuery)
				* 语法：参考Selector类中定义的语法
		2. XPath：XPath即为XML路径语言，它是一种用来确定XML（标准通用标记语言的子集）文档中某部分位置的语言
			* 使用Jsoup的Xpath需要额外导入jar包。
			
			* 查询w3cshool参考手册，使用xpath的语法完成查询
			
		   * ```
		   	1. * 1. * 代码：
		                     //1.获取student.xml的path
		                     String path = JsoupDemo6.class.getClassLoader().getResource("student.xml").getPath();
		                        //2.获取Document对象
		                      Document document = Jsoup.parse(new File(path), "utf-8");
		    
		                        //3.根据document对象，创建JXDocument对象
		                      JXDocument jxDocument = new JXDocument(document);
		     
		                        //4.结合xpath语法查询
		                        //4.1查询所有student标签
		                        List<JXNode> jxNodes = jxDocument.selN("//student");
		                     for (JXNode jxNode : jxNodes) {
		                            System.out.println(jxNode);
		                   }
		     
		                      System.out.println("--------------------");
		     
		                        //4.2查询所有student标签下的name标签
		                        List<JXNode> jxNodes2 = jxDocument.selN("//student/name");
		                     for (JXNode jxNode : jxNodes2) {
		                            System.out.println(jxNode);
		                   }
		     
		                      System.out.println("--------------------");
		     
		                        //4.3查询student标签下带有id属性的name标签
		                        List<JXNode> jxNodes3 = jxDocument.selN("//student/name[@id]");
		                        for (JXNode jxNode : jxNodes3) {
		                            System.out.println(jxNode);
		                     }
		                        System.out.println("--------------------");
		                      //4.4查询student标签下带有id属性的name标签 并且id属性值为itcast
		     
		                        List<JXNode> jxNodes4 = jxDocument.selN("//student/name[@id='itcast']");
		                        for (JXNode jxNode : jxNodes4) {
		                            System.out.println(jxNode);
		                        }
		     
		     ​	
		     ```
		     
		     
		     


## web服务器软件：Tomcat

	* 服务器：安装了服务器软件的计算机
	* 服务器软件：接收用户的请求，处理请求，做出响应
	* web服务器软件：接收用户的请求，处理请求，做出响应。
		* 在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目
		* web容器


	* 常见的java相关的web服务器软件：
		* webLogic：oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
		* webSphere：IBM公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
		* JBOSS：JBOSS公司的，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
		* Tomcat：Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的JavaEE规范servlet/jsp。开源的，免费的。


	* JavaEE：Java语言在企业级开发中使用的技术规范的总和，一共规定了13项大的规范
	
	* Tomcat：web服务器软件
		1. 下载：http://tomcat.apache.org/
		2. 安装：解压压缩包即可。
			* 注意：安装目录建议不要有中文和空格
		3. 卸载：删除目录就行了
		4. 启动：
			* bin/startup.bat ,双击运行该文件即可
			* 访问：浏览器输入：http://localhost:8080 回车访问自己
							  http://别人的ip:8080 访问别人
			
			* 可能遇到的问题：
				1. 黑窗口一闪而过：
					* 原因： 没有正确配置JAVA_HOME环境变量
					* 解决方案：正确配置JAVA_HOME环境变量
	
				2. 启动报错：
					1. 暴力：找到占用的端口号，并且找到对应的进程，杀死该进程
						* netstat -ano
					2. 温柔：修改自身的端口号
						* conf/server.xml
						* <Connector port="8888" protocol="HTTP/1.1"
			               connectionTimeout="20000"
			               redirectPort="8445" />
						* 一般会将tomcat的默认端口号修改为80。80端口号是http协议的默认端口号。
							* 好处：在访问时，就不用输入端口号
		5. 关闭：
			1. 正常关闭：
				* bin/shutdown.bat
				* ctrl+c
			2. 强制关闭：
				* 点击启动窗口的×
		6. 配置:
			* 部署项目的方式：
				1. 直接将项目放到webapps目录下即可。
					* /hello：项目的访问路径-->虚拟目录
					* 简化部署：将项目打成一个war包，再将war包放置到webapps目录下。
						* war包会自动解压缩
	
				2. 配置conf/server.xml文件
					在<Host>标签体中配置
					<Context docBase="D:\hello" path="/hehe" />
					* docBase:项目存放的路径
					* path：虚拟目录
	
				3. 在conf\Catalina\localhost创建任意名称的xml文件。在文件中编写
					<Context docBase="D:\hello" />
					* 虚拟目录：xml文件的名称
			
			* 静态项目和动态项目：
				* 目录结构
					* java动态项目的目录结构：
						-- 项目的根目录
							-- WEB-INF目录：
								-- web.xml：web项目的核心配置文件
								-- classes目录：放置字节码文件的目录
								-- lib目录：放置依赖的jar包


	* 将Tomcat集成到IDEA中，并且创建JavaEE的项目，部署项目。
			1. IDEA会为每一个tomcat部署的项目单独建立一份配置文件
		* 查看控制台的log：Using CATALINA_BASE:   "C:\Users\fqy\.IntelliJIdea2018.1\system\tomcat\_itcast"
	
	        2. 工作空间项目    和     tomcat部署的web项目
	            * tomcat真正访问的是“tomcat部署的web项目”，"tomcat部署的web项目"对应着"工作空间项目" 的web目录下的所有资源
	            * WEB-INF目录下的资源不能被浏览器直接访问。
	        3. 断点调试：使用"小虫子"启动 dubug 启动





## Servlet：  server applet

	* 概念：运行在服务器端的小程序
		* Servlet就是一个接口，定义了Java类被浏览器访问到(tomcat识别)的规则。
		* 将来我们自定义一个类，实现Servlet接口，复写方法。


	* 快速入门：
		1. 创建JavaEE项目
		2. 定义一个类，实现Servlet接口
			* public class ServletDemo1 implements Servlet
		3. 实现接口中的抽象方法
		4. 配置Servlet
			 在web.xml中配置：
		    <!--配置Servlet -->
		    <servlet>
		        <servlet-name>demo1</servlet-name>
		        <servlet-class>cn.itcast.web.servlet.ServletDemo1</servlet-class>
		    </servlet>
		
		    <servlet-mapping>
		        <servlet-name>demo1</servlet-name>
		        <url-pattern>/demo1</url-pattern>
		    </servlet-mapping>
	
	* 执行原理：
		1. 当服务器接受到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet的资源路径
		2. 查找web.xml文件，是否有对应的<url-pattern>标签体内容。
		3. 如果有，则在找到对应的<servlet-class>全类名
		4. tomcat会将字节码文件加载进内存，并且创建其对象
		5. 调用其方法
	
	* Servlet中的生命周期方法：
		1. 被创建：执行init方法，只执行一次
			* Servlet什么时候被创建？
				* 默认情况下，第一次被访问时，Servlet被创建
				* 可以配置执行Servlet的创建时机。
					* 在<servlet>标签下配置
						1. 第一次被访问时，创建
	                		* <load-on-startup>的值为负数
			            2. 在服务器启动时，创建
			                * <load-on-startup>的值为0或正整数
			    * Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
				* 多个用户同时访问时，可能存在线程安全问题。
				* 解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要对修改值
	
		2. 提供服务：执行service方法，执行多次
			* 每次访问Servlet时，Service方法都会被调用一次。
		3. 被销毁：执行destroy方法，只执行一次
			* Servlet被销毁时执行。服务器关闭时，Servlet被销毁
			* 只有服务器正常关闭时，才会执行destroy方法。
			* destroy方法在Servlet被销毁之前执行，一般用于释放资源
	
	* Servlet3.0：
		* 好处：
			* 支持注解配置。可以不需要web.xml了。
	
		* 步骤：
			1. 创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml
			2. 定义一个类，实现Servlet接口
			3. 复写方法
			4. 在类上使用@WebServlet注解，进行配置
				* @WebServlet("资源路径")   


				@Target({ElementType.TYPE})
				@Retention(RetentionPolicy.RUNTIME)
				@Documented
				public @interface WebServlet {
				    String name() default "";//相当于<Servlet-name>
				
				    String[] value() default {};//代表urlPatterns()属性配置
				
				    String[] urlPatterns() default {};//相当于<url-pattern>
				
				    int loadOnStartup() default -1;//相当于<load-on-startup>
				
				    WebInitParam[] initParams() default {};
				
				    boolean asyncSupported() default false;
				
				    String smallIcon() default "";
				
				    String largeIcon() default "";
				
				    String description() default "";
				
				    String displayName() default "";
				}
