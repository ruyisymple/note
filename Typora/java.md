[TOC]

# 基本函数

### 输入nextLine

Java中Scanner类中的方法next()和nextLine()都是吸取输入台输入的字符，区别：

next()不会吸取字符前/后的空格/Tab键，只吸取字符，开始吸取字符（字符前后不算）直到遇到空格/Tab键/回车截止吸取；

nextLine()吸取字符前后的空格/Tab键，回车键截止

### 垃圾回收 重写finalize(已弃用)

1) 当对象被回收时，系统自动调用该对象的 finalize 方法。子类可以重写该方法，做一些释放资源的操作

2) 什么时候被回收：当某个对象没有任何引用时，则 jvm 就认为这个对象是一个垃圾对象，就会使用垃圾回收机制来 销毁该对象，在销毁该对象前，会先调用 finalize 方法。

 3) 垃圾回收机制的调用，是由系统来决定(即有自己的 GC 算法), 也可以通过 System.gc() 主动触发垃圾回收机制，

### 当前时间差 System.currentTimeMillis();

```java
public static long currentTimeMillis()
返回以毫秒为单位的当前时间。注意，当返回值的时间单位是毫秒时，值的粒度取决于底层操作系统，并且粒度可能更大。例如，许多操作系统以几十毫秒为单位测量时间。 
返回：
当前时间与协调世界时 1970 年 1 月 1 日午夜之间的时间差（以毫秒为单位测量）。
```

//得到开始的时间 精确毫秒

long start = System.currentTimeMillis()

//得的结束的时间 

long end = System.currentTimeMillis(); 

System.out.println("任务执行时间 "\+ (end - start)）

# 数据类型

### 数组

##### 排序

Arrays.sort(a); // 使用快排

##### 长度

a.length  //长度

### String

##### 长度

s.length()  //长度

##### 取位数

s.charAt(index)  //取出每一位0~s.length()-1;

##### 字符串是否相等

```
public boolean equals(Object anObject)
将此字符串与指定的对象比较。当且仅当该参数不为 null，并且是与此对象表示相同字符序列的 String 对象时，结果才为 true。
```

##### 字符串比较

```
public int compareTo(String anotherString)按字典顺序比较两个字符串。该比较基于字符串中各个字符的 Unicode 值。按字典顺序将此 String 对象表示的字符序列与参数字符串所表示的字符序列进行比较。如果按字典顺序此 String 对象位于参数字符串之前，则比较结果为一个负整数。如果按字典顺序此 String 对象位于参数字符串之后，则比较结果为一个正整数。如果这两个字符串相等，则结果为 0；compareTo 只在方法 equals(Object) 返回 true 时才返回 0。 
这是字典排序的定义。如果这两个字符串不同，那么它们要么在某个索引处的字符不同（该索引对二者均为有效索引），要么长度不同，或者同时具备这两种情况。如果它们在一个或多个索引位置上的字符不同，假设 k 是这类索引的最小值；则在位置 k 上具有较小值的那个字符串（使用 < 运算符确定），其字典顺序在其他字符串之前。在这种情况下，compareTo 返回这两个字符串在位置 k 处两个char 值的差，即值： 

 this.charAt(k)-anotherString.charAt(k)
 如果没有字符不同的索引位置，则较短字符串的字典顺序在较长字符串之前。在这种情况下，compareTo 返回这两个字符串长度的差，即值： 
 this.length()-anotherString.length()

```



##### String和int的转换

String转int：Integer.valueOf（String）或者 **Integer.praseInt(String)**

int转String：**String s = String.valueOf(i); ** **String s = Integer.toString(i);**  或者 int+' '

##### String 转 char

怎么把字符串转成字符 char -> 含义是指 把字符串的第一个字符得到 

 System.out.println(s5.charAt(0));//解读 s5.charAt(0) 得到 s5 字符串的第一个字符 '1'

```
public char charAt(int index)
返回指定索引处的 char 值。索引范围为从 0 到 length() - 1。序列的第一个 char 值位于索引 0 处，第二个位于索引 1 处，依此类推，这类似于数组索引
```

##### 字符串和字符数组转化

```
字符串转换为字符数组
char[ ] ch=s.toCharArray();
字符数组转化为字符串
String str=string.valueOf(c);
```



# 运算

### i++ 

```java
// int i = 1;//i->1
// i = i++; //规则使用临时变量: (1) temp=i;(2) i=i+1;(3)i=temp;
// System.out.println(i); // 1
// int i=1;
// i=++i; //规则使用临时变量: (1) i=i+1;(2) temp=i;(3)i=temp;
// System.out.println(i); //
```

### instanceOf

 比较操作符，用于判断对象的运行类型是否为 XX 类型或 XX 类型的子类型

```java
class Annimal{}
class Dog entends Annimal{}
//1
Annimal annimal = new Dog();//左边Annimal为编译类型，右边Dog为运行类型
System.out.println(annimal instanceOf Annimal);//true
System.out.println(annimal instanceOf Dog);//true
//2
Dog dog = new Dog();
System.out.println(annimal instanceOf Annimal);//true
System.out.println(annimal instanceOf Dog);//true
```

### 三元运算符

三元运算符是一个整体

Object obj = true ? new Integer(2) : new Double(1.0)

执行的是new Integer(2) 但结果是2.0 ，自动向高精度转换（Double)

# 标签+break（continue)

可以指定跳出某个循环(语句块)

```java
label1:
	for(int i=1;i<n;i++){
        label2:
        	for(int j=1;j<i;j++){
                执行语句；
                    if(...)
                        break label2;//可以指定跳出某个循环，默认最近的循环
            }
    }
```

# 可变参数（类似数组参数）

基本概念： java 允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法。 就可以通过可变参数实现 

基本语法： 访问修饰符 返回类型 方法名(数据类型... 形参名) { }

```java
//1. int... 表示接受的是可变参数，类型是 int ,即可以接收多个 int(0-多)
//2. 使用可变参数时，可以当做数组来使用 即 nums 可以当做数组
//3. 遍历 nums 求和即可
public int sum(int... nums) {
//System.out.println("接收的参数个数=" + nums.length);
	int res = 0;
	for(int i = 0; i < nums.length; i++) {
		res += nums[i];
	}
	return res;
}
//调用
int n = sum(1,2,3);
int n = sum();
```

细节：可变参数的实参可以为数组

​			可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数在最后

​			一个形参列表中只能出现一个可变参数

# java反编译指令（javap)

用法: javap <options> <classes>
其中, 可能的选项包括:
  -help  --help  -?        输出此用法消息
  -version                 版本信息
  -v  -verbose             输出附加信息
  -l                       输出行号和本地变量表
  -public                  仅显示公共类和成员
  -protected               显示受保护的/公共类和成员
  -package                 显示程序包/受保护的/公共类
                           和成员 (默认)
  -p  -private             显示所有类和成员
  -c                       对代码进行反汇编
  -s                       输出内部类型签名
  -sysinfo                 显示正在处理的类的
                           系统信息 (路径, 大小, 日期, MD5 散列)
  -constants               显示静态最终常量
  -classpath <path>        指定查找用户类文件的位置
  -bootclasspath <path>    覆盖引导类文件的位置

# super和this

super 调用方法或属性 从父类开始向上查找（子类访问父类对象），若在构造器中须首行

this  调用方法或属性 从本类开始向上查找（表示当前对象），若在构造器中须首行

如果子类和父类方法同名，就近原则

# 重写和重载

重写：在父类和子类之间，方法名同，形参列表同，返回值类型:子类重写的方法，返回值类型和父类一致或为父类的子类，修饰符：子类不能缩小父类的方法的访问范围

重载：在本类，   方法名同，形参列表：类型，个数，顺序至少有一种不同，返回值类型:无要求，修饰符：无要求

# 多态

1) 方法的多态  重写和重载就体现多态

2) 对象的多态 (核心，困难，重点)

class A{}

class B entends A{}

class C entends A{}

一个对象的编译类型和运行类型不一致	(A a = new B()  左边A为编译类型，右边B为运行类型）、

编译类型不能变，运行类型可以变；（ a = new C())

### 向上转型和向下转型

向上转型 ：(A a = new B()  ）可以调用父类A中的所有成员（遵守访问权限）,不能调用子类B中特有的成员     (一般是调用子类重写的父类方法)

向下转型 ：B b = (B) a 只能强转父类引用，不能是对象（如不能 B b = (B) new A), 父类引用必须是只想目标类型的对象（如不能 A a = new C())，可以调用子类中所有成员

### 应用（多态数组、多态参数）

**子类父类共有的使用动态绑定（系统自动（重写，就近原则）），子类特有的使用向下转型**

##### 动态绑定

​				当调用对象的方法时，该方法会和对象的内存地址（运行类型）绑定

​				当调用对象属性时，没有动态绑定，哪里声明，哪里使用

##### 多态数组

数组的定义类型为父类类型，里面保存的实际元素类型为子类类型

```java
//现有一个继承结构如下：要求创建 1 个 Person 对象、2 个 Student 对象和 2 个 Teacher 对象, 统一放在数组
//中，并调用每个对象
Person[] persons = new Person[5];
persons[0] = new Person("jack", 20);
persons[1] = new Student("mary", 18, 100);
persons[2] = new Student("smith", 19, 30.1);
persons[3] = new Teacher("scott", 30, 20000);
persons[4] = new Teacher("king", 
for (int i = 0; i < persons.length; i++) {
//老师提示: person[i] 编译类型是 Person ,运行类型是是根据实际情况有 JVM 来判断
	System.out.println(persons[i].say());											//动态绑定机制
//这里大家聪明. 使用 类型判断 + 向下转型. 
    if(persons[i] instanceof Student) {		//判断 person[i] 的运行类型是不是 // Student
		Student student = (Student)persons[i];										//向下转型
		student.study();
		//小伙伴也可以使用一条语句 ((Student)persons[i]).study();
	} else if(persons[i] instanceof Teacher) {
			Teacher teacher = (Teacher)persons[i];
			teacher.teach();
}

```

##### 多态参数

方法定义的形参为父类，实参允许为子类类型

```java
public class PloyParameter {
	public static void main(String[] args) {
		Worker tom = new Worker("tom", 2500);
		Manager milan = new Manager("milan", 5000, 200000);
		PloyParameter ployParameter = new PloyParameter();
		ployParameter.showEmpAnnual(tom);
		ployParameter.showEmpAnnual(milan);
		ployParameter.testWork(tom);
		ployParameter.testWork(milan);
	}
//showEmpAnnual(Employee e)
//实现获取任何员工对象的年工资,并在 main 方法中调用该方法 [e.getAnnual()]
	public void showEmpAnnual(Employee e) {
		System.out.println(e.getAnnual());								//动态绑定机制. 
    }
//添加一个方法，testWork,如果是普通员工，则调用 work 方法，如果是经理，则调用 manage 方法
	public void testWork(Employee e) {
		if(e instanceof Worker) {
			((Worker) e).work();										//有向下转型操作
			} else if(e instanceof Manager) {
					((Manager) e).manage();//有向下转型操作
				} else {
						System.out.println("不做处理...");
						}
		}
}

```

# equals（效率低，可靠） 和==和hashCode（效率高，但不可靠）

equals:判断引用类型，默认判断地址是否相等，子类中往往重写该方法，用于判断类容是否相等

==:既可判断基本类型，又可判断引用类型，基本类型是判断值是否相等，引用类型判断地址是否相等（是不是同一对象）

hashCode:在object类中，hashcode()方法是本地方法，返回的是**对象的地址值**

1、哈希码并不是完全唯一的，它是一种算法，让同一个类的对象按照自己不同的特征尽量的有不同的哈希码，但不表示不同的对象哈希码完全不同。也有相同的情况，看程序员如何写哈希码的算法。

​	 1.equal()相等的两个对象他们的hashCode()肯定相等，也就是用equal()对比是绝对可靠的。
​	 2.hashCode()相等的两个对象他们的equal()不一定相等，也就是hashCode()不是绝对可靠的。

2.如果两个对象相同，那么它们的hashCode值一定要相同
　
3.如果两个对象的hashCode相同，它们并不一定相同（这里说的对象相同指的是用eqauls方法比较）。如不按要求去做了，会发现相同的对象可以出现在Set集合中，同时，增加新元素的效率会大大下降。

4.equals()相等的两个对象，hashcode()一定相等；equals()不相等的两个对象，却并不能证明他们的hashcode()不相等。
换句话说，equals()方法不相等的两个对象，hashcode()有可能相等（我的理解是由于哈希码在生成的时候产生冲突造成的）。反过来，hashcode()不等，一定能推出equals()也不等；hashcode()相等，equals()可能相等，也可能不等。

### 重写equals(ctrl+b查看源码)

```java
//重写 Object 的 equals 方法
public boolean equals(Object obj) {
//判断如果比较的两个对象是同一个对象，则直接返回 true
	if(this == obj) {
		return true;
	}
//类型判断
	if(obj instanceof Person) {//是 Person，我们才比较
//进行 向下转型, 因为我需要得到 obj 的 各个属性
		Person p = (Person)obj;
		return this.name.equals(p.name) && this.age == p.age && this.gender == p.gender;
	}
//如果不是 Person ，则直接返回 false
	return false;
}
```

# 代码块（先于构造方法执行）

### 定义

过{}包围起来。但和方法不同，没有方法名，没有返回，没有参数，只有方法体，而且不用通过对象或类显式调用，而是加载类时，或创建对象时隐式调用。

### 性质（静态和非静态）

静态代码块只能直接调用静态成员(静态属性和静态方法)，普通代码块可以调用任意成员

```
[static]{

}
无static修饰的，非静态代码块，在类创建实例时隐式调用，先于构造方法执行，创建一次调用一次（使用类的静态成员，没有创建实例，不会调用）
有static修饰的，静态代码块，作用是对类进行初始化，随着类的加载而执行，先于构造方法执行，并且只会执行一次（创建对象实例，创建子类对象实例父类也被加载，使用类的静态成员）
```

### 同一个类中执行顺序

**同一个类中执行顺序：静态代码块和静态属性初始化（按定义顺序调用）>普通代码块和普通属性初始化（按定义顺序调用）>构造方法**

```java
public class CodeBlockDetail02 {
public static void main(String[] args) {
A a = new A();// (1) A 静态代码块 01 (2) getN1 被调用...(3)A 普通代码块 01(4)getN2 被调用...(5)A() 构造器被调
用
}
}
class A {
	{ //普通代码块

		System.out.println("A 普通代码块 01");
	}
	private int n2 = getN2();//普通属性的初始化
	static { //静态代码块
		System.out.println("A 静态代码块 01");
	}
//静态属性的初始化
	private static int n1 = getN1();
	public static int getN1() {
			System.out.println("getN1 被调用...");
			return 100;
		}
	public int getN2() { //普通方法/非静态方法
		System.out.println("getN2 被调用...");
		return 200;
	}
//无参构造器
	public A() {
		System.out.println("A() 构造器被调用");
	}
}

```

### 有继承时执行顺序

**子类继承父类时，实例化对象：考虑到构造方法中 super(),即先执行super()父类构造器方法，再调用本类普通代码块，最后执行本类构造器方法**

```java
public AAA() {
//(1)super()
//(2)调用本类的普通代码块
System.out.println("AAA() 构造器被调用....");
}
class BBB extends AAA {
	{
		System.out.println("BBB 的普通代码块...");
	}
	public BBB() {
	//(1)super()  隐藏
	//(2)调用本类的普通代码块
		System.out.println("BBB() 构造器被调用....");
	}
}
```

### 总执行顺序

总：创建一个子类对象时(继承关系)，他们的静态代码块，静态属性初始化，普通代码块，普通属性初始化，构造方法的调用顺序如下:

①父类的静态代码块和静态属性(优先级一样，按定义顺序执行)

②子类的静态代码块和静态属性(优先级一样，按定义顺序执行)

③父类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)

④父类的构造方法

⑤子类的普通代码块和普通属性初始化(优先级一样，按定义顺序执行)

⑥子类的构造方法

# final关键字

### 使用场景（可以在单例模式）

1)当**不希望类被继承时**，可以用final修饰. final class A{}

2)当**不希望**父类的某个方法**被子类覆盖/重写**(override)时，可以用final关键字

3)当**不希望类的的某个属性的值被修改**，可以用final修饰. [public final double TAX RATE=0.08]

4)当**不希望某个局部变量被修改**，可以使用final修饰[案例演示final double TAX RATE=0.08 ]

### 使用细节

1) final修饰的属性又**叫常量**，一般用XX_ XX XX来命名(大写)

2) final修饰的属性在定义时必须**赋初值**，并且以后不能再修改，赋值可以在如下位置之一 [选择一个位置赋初值即可] :

​	①定义时:如public final double TAX RATE=0.08; 

​	②在构造器中

​	③在代码块中。

3)如果final修饰的属性是**静态**的，则**初始化**的位置只能是 

​	①定义时

​	②在静态代码块不能在构造器中赋值。

4) **final类不能被继承，但是可以实例化对象**。

5)如果类不是final类，但是含有final方法，则该**方法虽然不能重写，但是可以被继承。**

6)一般来说，如果一个类已经是final类了，就没有必要再将方法修饰成final方法。

7) **final不能修饰构造方法**(即构造器)

8) **final和static往往搭配使用，效率更高，不会导致类加载**.底层编译器做了优化处理。

9)包装类(Integer,Double,Float, Boolean等都是final),String也是final类.

# 抽象类	

**可以在模板模式中使用**

细节：

1)抽象类**不能被实例化**[举例]

2)抽象类不一定要包含abstract方法。 也就是说**抽象类可以没有abstract方法**

3)一旦**类包含了abstract方法，则这个类必须声明为abstract** 

4) **abstract只能修饰类和方法**，不能修饰属性和其它的。

5)**抽象类可以有任意成员**[抽象类本质还是类] ,比如:非抽象方法、构造器、 静态属性等等 [举例]

6)**抽象方法不能有主体**，即不能实现.如不能 abstract void aa{};

7) 如果个类**继承了抽象类，则它必须实现抽象类的所有抽象方法**，除非它自己也声明为abstract类。

8)抽象方法**不能使用private、final 和static来修饰**，因为这些关键字都是和重写相违背的。

# 接口(多继承)

### 形式

```java
interface 接口名{
    //属性
    [public static final] int a=0;
    //方法（抽象方法、默认实现方法、静态方法）
    [public abstract] void a();
    //jdk8之后，可以有具体实现
    default public void b(){...}
    public static void c(){...}
}

//实现案例
public class InterfaceTest {
    public static void main(String[] args) {
        extendB e = new extendB();
        System.out.println(extendB.a);//10
        System.out.println(e.a);//10
        System.out.println(interf.a)//10;
    }
}
interface interf{
    int a=10;
}
class extendB implements interf{
}


//若class B和Interface中都有属性x
class C extends B implements A {
    public void abc(){
        System.out.print(x);//错误，因为系统不知道调用哪个x
        //调用父类的x
        super.x;
        //调用接口的x
        A.x;
    }
}

```

### 细节

1)**接口不能被实例化**

2)接口中**所有的方法是public方法**，接口中抽象方法，可以不用abstract修饰

3)一个**普通类实现接口**,就必须将该接口的**所有方法都实现**。

4)**抽象类实现接口**，**可以不用实现**接口的方法。

5)**一个类同时可以实现多个接口** 

6)接口中的**属性,只能是final**的，而且是public static final修饰符。（默认）

7)**接口中属性的访问**形式:**接口名.属性名**

8)**接口不能继承其它的类**,但是**可以继承多个别的接口**

9)**接口的修饰符只能是public和默认**，这点**和类的修饰符是一样**的。

### 接口vs继承

1、接口和继承解决的问题不同
**继承的价值主要在于:解决代码的复用性和可维护性**。
**接口的价值主要在于:设计**，设计好各种规范(方法)，让其它类去实现这些方法。即更加的灵活..
2、接口比继承更加灵活
接口比继承更加灵活，继承是满足is - a的关系，而接口只需满足like - a的关系。
**接口**在一定程度上**实现代码解耦**[即:接口规范性+动态绑定机制]

# 内部类

**类的五大成员**之一【属性、方法、构造器、代码块、内部类】

基本**语法**：

class outer{//外部类

​		class inner{//内部类

​	}

}

class other{//外部其他类

}

**分类**：

如果定义类在局部位置(方法中/代码块) :

(1) 局部内部类（有类名） (2) 匿名内部类 （无类名）

定义在成员位置 

(1) 成员内部类 (无static)  (2) 静态内部类（有static）

### (1) 局部内部类

```java

class outer{//外部类

​		class inner{//内部类

​	}

}
```

说明:局部内部类是定义在外部类的局部位置，比如方法中，并且有类名。

1.可以**直接访问外部类的所有成员**，包**含私有**的

2.**不能添加访问修饰符**，因为它的地位就**是一个局部变量**。局部变量是不能使用修饰符的。 但是**可以使用final修饰**，因为局部变量也可以使用final，**final修饰后不能被继承**

3.**作用域**:仅仅在定义它的方法或代码块中。（**外部类的方法或代码块中**）

4.局部**内部类--访向---外部类的成员**[访问方式:**直接访问**

5.**外部类-访向---->局部内部类**的成员【访问方式:**创建对象，再访问**(注意:必须在作用域内)
记住:(1)局部内部类定义在方法中/代码块
(2)作用域在方法体或者代码块中
(3)本质仍然是一个类

6.**外部其他类---不能访---->局部内部类**(因为局部内部类地位是一个局部变量)

7.如果**外部类和局部内部类的成员重名**时，**默认遵循就近原则**，如果**想访问外部类的成员，则可以使用(外部类名.this.成员) 去访问**（class inner{	outer.this.n  })

### (2) 匿名内部类 (实现接口，重写或添加类的方法)

```java
//语法
new类或接口(参数列表){
类体
};
//使用
//1
new A(){
    @override
    public void cry(){
        ...
    }
}.cry();
//2
A a = new A(){
    @override
    public void cry(){
        ...
    }
};
a.cry();
```

说明:匿名内部类是定义在外部类的局部位置，比如方法中，并且没有类名

(1)本质是类(2)内部类(3)该类**没有名字（系统自动分配临时名字**）(4)同时还是一个对象

1.可以**直接访问外部类的所有成员**，**包含私有**的

2.**不能添加访问修饰符**因为它的地位就是一 个局部变量。

3.**作用域**:仅仅在定义它的方法或代码块中。**(外部类的方法或代码块中)**
4.匿名**内部类---访向---->外部类**成员[访问方式:**直接访问**]

4.**外部其他类---不能----匿名内部**类(因为匿名内部类地位是一个局部变量)

5.如果**外部类和匿名内部类**的**成员重名**时，匿名内部类访问的话，默认遵循**就近原则**，如果想访问外部类的成员，则可以使用(外部类名.this.成员) 去访问

 6.**匿名内部类使用一次，就不能再使用,但是对象实例可以一直使用**

**使用（实现接口更加灵活）**---**将接口作为形参，实现接口的的内部类作为实参传入**

```java
public class InnerClassExercise02 {
	public static void main(String[] args) {
            /*
            1.有一个铃声接口 Bell，里面有个 ring 方法。(右图)
            2.有一个手机类 Cellphone，具有闹钟功能 alarmClock，参数是 Bell 类型(右图)
            3.测试手机类的闹钟功能，通过匿名内部类(对象)作为参数，打印：懒猪起床了
            4.再传入另一个匿名内部类(对象)，打印：小伙伴上课了
            */
		CellPhone cellPhone = new CellPhone();
//老韩解读
//1. 传递的是实现了 Bell 接口的匿名内部类 InnerClassExercise02$1
//2. 重写了 ring
	 Bell bell = new Bell() {
		 @Override
 		public void ring() {
 			System.out.println("懒猪起床了");
 		}
	};
    bell.ring();
	cellPhone.alarmClock(new Bell() {
		@Override
		public void ring() {
			System.out.println("懒猪起床了");
			}
		});
	cellPhone.alarmClock(new Bell() {
		@Override
		public void ring() {
			System.out.println("小伙伴上课了");
			}
		});
	}
}
interface Bell{ //接口
	void ring();//方法
	}
class CellPhone{//类
	public void alarmClock(Bell bell){//形参是 Bell 接口类型
		System.out.println(bell.getClass());
		bell.ring();//动态绑定
	}
}
```

### (3) 成员内部类 

```java
class Outer01{//外部类
    private int n1 =10;
    public String name = "张三";
    class Inner01{//内部类
        public void say(){
            System.out.println(n1==Outer01.this.n1);
        }
    }
}
```

说明:成员内部类是定义在外部类的成员位置，并且没有static修饰。
1.可以**直接访问外部类的所有成员**，**包含私有**的

2.**可以添加任意访问修饰符(**public、 protected、默认、private),因为它的地位就是一个成员。

3.**作用域和外部类的其他成员样，为整个类体**

4.**成员内部类---访--- >外部类成员**(比如:属性) [访问方式:**直接访问**] 

5.**外部类-- ------成员内部类(**说明)访向方式:**创建对象， 再访问**
6.**外部其他类-- -访向---->成员内部类**

```java
Outer08 outer08 = new Outer08();
outer08.t1();
//外部其他类，使用成员内部类的三种方式
//老韩解读
// 第一种方式
// outer08.new Inner08(); 相当于把 new Inner08()当做是 outer08 成员
// 这就是一个语法，不要特别的纠结.Outer08.Inner08 inner08 = outer08.new Inner08();
inner08.say();
// 第二方式 在外部类中，编写一个方法，可以返回 Inner08 对象
Outer08.Inner08 inner08Instance = outer08.getInner08Instance();
class Outer08{
	class inner08{}
	public Inner08 getInner08Instance(){
		return new Inner08();
	}
}
```

7.如果外部类和内部类的**成员重名**时，内部类访问的话，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.this.成员) 去访问

### (4) 静态内部类

说明:静态内部类是定义在外部类的成员位置，并且有static修饰

1.**可以直接访问外部类的所有静态成员**，**包含私有**的，但**不能直接访问非静态**成员

2.**可以添加任意访问修饰符**(public、 protected、 默认、private),因为它的地位就是一个成员。

3.**作用域:**同其他的成员，为**整个类**体

4.**静态内部类---访问---->外部类**(比如:静态属性) [访问方式:**直接访问所有静态**成员]

5.**外部类--访-----静态内部**类访问方式:**创建对象，再访问**

6.外部其他类-- -访向----静态内部类

```java
Outer10 outer10 = new Outer10();
outer10.m1();
//外部其他类 使用静态内部类
//方式 1
//因为静态内部类，是可以通过类名直接访问(前提是满足访问权限)
Outer10.Inner10 inner10 = new Outer10.Inner10();
inner10.say();
//方式 2
//编写一个方法，可以返回静态内部类的对象实例. Outer10.Inner10 inner101 = outer10.getInner10();
inner101.say();
Outer10.Inner10 inner10_ = Outer10.getInner10_();
inner10_.say();
```

7.如果外部类和静态内部类的**成员重名**时，静态内部类访问的时，默认遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.成员) 去访问

# 枚举

### 自定义枚举类

1. 将构造器私有化,目的防止 直接 new 
2. 去掉 setXxx 方法, 防止属性被修改
3. 在 Season 内部，直接创建固定的对象
4.  优化，可以加入 final static 修饰

```java
public class Enumeration02 {
	public static void main(String[] args) {
		System.out.println(Season.AUTUMN);
		System.out.println(Season.SPRING);
	}
}
//演示字定义枚举实现
class Season {//类
	private String name;
	private String desc;//描述
	//定义了四个对象, 固定. public static final Season SPRING = new Season("春天", "温暖");
	public static final Season WINTER = new Season("冬天", "寒冷");
	public static final Season AUTUMN = new Season("秋天", "凉爽");
	public static final Season SUMMER = new Season("夏天", "炎热");
	private Season(String name, String desc) {
		this.name = name;
		this.desc = desc;
	}
	public String getName() {
		return name;
	}
	public String getDesc() {
		return desc;
	}
	@Override
	public String toString() {
		return "Season{" +
						"name='" + name + '\'' +
						", desc='" + desc + '\'' +
						'}';
		}
}
```

### 使用enum关键字实现枚举

1. 使用关键字 **enum 替代 class** 
2.  public static final Season SPRING = new Season("春天", "温暖") **直接使用 SPRING("春天", "温暖") 代替**， 解读 ：**常量名(实参列表)** 
3.  如果有**多个常量(对象)， 使用 逗号”，“间隔**即可 
4. 如果使用 enum 来实现枚举，要求将**定义常量对象，写在前面** （属性前面）
5. 如果我们使用的是**无参构造器**，创建常量对象，则**可以省略 括号**   ==》 SPRING（）=SPRING；

```java
public class Enumeration03 {
	public static void main(String[] args) {
		System.out.println(Season2.AUTUMN);
		System.out.println(Season2.SUMMER);
	}
}
//演示使用 enum 关键字来实现枚举类
enum Season2 {//类

//定义了四个对象, 固定. // public static final Season SPRING = new Season("春天", "温暖");
// public static final Season WINTER = new Season("冬天", "寒冷");
// public static final Season AUTUMN = new Season("秋天", "凉爽");
// public static final Season SUMMER = new Season("夏天", "炎热");
//如果使用了 enum 来实现枚举类

	SPRING("春天", "温暖"), WINTER("冬天", "寒冷"), AUTUMN("秋天", "凉爽"), SUMMER("夏天", "炎热");
	private String name;
	private String desc;//描述
	private Season2() {//无参构造器
	}
	private Season2(String name, String desc) {
		this.name = name;
		this.desc = desc;
	}
	public String getName() {
		return name;
	}
	public String getDesc() {
		return desc;
	}
	@Override
	public String toString() {
		return "Season{" +
				"name='" + name + '\'' +
				", desc='" + desc + '\'' +
				'}';
		}
}
```

**细节：**

1) 当我们使用 enum 关键字开发一个枚举类时，**默认会继承 Enum 类,** 而且是一个 final 类[如何证明],老师使用 javap 工 具来演示 ，这说明**enum类不能再继承别的类，但可以实现接口**

2) 传统的 public static final Season2 SPRING = new Season2("春天", "温暖"); 简化成 SPRING("春天", "温暖")， 这里**必须知道，它调用的是哪个构造器**.

 3) 如果使用无参构造器 创建 枚举对象，则实参列表和小括号都可以省略 

 4) 当有多个枚举对象时，使用,间隔，最后有一个分号结尾 

5) 枚举对象必须放在枚举类的行首.

### enum的成员方法

1) toString:Enum 类已经重写过了，返回的是当前对象 名,子类可以重写该方法，用于返回对象的属性信息

 2) name：返回当前对象名（常量名），子类中不能重写 

3) ordinal：返回当前对象的位置号，默认从 0 开始 

4) values：返回当前枚举类中所有的常量

 5) valueOf：将字符串转换成枚举对象，要求字符串必须 为已有的常量名，否则报异常！

 6) compareTo：比较两个枚举常量，比较的就是编号！

**案例**：声明 Week 枚举类，其中包含星期一至星期日的定义； MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY; 使用 values 返回所有的枚举数组,

```java
public class EnumExercise02 {
	public static void main(String[] args) {
		//获取到所有的枚举对象， 即数组
		Week[] weeks = Week.values();
		//遍历，使用增强 for
		System.out.println("===所有星期的信息如下===");
		for (Week week : weeks) {
			System.out.println(week);
		}
	}
}
/*
声明 Week 枚举类，其中包含星期一至星期日的定义；
MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
使用 values 返回所有的枚举数组, 并遍历 
*/
enum Week {
	//定义 Week 的枚举对象
	MONDAY("星期一"), TUESDAY("星期二"), WEDNESDAY("星期三"), THURSDAY("星期四"), FRIDAY("星期五"), 			SATURDAY("星期六"), SUNDAY("星期日");
	private String name;
	private Week(String name) {//构造器
		this.name = name;
	}
	@Override
	public String toString() {
		return name;
    }
}
//可以解释 enum week{MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY};
```

# 异常

### 常见异常

Exception:其它因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。例如空指针访问，试图读取不存在的文件，网络连接中断等等，Exception **分为两大类**:**运行时异常**[程序运行时，发生的异常]和**编译时异常**[编程时，编译器检查出的异常]。

1.异常分为两大类，运行时异常和编译时异常.
2.运行时异常，编译器检查不出来。一般是指编程时的逻辑错误，是程序员应该避免其出现的异常。java.lang.**RuntimeException**类及它的子类都是运行时异常

【1) NullPointerException 空指针异常 

​	2) ArithmeticException 数学运算异常 

​	3) ArrayIndexOutOfBoundsException 数组下标越界异常 	

​	4) ClassCastException 类型转换异常 

​	5) NumberFormatException 数字格式不正确异常】

3.对于运行时异常，可以不作处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响

4.编译时异常，是编译器要求必须处置的异常。

【SQLException //操作数据库时，查询表可能发生异常
	IOException //操作文件时，发生的异常
	FileNotFoundException //当操作一个不存在的文件时，发生异常
	ClassNotFoundException //加载类，而该类不存在时，异常
	EOFException //操作文件，到文件末尾，发生异常
	IlegalArguementException //参数异常】

### 异常处理

**1) try-catch-finally**    （快捷键 ctrl + alt +t)
程序员在代码中捕获发生的异常，自行处理

细节：

1) 如果异常发生了， 则异常发生后面的代码不会执行， 直接进入到catch块.
2)如果异常没有发生，则顺序执行try的代码块，不会进入到catch.
3)如果希望不管是否发生异常， 都执行某段代码(比如关闭连接，释放资源等) ，则使用finally{}

4)可以有**多个catch语句**，捕获不同的异常(进行不同的业务处理)，要求**父类异常在后，子类异常在前**，比如(Exception 在后，NullPointerException 在前)，如果发生异常，只会匹配一-个catch

5)可以进行try-finally配合使用，这种用法相当于没有捕获异常，因此程序会直接崩掉/退出。应用场景，就是执行一段代码，不管是否发生异常，都必须执行某个业务逻辑

6)如果没有出现异常，则执行try块中所有语句，不执行catch块中语句，如果有finally,最后还需要执行finally里面的语句
7)如果出现异常，则**try块中异常发生后，try块剩下的语句不再执行**。将执行catch块中的语句，如果有finally, 最后还需要执行finally里面的语句!

**2) throws**
将发生的异常抛出，交给调用者(方法)来处理，最顶级的处理者就是JVM

细节：

1)如果一个方法(中的语句执行时)可能生成某种异常，但是并不能确定如何处理这种异常，则此方法应显示地声明抛出异常，表明该方法将不对这些异常进行处理，而由**该方法的调用者负责处理**。
2)在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类。

3)对于编译异常，程序中必须处理，比如try- catch或者throws
4)对于**运行时异常**，程序中如果没有处理，**默认就是throws的方式**处理[举例]
5)**子类重写父类**的方法时，对抛出异常的规定:子类重写的方法，所**抛出的异常类**型要么和父类抛出的异常一致， 要么为父类抛出的异常的类型的子类型[举例]
6)在throws过程中，如果有方法try-catch，就相当于处理异常，就可以不必throws

### 自定义异常

当程序中出现了某些"错误”,但该错误信息并没有在Throwable子类中描述处理，这个时候可以自己设计异常类，用于描述该错误信息。
**步骤**
1)定义类:自定义异常类名(程序员自己写)继承Exception或RuntimeException
2)如果继承Exception,属于编译异常
3)如果继承RuntimeException,属于运行异常(-般来说， 继承RuntimeException)

```java
public class CustomException {
	public static void main(String[] args) /*throws AgeException*/ {
		int age = 180;
		//要求范围在 18 – 120 之间，否则抛出一个自定义异常
		if(!(age >= 18 && age <= 120)) {
		//这里我们可以通过构造器，设置信息
			throw new MyException("年龄需要在 18~120 之间");        //抛出异常
		}
		System.out.println("你的年龄范围正确.");
	}
}
//自定义一个异常
//老韩解读
//1. 一般情况下，我们自定义异常是继承 RuntimeException
//2. 即把自定义异常做成 运行时异常，好处时，我们可以使用默认的处理机制
//3. 即比较方便

class MyException extends RuntimeException {  						//自定义异常
	public MyException(String message) {//构造器
		super(message);
	}
}
```

### throws 和 throw

throws  意义：异常处理的一种方式     				位置：方法声明处             后面跟：异常类型

throw    意义：手动生成异常对象的关键字          位置：方法体中				后面跟：异常对象

# 常用类

### 包装类（以Integer 和String为例）

##### 自动拆装箱

java自动装箱和拆箱（**直接赋值是自动（超过一定区间帮你new一个），new一个对象是手动**）
基本数据类型，如int,float,double,boolean,char,byte,不具备对象的特征，不能调用方法。
**装箱**：将基本类型转换成包装类对象
int i=10;
Integer x=new Integer(i);手动装箱 

Integer integer1 = Integer.valueOf(i）；手动装箱（事实上是使用了 new Integer())

Integer y=10;自动装箱
**拆箱**：将包装类对象转换成基本类型的值
Integer j=new Integer(8);
int m=j.intValue();//手动拆箱
int n=j;//自动拆箱

##### Integer

```java
public class Main {
public static void main(String[] args) {				1111111111111111111111111111111111111
Integer i1 = 100;										1	栈   1                        	1
Integer i2 = 100;										1	     1         堆                1
Integer i3 = 200;                                       1	     1                          1
Integer i4 = 200;                                       1	     1                          1
System.out.println(i1==i2);//true                       1	     1 111111111111111111111111 1           
System.out.println(i3==i4);//false                      1main()栈1    常量池       方法区      1
}														1	     1                类加载区    1
}														1111111111111111111111111111111111111
```

**Integer赋值在-128<= x<=127时候，直接从常量池中获取对象地址，超过这个范围在堆中自动new一个对象**(可以看源码)

Integer与Integer比较的时候，由于直接赋值的时候会进行自动的装箱，那么这里就需要注意两个问题，一个是-128<= x<=127的整数，将会直接缓存在IntegerCache中，那么当赋值在这个区间的时候，不会创建新的Integer对象，而是从缓存中获取已经创建好的Integer对象。二：当大于这个范围的时候，直接new Integer来创建Integer对象

```java
public class Main {
public static void main(String[] args) {
Double i1 = 100.0;
Double i2 = 100.0;
Double i3 = 200.0;
Double i4 = 200.0;
System.out.println(i1==i2);//false
System.out.println(i3==i4);//false
}
}
```

为什么Double类的valueOf方法会采用与Integer类的valueOf方法不同的实现呢？很简单：**在某个范围内的整型数值的个数是有限的，而浮点数却不是**

**包装类与String之间的转换**

> 1、基本数据类型转换成字符串									int a=100;
> 使用包装类的toString()方法； 								String m=String.valueOf(a);*//方法一* 
> 使用String类的valueOf()方法；								String n=Integer.tostring(a);*//方法二* 
> 使用一个空字符串加上基本类型。							String p=a+" ";*//方法三*

> 2、字符串转换成基本数据类型																	String a="8";
> 调用包装类的parseXXX()方法；																	int b=Integer.parseInt(a);//方法一
> 调用包装类的valueOf()方法转换为基本数据类型的包装类。					int c=Integer.valueOf(a);//方法二
>
> 使用构造器																										int d = new Integer(a);//方法三

##### String

1) String对象用于保存字符串，也就是一组字符序列
2)字符串常量对象是用双引号括起的字符序列。例如: "你好"、"12.97"、"boy"等 
3)字符串的字符使用**Unicode字符编码**，一个字符(不区分字母还是汉字)**占两个字节**。
4) String类较**常用构造器**(其它看手册):
String s1 = new String(); 
String s2 = new String(String original);
String s3 = new String(char[] a);
String s4 = new String(char[] a,int startIndex,int count)

/5. String 类实现了接口 Serializable【String 可以串行化:可以在网络传输】 // 接口 Comparable [String 对象可以比较大小] 

6. String **是 final 类，不能被其他的类继承**

7. String 有属性 private final char value[]; 用于存放字符串内容 

8. 一定要注意：**value 是一个 final 类型， 不可以修改**(需要功力)：即 value 不能指向 新的地址，但是单个字符内容是可以变化

    ​	String name = "jack"; name = "tom";   可以

    ​	final char[] value = {'a','b','c'}; char[] v2 = {'t','o','m'}; value[0] = 'H';  可以

    ​	 value = v2;  不行     不可以修改 value 地址

 **创建对象**

方式一:直接赋值String S = "hsp";
方式二: 调用构造器String s2 = new String("hsp");
1.方式:先从常量池查看是否有"hsp"数据空间，如果有，直接指向;如果没有则重新创建，然后指向。s最终指向的是常量池的空间地址
2.方式二:先在堆中创建空间，里面维护了value属性， 指向常量池的hsp空间。如果常量池没有"hsp",重新创建，如果有，直接通过value指向。最终指向的是堆中的空间地址。

**面试题**

**两种字符串对象的地址**

```java
String a = "hsp"; //a指向常量池的"hsp"
String b =new String("hsp");//b指向堆中对象
System.out.println(a.equals(b)); //T
System.out.println(a==b); //F
System.out.println(a== b.intern(); //T //intern方法自己先查看API
|System.out.println(b= =b.intern(); //F
'知识点:
|当调用intern方法时，如果池已经包含个等于此String对象的字符串(用equal(obieet)方法确定) ,则返回池中的字符串。否则，将此String对象添加到池中，并返回此String对象的引用
老韩解读; (1) b.intern() 方法最终返回的是常量池的地址(对象) .
```

**字符串拼接时的地址变化**：重要规则， Stringc1 = "ab" + "cd"; 常量相加，看的是池。Stringc1 = a + b;变量相加,是在堆中

```
String a = "hello"; //创建a对象
String b = "abc";//创建 b对象
String c=a+ b;创建了几个对象?画出内存图?
//关键就是要分析Stringc= a + b;到底是如何执行的
//-共有3对象，
老韩小结: 底层是StringBuilder sb = new StringBuilder(); sb.append(a);
sb.append(b); sb是在堆中，并且append是在原来字符串的基础 上追加的.
重要规则， Stringc1 = "ab" + "cd"; 常量相加，看的是池。Stringc1 = a + b;变量相加,是在堆中
学习思路:一定尽量看源码学习。
```

**常见方法**：

equals //区分大小写，判断内容是否相等
equalslgnoreCase //忽略大小写的判断内容是否相等
length /获取字符的个数，字符串的长度
indexOf //获取字符在字符串中第1次出现的索引,索引从开始如果找不到,返回-1
lastIndexOf //获取字符在字符串中最后1次出现的索引,索引从0开始，如找不到，返回-1
substring //截取指定范围的子串
trim //去前后空格
charAt:获取某索引处的字符，注意不能使用Str[index]这种方式

toUpperCase
toLowerCase
concat
replace替换字符串中的字符
split分割字符串，对于某些分割字符，我们需要转义比如| |\等
compareTo //比较两个字符串的大小
toCharArray //转换成字符数组
format //格式字符串，%s字符串%c字符%d整型%.2f浮点型

##### StringBuffer

java.lang.StringBuffer代表可变的字符序列，可以对字符串内容进行增删。很多方法与String相同，但StringBuffer是可变长度StringBuffer是一个容器。

/1. StringBuffer 的直接父类 是 AbstractStringBuilder 

//2. StringBuffer 实现了 Serializable, 即 StringBuffer 的**对象可以串行化** 

//3. 在父类中 AbstractStringBuilder 有**属性 char[] value,不是 final** // 该 value 数组存放 字符串内容，引出存放在堆中的

 //4. StringBuffer 是**一个 final 类，不能被继承**

**String 和 StringBuffer 区别**

1) String保存的是字符串常量，里面的值不能更改，每次String类的更新实际上就是更改地址，效率较低//private final char value[];
2) StringBuffer保存的是字符串变量，字符内容是存在 char[] value,里面的值可以更改，每次StringBuffer的更新实际上可以更新内容，不用每次更新地址，效率较高
//char[] value;//这个放在堆.

**String 和StringBuffer的转换**

```java
//看 String——>StringBuffer
String str = "hello tom";
//方式 1 使用构造器
//注意： 返回的才是 StringBuffer 对象，对 str 本身没有影响
StringBuffer stringBuffer = new StringBuffer(str);

//方式 2 使用的是 append 方法
StringBuffer stringBuffer1 = new StringBuffer();
stringBuffer1 = stringBuffer1.append(str);



//看看 StringBuffer ->String
StringBuffer stringBuffer3 = new StringBuffer("韩顺平教育");
//方式 1 使用 StringBuffer 提供的 toString 方法
String s = stringBuffer3.toString();

//方式 2: 使用构造器来搞定
String s1 = new String(stringBuffer3)
```

**常用方法**

StringBuffer s = new StringBuffer("hello"); 

//增  s.append(String s)    **若s = null;则会自动转为 s = "null";**

s.append(',');// "hello,"

 s.append("张三丰");//"hello,张三丰" 

s.append("赵敏").append(100).append(true).append(10.5);//"hello,张三丰赵敏 100true10.5"

 System.out.println(s);//"hello,张三丰赵敏 100true10.5"



//删 s.delete(start ，end)

/*
*删除索引为>= =start && <end处的字符
*解读:删除11~14 的字符[11, 14)
*/
s.delete(11, 14);
System.out.println(s);//"hello,张三丰赵敏true10.5" 



//改 s.replace(start ，end,String)
//老韩解读，使用周芷若替换索引9-11的字符[9,11)
s.replace(9, 11, "周芷若"); 
System.out.println(s//"hello,张三丰周芷若true10.5"



//查	 s.indexOf(String s);

//找指定的子串在字符串第- -次出现的索引，如果找不到返回-1
int indexOf = s.indexOf("张三丰");
System.out.println(indexOf;//6



//插  s.insert(9, "赵敏");

//老韩解读，在索引为9的位置插入"赵敏",原来索引为9的内容自动后移
s.insert(9, "赵敏");
System.out.println(s//"hello,张三丰赵敏周芷若true10.5"



//长度  s.length()
System.out.println(s.length());//2
System.out.println(s);



##### StringBuilder

1)一个可变的字符序列。此类提供一 个与StringBuffer兼容的API,但**不保证同步(StringBuilder不是线程安全**)。该类被设计用作StringBuffer的一一个简易替换，用在字符串缓冲区被**单个线程使用**的时候。如果可能，建议**优先采用**该类!因为在大多数实现中，它**比StringBuffer要快**。
2)在StringBuilder上的主要操作是append和insert方法，可重载这些方法，以接受任意类型的数据。

**StringBuilder和StringBuffer均代表可变的字符序列，方法是一样的，所以使用和StringBuffer-样**



##### String 、 StringBuffer 和 StringBuilder

**区别**

1) StringBuilder和StringBuffer非常类似，均代表可变的字符序列，而且方法也一样
2) String:不可变字符序列，效率低，但是复用率高。
3) StringBuffer:可变字符序列、效率较高(增删)、线程安全，看源码
4) StringBuilder:可变字符序列、效率最高、线程不安全
5) String使用注意说明:
string s="a"; //创建了-一个字符串
s += "b"; //实际上原来的" a"字符串对象已经丢弃了，现在又产生了一一个字符
串s+"b" (也就是"ab")。如果多次执行这些改变串内容的操作，会导致大量副
本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大
影响程序的性能=>**结论:如果我们对String做大量修改，不要使用String**

**使用场景**

使用的原则，结论:
1.如果字符串存在大量的修改操作，- 般使用StringBuffer或StringBuilder
2.如果字符串存在大量的修改操作，并在单线程的情况，使用StringBuilder
3.如果字符串存在大量的修改操作，并在多线程的情况，使用StringBuffer
4.如果我们字符串很少修改，被多个对象引用，使用String, 比如配置信息等
StringBuilder的方法使用和StringBuffer-一样，不再说.

### Math

Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。(**静态**)

1.abs 绝对值 	

​	int abs = Math.abs(-9); System.out.println(abs); //9

2.pow 求幂 	

​	double pow = Math.pow(2, 4);//2 的 4 次方 System.out.println(pow);//16 

3.ceil 向上取整,返回>=该参数的最小整数(转成 double); 

​	double ceil = Math.ceil(3.9); System.out.println(ceil);//4.0 

4.floor 向下取整，返回<=该参数的最大整数(转成 double) 

​	double floor = Math.floor(4.001); System.out.println(floor);//4.0 

5.round 四舍五入 

​	Math.floor(该参数+0.5) long round = Math.round(5.51); System.out.println(round);//6 

6.sqrt 求开方 

​	double sqrt = Math.sqrt(9.0); System.out.println(sqrt);//3.0

7.random 求随机数 // random 返回的是 0 <= x < 1 之间的一个随机小数 //

​	思考：请写出获取 a-b 之间的一个随机整数,a,b 均为整数 ，比如 a = 2, b=7 // 即返回一个数 x 2 <= x <= 7 

​	(int)(a + Math.random() * (b-a +1) ) 

8.max , min 返回最大值和最小值 

​	int min = Math.min(1, 9); int max = Math.max(45, 90); System.out.println("min=" + min); System.out.println("max=" + max); 

### Arrays

Arrays里面包含了一系列静态方法，用于管理或操作数组(比如排序和搜索)。

##### 常用方法(查看api)

1) toString返回数组的字符串形式
	**Arrays.toString(arr)**
2) sort排序(自然排序和定制排序) Integer arr[]= {1,-1, 7, 0, 89};

3) binarySearch通过二分搜索法进行查找，要求必须排好序
	int index = Arrays.binarySearch(arr, 3);    //如果数组中不存在该元素，就返回 return -(low + 1); // key not found
4) copyOf数组元素的复制
	Integer[] newArr = Arrays.copyOf(arr, arr.length);
5) fill数组元素的填充
	Integer[] num = new Integer[]{9,3,2};
	Arrays,fill(num, 99);
6) equals 比较两个数组元素内容是否完全 -致
	boolean equals = Arrays.equals(arr, arr2);
7) asList将一组值，转换成list
	List< Integer> asList = Arrays.asList(2,3,4,5,6,1);
	System.out.println( asList=" + asList); 

##### 定制排序

```java
Integer []arr = new Integer[]{1,5,6,2,4,9,8,2,4};
        Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2-o1;
            }
        });
        System.out.println(Arrays.toString(arr));//逆序
    }
```

按第一维元素比较二维数组

```java
 int[][] nums=new int[][]{{1,3},{1,2},{4,5},{3,7}};
        //方法一
        Arrays.sort(nums,new Comparator<int[]>(){
            @Override
            public int compare(int[] a,int[] b){
                if(a[0]==b[0]){
                    return a[1]-b[1];
                }else{
                    return a[0]-b[0];
                }
            }
        });
```

### BigInteger 和 BigDecimal 类

**应用场景**:
1) BigInteger适合保存比较大的整型
2) BigDecimal适合保存精度更高的浮点型(小数)



 BigInteger和BigDecimal**常见方法**
1) add加
2) subtract减
3) multiply乘 
4) divide除   bigDecimal.divide(bigDecimal2, BigDecimal.ROUND_CEILING)   BigDecimal.ROUND_CEILING//如果有无限循环小数，就会保留 分子 的精度

```java
BigDecimal bigDecimal = new BigDecimal("1999.11");
BigDecimal bigDecimal2 = new BigDecimal("3");
System.out.println(bigDecimal);
//老韩解读
//1. 如果对 BigDecimal 进行运算，比如加减乘除，需要使用对应的方法
//2. 创建一个需要操作的 BigDecimal 然后调用相应的方法即可
System.out.println(bigDecimal.add(bigDecimal2));
System.out.println(bigDecimal.subtract(bigDecimal2));
System.out.println(bigDecimal.multiply(bigDecimal2));
//System.out.println(bigDecimal.divide(bigDecimal2));//可能抛出异常 ArithmeticException
//在调用 divide 方法时，指定精度即可. BigDecimal.ROUND_CEILING
//如果有无限循环小数，就会保留 分子 的精度
System.out.println(bigDecimal.divide(bigDecimal2, BigDecimal.ROUND_CEILING));
```

### 日期类

##### Date

Date d1 = new Date(); //**获取当前系统时间** 

System.out.println("当前日期=" + d1);



 Date d2 = new Date(9234567); //通过**指定毫秒数得到时间** 

System.out.println("d2=" + d2); //获取某个时间对应的毫秒数



SimpleDateFormat sdf = new SimpleDateFormat("yyyy 年 MM 月 dd 日 hh:mm:ss E"); 

String format = sdf.format(d1); // format:**将日期转换成指定格式的字符串** 

System.out.println("当前日期=" + format);



 //1. 可以把**一个格式化的 String 转成对应的 Date** 

//2. 得到 Date 仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转换

 //3. 在把 String -> Date ， 使用的 sdf 格式需要和你给的 String 的格式一样，否则会抛出转换异常 

String s = "1996 年 01 月 01 日 10:20:30 星期一"; 

Date parse = sdf.parse(s); 

System.out.println("parse=" + sdf.format(parse));



##### Calendar（日历）

   //1. Calendar 是一个**抽象类， 并且构造器是 private**
//2. 可以通过 **getInstance() 来获取实例**
//3. 提供大量的方法和字段提供给程序员

//4. Calendar 没有提供对应的格式化的类，因此需要程序员自己组合来输出(灵活)
//5. 如果我们需要按照 24 小时进制来获取时间， Calendar.HOUR ==改成=> Calendar.HOUR_OF_DAY

```
        Calendar c = Calendar.getInstance(); //创建日历类对象//比较简单，自由
        System.out.println("c=" + c);
```

//2.获取日历对象的某个日历字段
        System.out.println("**年：" + c.get(Calendar.YEAR)**);
// 这里为什么要 + 1, 因为 Calendar 返回月时候，是按照 0 开始编号
        System.out.println(**"月：" + (c.get(Calendar.MONTH) + 1))**;
        System.out.println(**"日：" + c.get(Calendar.DAY_OF_MONTH**));
        System.out.println("**小时：" + c.get(Calendar.HOUR)**);
        System.out.println("**分钟：" + c.get(Calendar.MINUTE**));
        System.out.println("**秒：" + c.get(Calendar.SECOND)**);
//Calender **没有专门的格式化**方法，所以需要程序员自己来组合显示
        System.out.println(c.get(Calendar.YEAR) + "-" + (c.get(Calendar.MONTH) + 1) + "-" +
                c.get(Calendar.DAY_OF_MONTH) +
                " " + c.get(Calendar.HOUR_OF_DAY) + ":" + c.get(Calendar.MINUTE) + ":" + c.get(Calendar.SECOND) );

上述输出：

c=java.util.GregorianCalendar[time=1642426204248,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2022,MONTH=0,WEEK_OF_YEAR=4,WEEK_OF_MONTH=4,DAY_OF_MONTH=17,DAY_OF_YEAR=17,DAY_OF_WEEK=2,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=9,HOUR_OF_DAY=21,MINUTE=30,SECOND=4,MILLISECOND=248,ZONE_OFFSET=28800000,DST_OFFSET=0]
年：2022
月：1
日：17
小时：9
分钟：30
秒：4
2022-1-17 21:30:4



##### LocalDateTime(最新版日期表示)

**前面两代日期类的不足分析**
JDK 1.0中包含了一个java.util.Date类， 但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了。而Calendar也存在问题是:
1)可变性:像日期和时间这样的类应该是不可变的。
2)偏移性: Date中的年份是从1900开始的，而月份都从0开始。
3)格式化:格式化只对Date有用，Calendar则不行。
4)此外，它们也不是线程安全的;不能处理闰秒等(每隔2天，多出1s)

**1) LocalDate(日期/年月日)、 LocalTime(时间/时分秒)、 LocalDate Time(日期时间/年月日时分秒)** JDK8加入
LocalDate只包含日期，可以获取日期字段
LocalTime只包含时间， 可以获取时间字段
LocalDateTime包含日期+时间，可以获取日期和时间字段

​       //第三代日期
//老韩解读
//1. **使用 now() 返回表示当前日期时间的 对象**
​        LocalDateTime ldt = LocalDateTime.now(); //LocalDate.now();//LocalTime.now()
​        System.out.println(ldt);

//2. **使用 DateTimeFormatter 对象来进行格式化**
// 创建 DateTimeFormatter 对象
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String format = dateTimeFormatter.format(ldt);       

​		System.out.println("格式化的日期=" + format);

​        System.out.println("**年=" + ldt.getYear()**);
​        System.out.println("**月=" + ldt.getMonth())**;
​        System.out.println("**月=" + ldt.getMonthValue())**;
​        System.out.println("**日=" + ldt.getDayOfMonth()**);
​        System.out.println("**时=" + ldt.getHour(**));
​        System.out.println("**分=" + ldt.getMinute(**));
​        System.out.println("**秒=" + ldt.getSecond(**));

​        LocalDate now = LocalDate.now(); //**可以获取年月日**

​        LocalTime now2 = LocalTime.now();//**获取到时分秒**
​        System.out.println(now+"-----"+now2);



​	//**提供 plus 和 minus 方法可以对当前时间进行加或者减**
​	//看看 890 天后，是什么时候 把 年月日-时分秒
​        LocalDateTime localDateTime = ldt.plusDays(890);
​        System.out.println("890 天后=" + dateTimeFormatter.format(localDateTime));
​	//看看在 3456 分钟前是什么时候，把 年月日-时分秒输出
​        LocalDateTime localDateTime2 = ldt.minusMinutes(3456);
​        System.out.println("3456 分钟前 日期=" + dateTimeFormatter.format(localDateTime2));

上述输出

2022-01-17T21:41:08.174
格式化的日期=2022-01-17 21:41:08
年=2022
月=JANUARY
月=1
日=17
时=21
分=41
秒=8
2022-01-17-----21:41:08.185
890 天后=2024-06-25 21:41:08
3456 分钟前 日期=2022-01-15 12:05:08



##### **时间戳**Instant

类似于Date,提供了一-系列和Date类转换的方式
Instant-- > Date:
Date date = Date.from(instant);
Date- > Instant:
Instant instant = date.tolnstant();

//1.通过 静态方法 now() 获取表示当前时间戳的对象 

​	Instant now = Instant.now(); 

​	System.out.println(now);   //2022-01-17T13:50:52.586Z

//2. 通过 from 可以把 Instant 转成 Date

​	Date date = Date.from(now);  //Mon Jan 17 21:50:52 CST 2022

//3. 通过 date 的 toInstant() 可以把 date 转成 Instant 对象 

​	Instant instant = date.toInstant()

# 集合

### 集合遍历三种方法

##### 普通for循环

```java
Collection col = new ArrayList();
for(int i = 0;i<col.size();i++){
    System.out.print(col.get(i));
}
```

##### 增强for循环

基本语法
for(元素类型元素名:集合名或数组名) {
	访问元素

}

```java
Collection col = new ArrayList();
for(Object obj:col){
    System.out.print(obj);
}
```

##### 使用迭代器(快捷输出 itit)

1) Iterator对象称为迭代器，主要用于遍历Collection集合中的元素。
2)所有实现了Collection接口的集合类都有一个iterator(方法， 用以返回
一个实现了Iterator接口的对象，即可以返回一一个迭代器。
3) Iterator的结构.[看一 -张图]
4) Iterator仅用于遍历集合，Iterator本身并不存放对象。

```java
Collection col = new ArrayList();
Iterator iterator = coll.iterator(); //得到个集合的迭代器
//hasNext():判断是否还有下一个元素
while(iterator.hasNext()){
//next(作用:1.下移2.将下移以后集合位置上的元素返回
	System. out.println(iterator.next());
}
```

### List

List 接口是Collection接口的子接口
1) List集合类中**元素有序**(即添加顺序和取出顺序一致)、 且**可重复**
2) List集合中的每个元素都有其对应的**顺序索引**， 即支持索引。
3) List容器中的元素都对应一个**整数型的序号记载其在容器中的位置**，可以根据序号存取容器中的元素。

**常用方法**

public static void main(String[] args) {
List list = new ArrayList();
list.add("张三丰");
list.add("贾宝玉");
**// void add(int index, Object ele):在 index 位置插入 ele 元素**
//在 index = 1 的位置插入一个对象
list.add(1, "韩顺平");
System.out.println("list=" + list);
**// boolean addAll(int index, Collection eles):从 index 位置开始将 eles 中的所有元素添加进来**
List list2 = new ArrayList();
list2.add("jack");
list2.add("tom");
list.addAll(1, list2);
System.out.println("list=" + list);
**// Object get(int index):获取指定 index 位置的元素**
//说过
**// int indexOf(Object obj):返回 obj 在集合中首次出现的位置**
System.out.println(list.indexOf("tom"));//2
**// int lastIndexOf(Object obj):返回 obj 在当前集合中末次出现的位置**
list.add("韩顺平");
System.out.println("list=" + list);
System.out.println(list.lastIndexOf("韩顺平"));
**// Object remove(int index):移除指定 index 位置的元素，并返回此元素**
list.remove(0);
System.out.println("list=" + list);
**// Object set(int index, Object ele):设置指定 index 位置的元素为 ele , 相当于是替换. list.set(1, "玛丽");**
System.out.println("list=" + list);
**// List subList(int fromIndex, int toIndex):返回从 fromIndex 到 toIndex 位置的子集合**
// 注意返回的子集合 fromIndex <= subList < toIndex
List returnlist = list.subList(0, 2);
System.out.println("returnlist=" + returnlist);
}



##### ArrayList（改查效率高）

```
//使用无参构造器创建 ArrayList 对象 

ArrayList list = new ArrayList(); 

//使用有参构造器创建 ArrayList 对象 

ArrayList list = new ArrayList(8)
```



1) permits all elements, including null，**ArrayList可以加入null,并且多个**
2) ArrayList是由**数组来实现数据存储**的
3) ArrayList**基本等同于Vector**，除了ArrayList是**线程不安全**(**执行效率高**)看源码.在多线程情况下，不建议使用ArrayList

**扩容机制**：

1) ArrayList中维护了一个Object类型的数组elementData. transient Object[] elementData; //transient表示瞬间，短暂的，表示该属性不会被序列号
2)当创建ArrayList对象时， 如果使用的是无参构造器，则初始elementData容量为0,第1次添加，则扩容elementData为10,如需要再次扩容，则扩容elementData为1.5倍。
3)如果使用的是指定大小的构造器，则初始elementData容量为指定大小，如果需要扩容，则直接扩容elementData为1.5倍。



##### Vector（线程安全）

```
//无参构造器

Vector vector = new Vector();

 //有参数的构造 

Vector vector = new Vector(8);


```

1) Vector类的定义说明
public class Vector<E>extends Abstractlist<E>implements List<E>, RandomAccess, Cloneable, Serializable
2) Vector底层也是一个**对象数组**，protected Object[] elementData;
3) Vector是**线程同步的，即线程安全**，Vector类的操作方法带有synchronized
public synchronized E get(int index) {
	if (index >= elementCount)
		throw new ArrayIndexOutOfBoundsException(index);
	return elementData(index);

}

4)在开发中，需要线**程同步安全时，考虑使用Vector**



**扩容机制：**

如果是无参，默认10，满后，就按2倍扩容
如果指定大小，则每次直接按2倍扩容.



##### LinkedList（增删效率高）

```
LinkedList linkedList = new LinkedList()
```

1) LinkedList底层实现了双向链表和双端队列特点
2)可以**添加任意元素(元素可以重复)，包括null**
3)**线程不安全**，没有实现同步



LinkedList 的**底层操作机制**
1) LinkedList**底层维护了一个双向链表.**
2) LinkedList中维护了两个属性first和last分别指向首节点和尾节点
3)每个节点(Node对象)，里面又维护了prev、next、 item三个属性， 其中通过prev指向前一个，通过next指向后个节点。最终实现双向链表
4)所以LinkedList的元素的**添加和删除，不是通过数组完成的，相对来说效率较高**。

**//演示一个删除结点的 linkedList.remove(); // 这里默认删除的是第一个结点**



**如何选择ArrayList和LinkedList:**
1)如果我们改查的操作多，选择ArrayList
2)如果我们增删的操作多，选择LinkedList
3)一般来说，在程序中，80%-90%都是查询，因此大部分情况下会选择ArrayList
4)在一个项目中，根据业务灵活选择，也可能这样，一个模块使用的是ArrayList,另外一个模块是LinkedList,也就是说，要根据业务来进行选择



### Set

1)**无序(添加和取出的顺序不一致**) ,**没有索引**

2)**不允许重复**元素，所以**最多包含一个null**

3)和 List 接口一样, Set 接口也是 Collection 的子接口，因此，**常用方法和 Collection 接口一样**

4)同Collection的遍历方式一样，因为Set接口是Collection接口的子接口。
		1.可以使用迭代器
		2.增强for
		3.**不能使用索引**的方式来获取.

//1. 以 Set 接口的实现类 HashSet 来讲解 Set 接口的方法 

//2. set 接口的实现类的对象(Set 接口对象), 不能存放重复的元素, 可以添加一个 null 

//3. set 接口对象存放数据是无序(即添加的顺序和取出的顺序不一致) 

//4. 注意：取出的顺序的顺序虽然不是添加的顺序，但是他的固定



##### HashSet(无序，无重)

1) HashSet实现了Set接口
2) HashSet实际上是HashMap,HashMap底层是(**数组+链表+红黑树**)
3)可以存放null值，但是只能有一个null
4) HashSet不保证元素是有序的,取决于hash后，再确定索引的结果. (即，不保证存放元素的顺序和取出顺序一致)
5)**不能有重复元素/对象**.在前面Set接口使用已经讲过

HashSet添加元素底层实现：

1. HashSet 底层是HashMap
2. 添加一个元素时，先得到hash值 -会转成->索引值
3. 找到存储数据表table，看这个索引位置是否已经存放的有元素
4. 如果没有，直接加入
5. 如果有，调用equals比较，如果相同，就放弃添加，如果不相同，则添加到最后
6. 在Java8中， 如果一条链表的元素个数到达TREEIFY THRESHOLD(默认是8)，并且table的大小>=MIN TREEIFY CAPACITY(默认64),就会进行树化(红黑树)

分析HashSet的扩容和转成红黑树机制：

1. HashSet底层是HashMap,第一次添加时，table 数组扩容到16,临界值(threshold)是1 6*加载因子(loadFactor)是0.75 = 12*

2. *如果table数组使用到了临界值12,就会扩容到16* 2 = 32,新的临界值就是32*0.75 = 24,依次类推

3. 在Java8中，如果条链表的元素个数到达TREEIFY THRESHOLD(默认是8),并且table的大小>=MIN TREEIFY CAPACITY(默认64),就会进行树化(红黑树)，否则仍然采用数组扩容机制

  

##### LinkedHashSet（有序，无重）

1) LinkedHashSet是HashSet的子类
2) LinkedHashSet底层是一个LinkedHashMap,底层维护了一个**数组+双向链表**
3) LinkedHashSet根据元素的hashCode值来决定元素的存储位置，同时使用链表维护元素的次序(图)，这使得元素**看起来是以插入顺序**保存的。
4) LinkedHashSet**不允许添重复**元素

底层逻辑：

1)在LinkedHastSet 中维护了一个hash表和双向链( LinkedHashSet有head和tail )
2)每一个节点有before和after属性，这样可以形成双向链表
3)在添加一个元素时，先求hash值，在求索引..确定该元素在table的位置，然后将添加的元素加入到双向链表(如果已经存在，不添加[原则和hashset- -样])
tail.next = newElement //示意代码
newElement.pre = tail
tail = newEelment;
4)这样的话，我们遍历LinkedHashSet也能确保插入顺序和遍历顺序-致



##### TreeSet(自定义有序)

```java
//老韩解读
//1. 当我们使用无参构造器，创建 TreeSet 时，仍然是无序的
//2. 老师希望添加的元素，按照字符串大小来排序
//3. 使用 TreeSet 提供的一个构造器，可以传入一个比较器(匿名内部类)
// 并指定排序规则
//4. 简单看看源码
//老韩解读
/*
1. 构造器把传入的比较器对象，赋给了 TreeSet 的底层的 TreeMap 的属性 this.comparator
public TreeMap(Comparator<? super K> comparator) {
this.comparator = comparator;
}
2. 在 调用 treeSet.add("tom"), 在底层会执行到
if (cpr != null) {//cpr 就是我们的匿名内部类(对象)
韩顺平循序渐进学 Java 零基础
第 688页
do {
parent = t;
//动态绑定到我们的匿名内部类(对象)compare
cmp = cpr.compare(key, t.key);
if (cmp < 0)
t = t.left;
else if (cmp > 0)
t = t.right;
else //如果相等，即返回 0,这个 Key 就没有加入
return t.setValue(value);
} while (t != null);
}
*/

// TreeSet treeSet = new TreeSet();
TreeSet treeSet = new TreeSet(new Comparator() {
@Override
public int compare(Object o1, Object o2) {
//下面 调用 String 的 compareTo 方法进行字符串大小比较
//如果老韩要求加入的元素，按照长度大小排序
//return ((String) o2).compareTo((String) o1);
return ((String) o1).length() - ((String) o2).length();
}
});
//添加数据. treeSet.add("jack");

treeSet.add("tom");//3
treeSet.add("sp");
treeSet.add("a");
treeSet.add("abc");//3
System.out.println("treeSet=" + treeSet);
```

##### 试分析HashSet和TreeSet分别如何实现去重的

(1) HashSet的去重机制: hashCode() + equals() ,底层先通过存入对象，进行运算得到一个hash值，通过hash值得到对应的索引，如果发现table索引所在的位置，没有数据，就直接存放如果有数据，就进行equals比较[遍历比较]，如果比较后，不相同,就加入，否则就不加入.
(2) TreeSet的去重机制:如果你传入了一个Comparator匿名对象， 就使用实现的compare去重，如果方法返回0,就认为是相同的元素/数据，就不添加，如果你没有传入-个Comparator匿名对象，则以你添加的对象实现的Compareable接口的compareTo去重

### Map

1) **Map与Collection并列存在**。用于保存具有映射关系的数据:Key-Value
2) Map中的**key和value 可以是任何引用类型**的数据，会封装到HashMap$Node对象中（**key 在set，value在collection**)
3) Map中的**key不允许重复**，原因和HashSet一样，前面分析过源码.
4) Map中的**value可以重复**
5) Map的key可以为null, value也可以为null，注意key为null,只能有一个，value为null ,可以多个.
6)**常用String类作为Map的key**
7) **key和value**之间存在**单向一对一关系**，即通过指定的key总能找到对应的value

8) Map存放数据的key-value示意图，一对k-v是放在一个HashMap$Node中的， 有因为Node实现了Entry 接口，有些书上也说- -对k-v是一个Entry



**常用方法：**

public class MapMethod {
public static void main(String[] args) {
//演示 map 接口常用方法
Map map = new HashMap();

**//put：增加元素**

map.put("邓超", new Book("", 100));//OK
map.put("邓超", "孙俪");**//替换**-> 一会分析源码
map.put("王宝强", "马蓉");//OK
map.put("宋喆", "马蓉");//OK
map.put("刘令博", null);//OK
map.put(null, "刘亦菲");//OK
map.put("鹿晗", "关晓彤");//OK
map.put("hsp", "hsp 的老婆");
System.out.println("map=" + map);
**// remove:根据键删除映射关系**
map.remove(null);
System.out.println("map=" + map);
**// get：根据键获取值**
Object val = map.get("鹿晗");
System.out.println("val=" + val);
**// size:获取元素个数**
System.out.println("k-v=" + map.size());
**// isEmpty:判断个数是否为 0**
System.out.println(map.isEmpty());//F
**// clear:清除 k-v**
//map.clear();
System.out.println("map=" + map);
**// containsKey:查找键是否存在**
System.out.println("结果=" + map.containsKey("hsp"));//T
}
}
class Book {
private String name;
private int num;
public Book(String name, int num) {
this.name = name;
this.num = num;
}
}

//第一组: 先**取出 所有的 Key** , 通过 Key 取出对应的 Value
Set keyset = map.keySet();

//第二组: 把**所有的 values 取出**
Collection values = map.values();

//第三组: **通过 EntrySet 来获取 k-v**
Set entrySet = map.entrySet();// EntrySet<Map.Entry<K,V>>

**Map遍历**(三种)

1) containsKey:查找键是否存在
2) keySet:获取所有的键
3) entrySet:获取所有关系k-v
4) values:获取所有的值

```java
//第一组: 先取出 所有的 Key , 通过 Key 取出对应的 Value
Set keyset = map.keySet();
//(1) 增强 for
System.out.println("-----第一种方式-------");
for (Object key : keyset) {
System.out.println(key + "-" + map.get(key));
}
//(2) 迭代器
System.out.println("----第二种方式--------");
Iterator iterator = keyset.iterator();
while (iterator.hasNext()) {
Object key = iterator.next();
System.out.println(key + "-" + map.get(key));
}


//第二组: 把所有的 values 取出
Collection values = map.values();
//这里可以使用所有的 Collections 使用的遍历方法
//(1) 增强 for
System.out.println("---取出所有的 value 增强 for----");
for (Object value : values) {
System.out.println(value);
}
//(2) 迭代器
System.out.println("---取出所有的 value 迭代器----");
Iterator iterator2 = values.iterator();
while (iterator2.hasNext()) {
Object value = iterator2.next();
System.out.println(value);
}


//第三组: 通过 EntrySet 来获取 k-v
Set entrySet = map.entrySet();// EntrySet<Map.Entry<K,V>>
//(1) 增强 for
System.out.println("----使用 EntrySet 的 for 增强(第 3 种)----");
for (Object entry : entrySet) {
//将 entry 转成 Map.Entry
Map.Entry m = (Map.Entry) entry;
System.out.println(m.getKey() + "-" + m.getValue());
}
//(2) 迭代器
System.out.println("----使用 EntrySet 的 迭代器(第 4 种)----");
Iterator iterator3 = entrySet.iterator();
while (iterator3.hasNext()) {
Object entry = iterator3.next();
//System.out.println(next.getClass());//HashMap$Node -实现-> Map.Entry (getKey,getValue)
//向下转型 Map.Entry
Map.Entry m = (Map.Entry) entry;
System.out.println(m.getKey() +  m.getValue())
}
```

##### HashMap(不安全)

1) Map接口的常用实现类: HashMap、Hashtable和Properties。
2) HashMap是Map接口**使用频率最高**的实现类。
3) HashMap是以**key-val对的方式来存储**数据(HashMap$Node类型) [案例Entry ] 
4) key不能重复，但是值可以重复,允许使用nul键和null值。
5)如果**添加相同的key，则会覆盖原来的key-val** ,等同于修改.(key不会替换，val会替换)
6)与HashSet-样，不保证映射的顺序，因为底层是以hash表的方式来存储的. (jdk8的hashMap底层数组+链表+红黑树)
7) HashMap**没有实现同步**，因此是**线程不安全**的，方法没有做同步互斥的操作，没有synchronized

底层机制：

1) HashMap底层**维护了Node类型的数组tabl**e,默认为null
2)当创建对象时，将加载因子(loadfactor)初始化为0.75.
3)当添加key-val时，通过key的哈希值得到在table的索引。然后判断该索引处是否有元素，如果没有元素直接添加。如果该索引处有元素，继续判断该元素的key和准备加入的key相是否等，如果相等，则直接替换val;如果不相等需要判断是树结构还是链表结构，做出相应处理。如果添加时发现容量不够，则需要扩容。
4)第1次添加，则需要扩容table容量为16,临界值(threshold)为12 (16*0.75)
5)以后再扩容，则需要扩容table容量为原来的2倍(32)，临界值为原来的2倍,即24,依次类推，
6)在Java8中，如果一条链表的元素个数超过TREEIFY THRESHOLD(默认是8)，并且table的大小>= MIN TREEIFY CAPACITY(默认64),就会进行树化(红黑树)



##### Hashtable(安全，键和值都不能为空)

1)存放的**元素是键值对:**即K-V
2) hashtable的**键和值都不能为null**,否则会抛出NullPointerException
3) hashTable使用方法基本上和HashMap-样
4) hashTable是线程安全的(synchronized), hashMap 是线程不安全的

5)**效率比HashMap高**



##### Properties(可以做配置文件)

1. Properties类继承自Hashtable类并且实现了Map接口， 也是使用一种**键值对的形式来保存数据。**

2. 他的使用**特点和Hashtable类似**(键和值都不能为空)

3. Properties还**可以用于从xx.properties文件中，加载数据到Properties类对象**，并进行读取和修改

4. 说明:工作后xxx.properties文件通常**作为配置文件**，这个知识点在IO流举例，有兴趣可先看文章

    

##### TreeMap(自定义键有序)

```java
//使用默认的构造器，创建 TreeMap, 是无序的(也没有排序)
/*
老韩要求：按照传入的 k(String) 的大小进行排序
*/
// TreeMap treeMap = new TreeMap();
TreeMap treeMap = new TreeMap(new Comparator() {
@Override
public int compare(Object o1, Object o2) {
//按照传入的 k(String) 的大小进行排序
//按照 K(String) 的长度大小排序
//return ((String) o2).compareTo((String) o1);
return ((String) o2).length() - ((String) o1).length();
}
});
treeMap.put("jack", "杰克");
treeMap.put("tom", "汤姆");
treeMap.put("kristina", "克瑞斯提诺");
treeMap.put("smith", "斯密斯");
treeMap.put("hsp", "韩顺平");//加入不了
System.out.println("treemap=" + treeMap);
/*
老韩解读源码：

1. 构造器. 把传入的实现了 Comparator 接口的匿名内部类(对象)，传给给 TreeMap 的 comparator
public TreeMap(Comparator<? super K> comparator) {
this.comparator = comparator;
}
2. 调用 put 方法
2.1 第一次添加, 把 k-v 封装到 Entry 对象，放入 root
Entry<K,V> t = root;
if (t == null) {
compare(key, key); // type (and possibly null) check
root = new Entry<>(key, value, null);
size = 1;
modCount++;
return null;
}
2.2 以后添加
Comparator<? super K> cpr = comparator;
if (cpr != null) {
do { //遍历所有的 key , 给当前 key 找到适当位置
parent = t;
cmp = cpr.compare(key, t.key);//动态绑定到我们的匿名内部类的 compare
if (cmp < 0)
t = t.left;
else if (cmp > 0)
t = t.right;
else //如果遍历过程中，发现准备添加 Key 和当前已有的 Key 相等，就不添加
韩顺平循序渐进学 Java 零基础
第 692页
return t.setValue(value);
} while (t != null);
}
*/
```



### 集合的实现类的选择（有无序，是否重复，键值对...)

在开发中，选择什么集合实现类，主要取决于业务操作特点，然后根据集合实现类特性进行
选择，分析如下:
1)先判断存储的类型(- 组对象[单列]或一 组键值对[双列])
2)一组对象[单列]: Collection接口
	允许重复: List
		增删多: LinkedList [底层维护了一个双向链表]
		改查多: ArrayList [底层维护Object类型的可变数组]
	不允许重复: Set
		无序: HashSet [底层是HashMap，维护了-个哈希表即(数组+链表+红黑树)]
		排序: TreeSet
	    插入和取出顺序一致: LinkedHashSet ， 维护数组+双向链表
3)、 一组键值对[双列]: Map 
	键无序: HashMap [底层是:哈希表jdk7: 数组+链表，jdk8: 数组+链表+红黑树]
	键排序: TreeMap [老韩举例说明]
	键插入和取出顺序一致: LinkedHashMap
	读取文件Properties

### Collections 工具类

1 Collections是个**操作Set、List 和Map等集合的工具类**
2) Collections中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作
**排序操作:**
(均为static方法)
1) reverse(List):**反转**List中元素的顺序
2) shuffle(List): 对List集合元素进行**随机**排序
3) sort(List): 根据元素的**自然顺序**对指定 List集合元素按升序排序
4) sort(List, Comparator): 根据指定的**Comparator产生的顺序**对List集合元素进行
排序
5) swap(List, int, int): 将指定list 集合中的i处元素和j处元素进行**交换**
**查找、替换：**
1) Object max(Collection):根据元素的自然顺序，返回给定集合中的**最大元素**
2) Object max(Collection, Comparator): 根据**Comparator指定的顺序**，返回给定集合中的最大元素
3) Object min(Collection)
4) Object min(Collection, Comparator)
5) int frequency(Collection, Object): 返回指定集合中指定**元素的出现次数**
6) void copy(List dest,List src): 将src中的内容**复制**到dest中
7) boolean replaceAll(List list, Object oldVal, Object newVal): 使用新值**替换**List对象的所有旧值

```java
public class Collections_ {
public static void main(String[] args) {
//创建 ArrayList 集合，用于测试. List list = new ArrayList();
list.add("tom");
list.add("smith");
list.add("king");
list.add("milan");
list.add("tom");
// reverse(List)：反转 List 中元素的顺序
Collections.reverse(list);
System.out.println("list=" + list);
// shuffle(List)：对 List 集合元素进行随机排序
// for (int i = 0; i < 5; i++) {
// Collections.shuffle(list);
// System.out.println("list=" + list);
// }
// sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
Collections.sort(list);
System.out.println("自然排序后");

System.out.println("list=" + list);
// sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
//我们希望按照 字符串的长度大小排序
Collections.sort(list, new Comparator() {
@Override
public int compare(Object o1, Object o2) {
//可以加入校验代码. return ((String) o2).length() - ((String) o1).length();
}
});
System.out.println("字符串长度大小排序=" + list);
// swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换
//比如
Collections.swap(list, 0, 1);
System.out.println("交换后的情况");
System.out.println("list=" + list);
//Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
System.out.println("自然顺序最大元素=" + Collections.max(list));
//Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
//比如，我们要返回长度最大的元素
Object maxObject = Collections.max(list, new Comparator() {
@Override
public int compare(Object o1, Object o2) {
return ((String)o1).length() - ((String)o2).length();

}
});
System.out.println("长度最大的元素=" + maxObject);
//Object min(Collection)
//Object min(Collection，Comparator)
//上面的两个方法，参考 max 即可
//int frequency(Collection，Object)：返回指定集合中指定元素的出现次数
System.out.println("tom 出现的次数=" + Collections.frequency(list, "tom"));
//void copy(List dest,List src)：将 src 中的内容复制到 dest 中
ArrayList dest = new ArrayList();
//为了完成一个完整拷贝，我们需要先给 dest 赋值，大小和 list.size()一样
for(int i = 0; i < list.size(); i++) {
dest.add("");
}
//拷贝
Collections.copy(dest, list);
System.out.println("dest=" + dest);
//boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值
//如果 list 中，有 tom 就替换成 汤姆
Collections.replaceAll(list, "tom", "汤姆");

System.out.println("list 替换后=" + list);
}
```



# 泛型

1)泛型又称参数化类型， 是Jdk5.0出现的新特性,，**解决数据类型的安全性问题**
2)在类声明或实例化时只要指定好需要的具体的类型即可。
3) Java泛型可以保证如果程序在编译时没有发出警告， 运行时就不会产生ClassCastException异常。同时，代码更加**简洁、健壮**
4)泛型的作用是:可以在类声明时通过一个标识表示类中某个属性的类型，或者是某个方法的返回值的类型，或者是参数类型。



### **泛型的声明**

interface接口<T> {}和class类<K,V> }
//比如: List，ArrayList
说明:
1)其中，T,K,V不代表值，而是表示类型。
2)任意字母都可以。常用T表示，是Type的缩写
**泛型的实例化**
要在类名后面指定类型参数的值(类型) 。如:
1) List<String> strList = new ArrayList <String> ();
2) Iterator< Customer> iterator = customers.iterator();

泛型使用的**注意事项和细节**
1. interface List<T>{} ，public class HashSet<E>{}..等等
说明: **T, E只能是引用类型**
看看下面语句是否正确?: 
List<Integer> list = new ArrayList< Integer> (); //OK
List<int> list2 = new ArrayList < int> 0);//错误
2. 在给泛型指定具体类型后，可以**传入该类型或者其子类类型**
3. 泛型使用形式
    List<Integer> list1 = new ArrayList <Integer> ();
    List <Integer> list2 = new ArrayList<> (); [说明:]
4. 如果我们这样写List list3 = new ArrayList(; **默认给它的泛型是[<E> E就是Object** ]



### 自定义泛型

##### 自定义泛型类

**基本语法**
class类名<T, R...> { /...表示可以有多个泛型成员

**注意细节**
1)**普通成员可以使用泛型**(属性、方法)
2)使用**泛型的数组，不能初始化** （不能new和赋初值）
3**)静态方法中不能使用类的泛型**（因为静态是和类相关的，在类加载时，对象还没有创建 ，所以，如果静态方法和静态属性使用了泛型，	JVM 就无法完成初始）
4)泛型类的**类型，是在创建对象时确定的**(因为创建对象时，需要指定确定类型)
5)如果在创建对象时，没有指定类型，**默认为Object**



##### **自定义泛型接口**

**基本语法**
interface 接口名<T, R..> {
**注意细节**
1)接口中，静态成员也不能使用泛型(这个和泛型类规定一样)
2)**泛型接口的类型，在继承接口或者实现接口时确定**
3) 没有指定类型， 默认为Object



##### 自定义泛型方法

**基本语法**
修饰符<T,R..>返回类型方法名(参数列表) {
**注意细节**
1.泛型方法，可以定义在**普通类**中，也可以定义在**泛型类**中
2.当泛型**方法被调用时，类型会确定**

3.public void eat(E e) {}**,修饰符后没有<T,R..>** eat方法**不是泛型方法，而是使用了泛型**（使用泛型只能在泛型类中使用，而泛型方法可以在普通类中使用）

```java
public class CustomMethodGeneric {
public static void main(String[] args) {
Car car = new Car();
car.fly("宝马", 100);//当调用方法时，传入参数，编译器，就会确定类型
System.out.println("=======");
car.fly(300, 100.1);//当调用方法时，传入参数，编译器，就会确定类型
//测试
//T->String, R-> ArrayList
Fish<String, ArrayList> fish = new Fish<>();
fish.hello(new ArrayList(), 11.3f);
}
}
//泛型方法，可以定义在普通类中, 也可以定义在泛型类中
class Car {//普通类
public void run() {//普通方法
}

//说明 泛型方法
//1. <T,R> 就是泛型
//2. 是提供给 fly 使用的
public <T, R> void fly(T t, R r) {//泛型方法
System.out.println(t.getClass());//String
System.out.println(r.getClass());//Integer
}
}
class Fish<T, R> {//泛型类
public void run() {//普通方法
}
public<U,M> void eat(U u, M m) {//泛型方法
}
//说明
//1. 下面 hi 方法不是泛型方法
//2. 是 hi 方法使用了类声明的 泛型
public void hi(T t) {
}
//泛型方法，可以使用类声明的泛型，也可以使用自己声明泛型
public<K> void hello(R r, K k) {
System.out.println(r.getClass());//ArrayList
System.out.println(k.getClass());//Float
}
}
```

```java
public class CustomMethodGenericExercise {
public static void main(String[] args) {
//T->String, R->Integer, M->Double
Apple<String, Integer, Double> apple = new Apple<>();
apple.fly(10);//10 会被自动装箱 Integer10, 输出 Integer
apple.fly(new Dog());//Dog

}
}
class Apple<T, R, M> {//自定义泛型类
public <E> void fly(E e) { //泛型方法
System.out.println(e.getClass().getSimpleName());
}
//public void eat(U u) {}//错误，因为 U 没有声明
public void run(M m) {
} //ok
}
class Dog {
}
```

### **泛型的继承和通配符**

泛 型的继承和通配符说明
1)**泛型不具备继承性**  (**我的理解 带有泛型无法强制转换**) 
	List<Object> list = new ArrayList<String> 0; //错

```java
public List<T> list()//返回map中存放的所有T对象
{
    return new ArrayList<T>(map.values());
}对
public List<T> list()//返回map中存放的所有T对象
{
    return (List<T>)map.values();
}错
```

2) **<?> :支持任意泛型类型**
3) **<? extends A>:支持A类以及A类的子类**，规定了泛型的上限
4) **<? super A>:支持A类以及A类的父类，不限于直接父类**，规定了泛型的下限

```java
public class GenericExtends {
public static void main(String[] args) {
Object o = new String("xx");
//泛型没有继承性
//List<Object> list = new ArrayList<String>();
//举例说明下面三个方法的使用
List<Object> list1 = new ArrayList<>();
List<String> list2 = new ArrayList<>();
List<AA> list3 = new ArrayList<>();
List<BB> list4 = new ArrayList<>();
List<CC> list5 = new ArrayList<>();
//如果是 List<?> c ，可以接受任意的泛型类型
printCollection1(list1);
printCollection1(list2);

printCollection1(list3);
printCollection1(list4);
printCollection1(list5);
//List<? extends AA> c： 表示 上限，可以接受 AA 或者 AA 子类
// printCollection2(list1);//×
// printCollection2(list2);//×
printCollection2(list3);//√
printCollection2(list4);//√
printCollection2(list5);//√
//List<? super AA> c: 支持 AA 类以及 AA 类的父类，不限于直接父类
printCollection3(list1);//√
//printCollection3(list2);//×
printCollection3(list3);//√
//printCollection3(list4);//×
//printCollection3(list5);//×
//冒泡排序
//插入排序
//....

}
// ? extends AA 表示 上限，可以接受 AA 或者 AA 子类
public static void printCollection2(List<? extends AA> c) {
for (Object object : c) {
System.out.println(object);
}
}
//说明: List<?> 表示 任意的泛型类型都可以接受
public static void printCollection1(List<?> c) {
for (Object object : c) { // 通配符，取出时，就是 Object
System.out.println(object);
}
}
// ? super 子类类名 AA:支持 AA 类以及 AA 类的父类，不限于直接父类，
//规定了泛型的下限
public static void printCollection3(List<? super AA> c) {
for (Object object : c) {
System.out.println(object);
}
}
}

```

# 线程

**进程**

1.进程是指运行中的程序，比如我们使用QQ，就启动了-一个进程，操作系统就会为该进程分配内存空间。当我们使用迅雷，又启动了-个进程，操作系统将为迅雷分配新的内存空间。
2.进程是程序的一次执行过程，或是正在运行的-个程序。是动态过程:有它自身的产生、存在和消亡的过程

**线程**

1.线程由进程创建的，是进程的一个实体

2.一个进程可以拥有多个线程

1.单线程:同个时刻，只允许执行一个线程
2.多线程:同一个时刻，可以执行多个线程，比如:一个qq进程，可以同时打开多个聊天窗口，一个迅雷进程，可以同时下载多个文件

3.并发:同一个时刻，多个任务交替执行，造成种“貌似同时”的错觉，简单的说，单核cpu实现的多任务就是并发。

4.并行:同一个时刻，多个任务同时执行。多核cpu可以实现并行。

**线程的创建**

### Thread类和Runnable接口

1. java是**单继承**的，在某些情况下一个类可能已经继承了某个父类,这时在用继承Thread类方法来创建线程 显然不可能了。
2. java设计者们提供 了另外个方式创建线程， 就是通过实现Runnable**接口来创建线程**

1. java的设计来看，通过继承Thread或者实现Runnable接口来创建线程**本质上没有区别**,从jdk帮助文档我们可以看到Thread类本身就实现了Runnable接口

2. 实现Runnable接口方式更加适合多个线程共享-个资源的情况，并且避免了单继承的限制，**建议使用Runnable**

  **继承Thread代码**

  start()方法调用start0()方法后，该线程并不一-定会立马执行，只是将线程变成了可运行状态。具
  体什么时候执行，取决于CPU,由CPU统一调度。

  //start0() 是本地方法，是 JVM 调用, 底层是 c/c++实现
  //真正实现多线程的效果， 是 start0(), 而不是 run

  //run 方法就是一个普通的方法, 没有真正的启动一个线程

  //1. 当一个类继承了 Thread 类， 该类就可以当做线程使用
  //2. 我们会重写 run 方法，写上自己的业务代码
  //3. run Thread 类 实现了 Runnable 接口的 run 方法

```java
public class Thread01 {
    public static void main(String[] args) throws InterruptedException {
        //创建 Cat 对象，可以当做线程使用
        Cat cat = new Cat();
//老韩读源码
/*

(1)
public synchronized void start() {
start0();
}
(2)
//start0() 是本地方法，是 JVM 调用, 底层是 c/c++实现
//真正实现多线程的效果， 是 start0(), 而不是 run
private native void start0();
*/
        cat.start();//启动线程-> 最终会执行 cat 的 run 方法
        //cat.run();//run 方法就是一个普通的方法, 没有真正的启动一个线程，就会把 run 方法执行完毕，才向下执行
        //说明: 当 main 线程启动一个子线程 Thread-0, 主线程不会阻塞, 会继续执行
        //这时 主线程和子线程是交替执行.. System.out.println("主线程继续执行" + Thread.currentThread().getName());//名字 main
        for(int i = 0; i < 60; i++) {
            System.out.println("主线程 i=" + i);
        //让主线程休眠
            Thread.sleep(1000);
        }
    }
 
}
//老韩说明
//1. 当一个类继承了 Thread 类， 该类就可以当做线程使用
//2. 我们会重写 run 方法，写上自己的业务代码
//3. run Thread 类 实现了 Runnable 接口的 run 方法
/*
@Override
public void run() {
if (target != null) {
target.run();
}
}
*/
class Cat extends Thread {
    int times = 0;
    @Override
    public void run() {//重写 run 方法，写上自己的业务逻辑
        while (true) {
        //该线程每隔 1 秒。在控制台输出 “喵喵, 我是小猫咪”
            System.out.println("喵喵, 我是小猫咪" + (++times) + " 线程名=" + Thread.currentThread().getName());
         
        //让该线程休眠 1 秒 ctrl+alt+t
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if(times == 80) {
                break;//当 times 到 80, 退出 while, 这时线程也就退出.. }
            }
        }
    }
```

**实现Runnable接口代码**

//dog.start(); 这里不能调用 start
//创建了 Thread 对象，把 dog 对象(实现 Runnable),放入 Thread

```java
public class Thread02 {
    public static void main(String[] args) {
        Dog dog = new Dog();
//dog.start(); 这里不能调用 start
//创建了 Thread 对象，把 dog 对象(实现 Runnable),放入 Thread
        Thread thread = new Thread(dog);
        thread.start();
// Tiger tiger = new Tiger();//实现了 Runnable
// ThreadProxy threadProxy = new ThreadProxy(tiger);
// threadProxy.start();
   
    }
}
class Animal {
}
class Tiger extends Animal implements Runnable {
    @Override
    public void run() {
        System.out.println("老虎嗷嗷叫....");
    }
}
//线程代理类 , 模拟了一个极简的 Thread 类
class ThreadProxy implements Runnable {//你可以把 Proxy 类当做 ThreadProxy
    private Runnable target = null;//属性，类型是 Runnable
    @Override
    public void run() {
        if (target != null) {
            target.run();//动态绑定（运行类型 Tiger）
        }
    }

    public ThreadProxy(Runnable target) {
        this.target = target;
    }
    public void start() {
        start0();//这个方法时真正实现多线程方法
    }
    public void start0() {
        run();
    }
}
class Dog implements Runnable { //通过实现 Runnable 接口，开发线程
    int count = 0;
    @Override
    public void run() { //普通方法
        while (true) {
            System.out.println("小狗汪汪叫..hi" + (++count) + Thread.currentThread().getName());
//休眠 1 秒
            try {
                Thread.sleep(1000);
      
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (count == 10) {
                break;
            }
        }
    }
}
```

**常用方法**

1. setName //设置线程名称，使之与参数name相同
2. getName //返回该线程的名称
3. start //使该线程开始执行; Java虚拟机底层调用该线程的startO方法  start底层会创建新的线程，调用run,
4. run //调用线程对象run方法;  run 就是一个简单的方法调用，不会启动新线程
5. setPriority //更改线程的优先级
6. getPriority //获取线程的优先级
7. sleep //在指定的毫秒数内让当前正在执行的线程休眠(暂停执行) sleep:线程的静态方法，使当前线程休眠
8. interrupt //中断线程  interrupt,中断线程，但并没有真正的结束线程。所以般用于中断正在休眠线程

### yield和join(抢占cpu)

1. yield:线程的礼让。让出cpu,让其他线程执行，但礼让的时间不确定，所以也不一定礼让成功
2. join:线程的插队。插队的线程一旦插队成功，则肯定先执行完插入的线程所有的任务


```java
/**
 * @author Deng Junsong
 * @date 2022-01-25 18:31:43
 * @description
 *
 * 1.主线程每隔1s,输出hi,一共10次
 * 2.当输出到hi 5时，启动一个子线程(要求
 * 实现Runnable),每隔1s输出hello ,等
 * 该线程输出10次hello后,退出
 * 3.主线程继续输出hi ,直到主线程退出
 * 4.如图，完成代码其实线程插队..
 */
public class Thread_ {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(new T());//创
        for (int i = 0; i < 10; i++) {
            System.out.println("hi"+i);
            if(i==5){
               t.start();
               t.join();
            }
            Thread.sleep(1000);
        }
    }
}
class T implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("hello"+i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}
```

### 用户线程和守护线程(自动结束线程)

1.用户线程:也叫工作线程，当线程的任务执行完或通知方式结束
2.守护线程:一般是为工作线程服务的，当所有的用户线程结束，守护线程自动结束
3.常见的守护线程:垃圾回收机制



  //如果我们希望当main线程结束后，子线程自动结束
  //,只需将子线程设为守护线程即可,**myDaemonThread.setDaemon(true);**

```java
public class ThreadMethod03 {
    public static void main(String[] args) throws InterruptedException {
        MyDaemonThread myDaemonThread = new MyDaemonThread();
        //如果我们希望当main线程结束后，子线程自动结束
        //,只需将子线程设为守护线程即可
        myDaemonThread.setDaemon(true);
        myDaemonThread.start();

        for( int i = 1; i <= 10; i++) {//main线程
            System.out.println("宝强在辛苦的工作...");
            Thread.sleep(1000);
        }
    }
}

class MyDaemonThread extends Thread {
    public void run() {
        for (; ; ) {//无限循环
            try {
                Thread.sleep(1000);//休眠1000毫秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("马蓉和宋喆快乐聊天，哈哈哈~~~");
        }
    }
}
```

### 同步（synchronized)和互斥

1.在多线程编程，一些敏感数据不允许被多个线程同时访问，此时就使用同步访问技术，保证数据在任何同-时刻，最多有一个线程访问，以保证数据的完整性。
2.也可以这里理解:线程同步，即当有一个线程在对内存进行操作时，其他线程都不可以对这个内存地址进行操作，直到该线程完成操作，其他线程才能对该内存地址进行操作.

```
1.
同步代码块
synchronized (对象) { // 得到对象的锁，才能操作同步代码
/需要被同步代码;
}
2. synchronized还可以放在方法声明中， 表示整个方法为同步方法
public synchronized void m (String name){
//需要被同步的代码
}
```



1. Java语言中，引入了对象互斥锁的概念，来保证共享数据操作的完整性。

2. 每个对象都对应于一一个可称为“互斥锁"的标记，这个标记用来保证在任时刻，**只能有一个线程访问该对象**。

3. 关键字synchronized来与对象的互斥锁联系。当某个对象用synchronized修饰时，表明该对象在任一时刻只能由一 个线程访问

4. 同步的局限性:导致程序的**执行效率要降低**

5. **同步方法(非静态的)的锁可以是this,也可以是其他对象(要求是同一个对象)**

6. **同步方法(静态的)的锁为当前类本身。**

  

**注意事项和细节**
1.**同步方法如果没有使用static修饰**: **默认锁对象为this**
2.**如果方法使用static修饰，默认锁对象:当前类.class**
3.实现的落地步骤:
需要先分析，上锁的代码
选择同步代码块或同步方法
要求多个线程的锁对象为同一个即可!



        //这是一个对象对应多线程 synchronized(this)this是同一对象sellTicket03
        new Thread(sellTicket03).start();//第 1 个线程-窗口
        new Thread(sellTicket03).start();//第 2 个线程-窗口
        new Thread(sellTicket03).start();//第 3 个线程-窗口


​        
​      //这是三个对象，所有不能使用synchronized(this)
​      new T().start();
​      new T().start();
​      new T().start();
​      class T extends Thread{
​      	public synchronized(this) void run(){
​      			...
​      	}
​      }
```java
package com.company.tankgame.Thread_;

/**
 * @author Deng Junsong
 * @date 2022-01-25 21:28:39
 * @description
 */
public class Synchronized_ {
    public static void main(String[] args) {
        SellTicket03 sellTicket03 = new SellTicket03();
        new Thread(sellTicket03).start();//第 1 个线程-窗口
        new Thread(sellTicket03).start();//第 2 个线程-窗口
        new Thread(sellTicket03).start();//第 3 个线程-窗口
    }
}
//实现接口方式, 使用 synchronized 实现线程同步
class SellTicket03 implements Runnable {
    private int ticketNum = 100;//让多个线程共享 ticketNum
    private boolean loop = true;//控制 run 方法变量
    Object object = new Object();
//同步方法（静态的）的锁为当前类本身
//老韩解读
//1. public synchronized static void m1() {} 锁是加在 SellTicket03.class
//2. 如果在静态方法中，实现一个同步代码块.
/*
    synchronized (SellTicket03.class) {
        System.out.println("m2");
    }
*/
    public synchronized static void m1() {
    }
    public static void m2() {
        synchronized (SellTicket03.class) {
            System.out.println("m2");
        }
    }
    //老韩说明
//1. public synchronized void sell() {} 就是一个同步方法
//2. 这时锁在 this 对象
//3. 也可以在代码块上写 synchronize ,同步代码块, 互斥锁还是在 this 对象

    public /*synchronized*/ void sell() { //同步方法, 在同一时刻， 只能有一个线程来执行 sell 方法

        synchronized (/*this*/ object) {
            if (ticketNum <= 0) {
                System.out.println("售票结束...");
                loop = false;
                return;
            }
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口 " + Thread.currentThread().getName() + " 售出一张票" + " 剩余票数=" + (--ticketNum));//1 - 0 - -1 - -2
        }
    }
    @Override
    public void run() {
        while (loop) {
            sell();//sell 方法是一共同步方法
        }
    }

}
```

### volatile(共享变量)

1、什么是volatile
volatile是Java提供的一种轻量级的同步机制。Java语言包含两种同步机制：1、同步块(或同步方法) 2、volatile变量。相比于synchronized加锁同步，volatile关键字比较轻量级，开销更低，因为他不会引起线程上下文的切换调度。

2、volatile定义
Java编程语言允许线程访问共享变量，为了确保共享变量能被准确和一致地更新，线程应该确保通过排他锁单独获得这个变量。Java语言提供了volatile，在某些情况下比锁要更加方便。如果一个字段被声明成volatile，Java线程内存模型确保所有线程看到这个变量的值是一致的。

3、volatile关键字的作用
volatile关键字保证了共享变量在多个线程中的可见性。当一个线程修改了共享变量的值时，其他的线程能够看见这个值的改变，并且将重新读取该值。

说明： 共享变量一般是存放在主存中，在多线程中每一个要使用到共享变量的线程都需要将主存中的共享变量拷贝一份放入到自己的工作内存中（线程私有，高速缓存）。每一个线程中都是读取的自己工作内存里共享变量的副本值来进行相关操作，而不会每次都会去访问主存取值(CPU直接访问主存效率低下)。
问题： 如果现在有一个线程（线程A）修改了自己的值。但是别的线程都不知道该值已经改变了，所以还是继续延用他们各自从主存中拷贝过来的共享变量值的副本。这样就会造成一些多线程相关的问题。

```
public class TestVolatitle1 {

	public static void main(String[] args) {
		ThreadDemo td = new ThreadDemo();
		Thread threadA = new Thread(td);
		threadA.start();
		
		while (true) {
			if (td.isFlag()) {
				System.out.println("------------------");
				break;
			}
		}
	}
}
class ThreadDemo implements Runnable {

	private boolean flag = false;
	@Override
	public void run() {
		try {
			Thread.sleep(200);
		} catch (InterruptedException e) {}
		flag = true;
		System.out.println("flag=" + isFlag());
	}

	public boolean isFlag() {
		return flag;
	}

	public void setFlag(boolean flag) {
		this.flag = flag;
	}
}

```

代码解释：
1、在以上代码中，一共有两个线程，一个是我们手动开启的线程threadA，一个是主线程。ThreadDemo td = new ThreadDemo(); 是创建一个共享变量td。
2、在线程threadA中会执行 run() 方法，先休眠200毫秒，然后将flag的值改变为true。
3、在主线程中while循环会一直不停的判断共享变量的flag值是否为true，若为true则结束程序。点击运行该程序以后发现，运行结果并不是我们想象的那样。主线程中的while循环一直不会结束。
问题产生原因：
首先线程threadA和主线程都去主存中拷贝一份共享变量的值，放入到自己的工作内存中。线程threadA将自己工作内存中的flag值改变成了true。但是主线程工作内存中的值并没有改变（依然是false），所以while循环就会一直循环不会结束。
问题解决：
当我们给共享变量flag加上volatile关键字修饰以后，程序正常运行并结束了。

**详解：**

1、给共享变量添加了volatile关键字修饰后。首先，线程threadA和主线程都会去主存中拷贝一份共享变量的值。
2、然后在线程A中将flag的值改变了，同时主线程里面的while循环也一直在执行。线程A将共享变量的flag值改变为true了。然后线程A就将flag改变后的值刷写到主存中。
3、当主存中共享变量的值更改以后，会导致其他线程中的共享变量副本失效，这时候其他线程需要重新从主存中读取一次共享变量的值到线程的工作内存中。
4、当主线程重新从主存读取共享变量的值以后，读取到的flag的值为true，此时while循环就结束了。

### 死锁与释放锁

多个线程都占用了对方的锁资源，但不肯相让，导致了死锁，在编程是一定要避免死锁的发生

```
public class DeadLock_ {
    public static void main(String[] args) {
//模拟死锁现象
        DeadLockDemo A = new DeadLockDemo(true);
        A.setName("A 线程");
        DeadLockDemo B = new DeadLockDemo(false);
        B.setName("B 线程");
        A.start();
        B.start();
    }
}
    //线程

class DeadLockDemo extends Thread {
    static Object o1 = new Object();// 保证多线程，共享一个对象,这里使用 static
    static Object o2 = new Object();
    boolean flag;
    public DeadLockDemo(boolean flag) {//构造器
        this.flag = flag;
    }
    @Override
    public void run() {
        //下面业务逻辑的分析
        //1. 如果 flag 为 T, 线程 A 就会先得到/持有 o1 对象锁, 然后尝试去获取 o2 对象锁
        //2. 如果线程 A 得不到 o2 对象锁，就会 Blocked
        //3. 如果 flag 为 F, 线程 B 就会先得到/持有 o2 对象锁, 然后尝试去获取 o1 对象锁
        //4. 如果线程 B 得不到 o1 对象锁，就会 Blocked
        if (flag) {
            synchronized (o1) {//对象互斥锁, 下面就是同步代码
                System.out.println(Thread.currentThread().getName() + " 进入 1");
                synchronized (o2) { // 这里获得 li 对象的监视权
                    System.out.println(Thread.currentThread().getName() + " 进入 2");
                }
            }
        } else {
           
            synchronized (o2) {
                System.out.println(Thread.currentThread().getName() + " 进入 3");
                synchronized (o1) { // 这里获得 li 对象的监视权
                    System.out.println(Thread.currentThread().getName() + " 进入 4");
                }
            }
        }
    }
}
```

**下面操作会释放锁**
1.当前线程的同步方法、 同步代码块执行结束
案例:上厕所， 完事出来
2.当前线程在同步代码块、同步方法中遇到break、return.
案例:没有正常的完事，经理叫他修改bug,不得已出来
3.当前线程在同步代码块、同步方法中出现了未处理的Error或Exception,导致异常结束
案例:没有正常的完事，发现忘带纸，不得已出来
4.当前线程在同步代码块、同步方法中执行了线程对象的wait(方法，当前线程暂停，并释
放锁。
案例:没有正常完事，觉得需要酝酿下，所以出来等会再进去
**下面操作不会释放锁**

1.线程执行同步代码块或同步方法时，程序调用Thread.sleep()、 Thread.yield(方法暂停当前线程的执行，不会释放锁
案例:上厕所， 太困了，在坑位上眯了一会
2.线程执行同步代码块时，其他线程调用了该线程的suspend(方法将该线程挂起，该线程不会释放锁。
提示:应尽量避免使用suspend()和resume()来控制线程，方法不再推荐使用

# 文件

字符流和字节流**区别**
实际上字节流在操作时本身不会用到缓冲区（内存），是文件本身直接 操 作的，而字符流在操作时使用了缓冲区，通过缓冲区再操作文件

字节流操作的基本单元为字节；字符流操作的基本单元为Unicode码元
字节流默认不使用缓冲区；字符流使用缓冲区
字节流通常用于处理二进制数据，实际上它可以处理任意类型的数据，但它不支持直接写入或读取Unicode码元；字符流通常处理文本数据，它支持写入及读取Unicode码元。

### **使用场景**

使用字符流的应用场景： 如果是读写字符数据的时候则使用字符流。
使用字节流的应用场景： 如果读写的数据都不需要转换成字符的时候，则使用字节流。
一般来说 自己能写的代码用字符流
自己不能写的用字节流,比如图片,视频,音频
字节流用的多

**常用构造器**

new File(String pathname) //根据路径构建一个File对象
new File(File parent, String child) //根据父目录文件+子路径构建
new File(String parent,String child) //根据父目录+子路径构建
createNewFile创建新文件

mkdir创建一 级目录、mkdirs创建多级目录、delete删除空目录或文件

**获取文件的相关信息**

```
    //先创建文件对象
    File file = new File("e:\\news1.txt");
//调用相应的方法，得到对应信息
System.out.println("文件名字=" + file.getName());
//getName、getAbsolutePath、getParent、length、exists、isFile、isDirectory
        System.out.println("文件绝对路径=" + file.getAbsolutePath());
        System.out.println("文件父级目录=" + file.getParent());
        System.out.println("文件大小(字节)=" + file.length());
        System.out.println("文件是否存在=" + file.exists());//T
        System.out.println("是不是一个文件=" + file.isFile());//T
        System.out.println("是不是一个目录=" + file.isDirectory());//F
```

###  节点流FileReader 和 FileWriter

**详情见**：https://blog.csdn.net/qq_43470705/article/details/106136276

**FileReader 相关方法:**
1) new FileReader(File/String)
2) read:每次读取单个字符，返回该字符，如果到文件末尾返回-1
3) read(char[]):批量读取多个字符到数组，返回读取到的字符数，如果到文件末尾返回-1
相关API: 
1) new String(char[]):将char[]转换成String
2) new String(char[],off,len):将char]的指定部分转换成String
 **FileWriter 常用方法**
new FileWriter(File/String):覆盖模式，相当于流的指针在首端
2) new FileWriter(File/String,true):追加模式，相当于流的指针在尾端
3) write(int):写入单个字符
| 4) write(char[]):写入指定数组
5) write(char[,offlen):写入指定数组的指定部分
6) write (string) :写入整个字符串
7) write(string,off,len):写入字符串的指定部分
相关APl: String类 toCharArray:将String转换成char[]
➢注意:
**FileWriter使用后，必须要关闭(close)或刷新(flush), 否则写入不到指定的文件**! |

read:

```
    String filePath = "e:\\story.txt";
    FileReader fileReader = null;
    int data = 0;
//1. 创建 FileReader 对象
try{
        fileReader=new FileReader(filePath);
//循环读取 使用 read, 单个字符读取
        while((data=fileReader.read())!=-1){
        System.out.print((char)data);
        }
      
}catch(IOException e){
        e.printStackTrace();
        }finally{
                try{
                    if(fileReader!=null){
                        fileReader.close();
                    }
                 }catch(IOException e){
                 e.printStackTrace();
        }
}
    
/**
 * 字符数组读取文件
 */
        System.out.println("~~~readFile02 ~~~");
        String filePath="e:\\story.txt";
        FileReader fileReader=null;
        int readLen=0;
        char[]buf=new char[8];
//1. 创建 FileReader 对象
    
        try{
        fileReader=new FileReader(filePath);
//循环读取 使用 read(buf), 返回的是实际读取到的字符数
//如果返回-1, 说明到文件结束
        while((readLen=fileReader.read(buf))!=-1){
        System.out.print(new String(buf,0,readLen));
        }
        }catch(IOException e){
            e.printStackTrace();
        }finally{
                try{
                    if(fileReader!=null){
                        fileReader.close();
                    }
                }catch(IOException e){
                e.printStackTrace();
        }
       
    }
```

write:

```
public class FileWriter_ {
    public static void main(String[] args) {
        String filePath = "e:\\note.txt";
//创建 FileWriter 对象
        FileWriter fileWriter = null;
        char[] chars = {'a', 'b', 'c'};
        try {
            fileWriter = new FileWriter(filePath);//默认是覆盖写入
// 3) write(int):写入单个字符
            fileWriter.write('H');
// 4) write(char[]):写入指定数组
            fileWriter.write(chars);
// 5) write(char[],off,len):写入指定数组的指定部分
            fileWriter.write("韩顺平教育".toCharArray(), 0, 3);
// 6) write（string）：写入整个字符串
            fileWriter.write(" 你好北京~");
            fileWriter.write("风雨之后，定见彩虹");
          
// 7) write(string,off,len):写入字符串的指定部分
            fileWriter.write("上海天津", 0, 2);
//在数据量大的情况下，可以使用循环操作. } catch (IOException e) {
            e.printStackTrace();
        } finally {
//对应 FileWriter , 一定要关闭流，或者 flush 才能真正的把数据写入到文件
//老韩看源码就知道原因. /*
            看看代码
            private void writeBytes() throws IOException {
                this.bb.flip();
                int var1 = this.bb.limit();
                int var2 = this.bb.position();
                assert var2 <= var1;
                int var3 = var2 <= var1 ? var1 - var2 : 0;
                if (var3 > 0) {
                    if (this.ch != null) {
                        assert this.ch.write(this.bb) == var3 : var3;
                    } else {
                        this.out.write(this.bb.array(), this.bb.arrayOffset() + var2, var3);
                       
                    }
                }
                this.bb.clear();
            }
*/
            try {
//fileWriter.flush();
//关闭文件流，等价 flush() + 关闭
                fileWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        System.out.println("程序结束...");
    }
}
```



### 节点流FileInputStream和 FileOutputStream

**详情见**：https://blog.csdn.net/qq_43470705/article/details/106136276

output:

```
public class FileOutputStream01 {
    public static void main(String[] args) {
    }
/**
 * 演示使用 FileOutputStream 将数据写到文件中, * 如果该文件不存在，则创建该文件
 */
    @Test
   
    public void writeFile() {
//创建 FileOutputStream 对象
        String filePath = "e:\\a.txt";
        FileOutputStream fileOutputStream = null;
        try {
//得到 FileOutputStream 对象 对象
//老师说明
//1. new FileOutputStream(filePath) 创建方式，当写入内容是，会覆盖原来的内容
//2. new FileOutputStream(filePath, true) 创建方式，当写入内容是，是追加到文件后面
            fileOutputStream = new FileOutputStream(filePath, true);
//写入一个字节
//fileOutputStream.write('H');//
//写入字符串
            String str = "hsp,world!";
//str.getBytes() 可以把 字符串-> 字节数组
//fileOutputStream.write(str.getBytes());
/*
write(byte[] b, int off, int len) 将 len 字节从位于偏移量 off 的指定字节数组写入此文件输出流
*/
            fileOutputStream.write(str.getBytes(), 0, 3);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                
                fileOutputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

intput:

```
public class FileInputStream_ {
    public static void main(String[] args) {
       
    }
    /**
     * 演示读取文件... * 单个字节的读取，效率比较低
     * -> 使用 read(byte[] b)
     */
    @Test
    public void readFile01() {
        String filePath = "e:\\hello.txt";
        int readData = 0;
        FileInputStream fileInputStream = null;
        try {
//创建 FileInputStream 对象，用于读取 文件
            fileInputStream = new FileInputStream(filePath);
//从该输入流读取一个字节的数据。 如果没有输入可用，此方法将阻止。
//如果返回-1 , 表示读取完毕
            while ((readData = fileInputStream.read()) != -1) {
                System.out.print((char)readData);//转成 char 显示
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
//关闭文件流，释放资源.
          
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    /**
     * 使用 read(byte[] b) 读取文件，提高效率
     */
    @Test
    public void readFile02() {
        String filePath = "e:\\hello.txt";
//字节数组
        byte[] buf = new byte[8]; //一次读取 8 个字节. int readLen = 0;
        FileInputStream fileInputStream = null;
        try {
//创建 FileInputStream 对象，用于读取 文件
            fileInputStream = new FileInputStream(filePath);
//从该输入流读取最多 b.length 字节的数据到字节数组。 此方法将阻塞，直到某些输入可用。
//如果返回-1 , 表示读取完毕
//如果读取正常, 返回实际读取的字节数
            while ((readLen = fileInputStream.read(buf)) != -1) {
             
                System.out.print(new String(buf, 0, readLen));//显示
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
//关闭文件流，释放资源. try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
}
```

### 处理流-BufferedReader 和 BufferedWriter（高效快捷）

1.节点流是底层流/低级流,直接跟数据源相接。
2.处理流(包装流)包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入输出。 [源码理解]
3.处理流(也叫包装流)对节点流进行包装，使用了修饰器设计模式，不会直接与数据源相连[模拟修饰器设计模式=》小伙伴就会非常清楚]

1.**性能的提高:主要以增加缓冲的方式来提高输入输出的效率**。（直接按行读取）

2.**操作的便捷:处理流可能提供了一-系列便捷的方法来一 次输入输出大批量的数据**，使用更加灵活方便

➢BufferedReader 和BufferedWriter属于字符流，是按照字符来读取数据的
关闭时处理流，只需要关闭外层流即可[后面看源码]

read:

```
public class BufferedReader_ {
    public static void main(String[] args) throws Exception {
        String filePath = "e:\\a.java";
//创建 bufferedReader
        BufferedReader bufferedReader = new BufferedReader(new FileReader(filePath));
   
//读取
        String line; //按行读取, 效率高
//说明
//1. bufferedReader.readLine() 是按行读取文件
//2. 当返回 null 时，表示文件读取完毕
        while ((line = bufferedReader.readLine()) != null) {
            System.out.println(line);
        }
//关闭流, 这里注意，只需要关闭 BufferedReader ，因为底层会自动的去关闭 节点流
//FileReader。
/*
public void close() throws IOException {
synchronized (lock) {
if (in == null)
return;
try {
in.close();//in 就是我们传入的 new FileReader(filePath), 关闭了. } finally {
in = null;
cb = null;
}
}
}
*/

        bufferedReader.close();
    }
}
```

write:

```
public class BufferedWriter_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\ok.txt";
//创建 BufferedWriter
//说明:
//1. new FileWriter(filePath, true) 表示以追加的方式写入
//2. new FileWriter(filePath) , 表示以覆盖的方式写入
      
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(filePath));
        bufferedWriter.write("hello, 韩顺平教育!");
        bufferedWriter.newLine();//插入一个和系统相关的换行
        bufferedWriter.write("hello2, 韩顺平教育!");
        bufferedWriter.newLine();
        bufferedWriter.write("hello3, 韩顺平教育!");
        bufferedWriter.newLine();
//说明：关闭外层流即可 ， 传入的 new FileWriter(filePath) ,会在底层关闭
        bufferedWriter.close();
    }
}
```

###  处理流-BufferedInputStream 和 BufferedOutputStream

BufferedInputStream是字节流在创建BufferedInputStream时，会创建一个内部缓冲区数组.

BufferedOutputStream是字节流，实现缓冲的输出流，可以将多个字节写入底层输出流中，而不必对每次字节写入调用底层系统

```
/**
 * 演示使用 BufferedOutputStream 和 BufferedInputStream 使用
 * 使用他们，可以完成二进制文件拷贝. * 思考：字节流可以操作二进制文件，可以操作文本文件吗？当然可以
 */
public class BufferedCopy02 {
    public static void main(String[] args) {
// String srcFilePath = "e:\\Koala.jpg";
// String destFilePath = "e:\\hsp.jpg";
// String srcFilePath = "e:\\0245_韩顺平零基础学 Java_引出 this.avi";
// String destFilePath = "e:\\hsp.avi";
        String srcFilePath = "e:\\a.java";
        String destFilePath = "e:\\a3.java";
//创建 BufferedOutputStream 对象 BufferedInputStream 对象
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
//因为 FileInputStream 是 InputStream 子类
            bis = new BufferedInputStream(new FileInputStream(srcFilePath));
        
                    bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
//循环的读取文件，并写入到 destFilePath
            byte[] buff = new byte[1024];
            int readLen = 0;
//当返回 -1 时，就表示文件读取完毕
            while ((readLen = bis.read(buff)) != -1) {
                bos.write(buff, 0, readLen);
            }
            System.out.println("文件拷贝完毕~~~");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
//关闭流 , 关闭外层的处理流即可，底层会去关闭节点流
            try {
                if(bis != null) {
                    bis.close();
                }
                if(bos != null) {
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
          
            }
        }
    }
}
```

###  对象流-ObjectInputStream 和 ObjectOutputStream（保留值和数据类型）

➢看一个需求
1.将int num = 100这个int数据保存到文件中，注意不是100数字，而是int 100, 并且，能够从文件中直接恢复int 100
2.将Dog dog = new Dog(“小黄”，3)这个dog对象保存到文件中，并且能够从文件恢复.
3.上面的要求， 就是能够将基本数据类型或者对象进行序列化和反序列化操作
➢ **序列化和反序列化**
1.序列化就是在保存数据时， 保存数据的值和数据类型
2.反序列化就是在恢复数据时， 恢复数据的值和数据类型
3.**需要让某个对象支持序列化机制，则必须让其类是可序列化的**，为了让某个类是可序列化的，**该类必须实现如下两个接口之一**:
-Serializable /这是一个标记接口，没有方法
➢Externalizable //该接口有方法需要实现，因此我们一般实现上面的Serializable接口

注意事项和细节说明
1**)读写顺序要一致**
2)**要求序列化或反序列化对象,需要实现Serializable**
3)序列化的类中建议添加SerialVersionUID,为了提高版本的兼容性：private static final Long serialVersionUID =1L
4)序列化对象时，默认将里面所有属性都进行序列化，但除了static或transient修饰的成员
5)序列化对象时，要求里面属性的类型也需要实现序列化接口
6)序列化具备可继承性，也就是如果某类已经实现了序列化，则它的所有子类也已经默认实现了序列化

```
public class Object_ {
    public static void main(String[] args) throws Exception {
//        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("d:\\t.dat"));
//        oos.writeInt(123);
//        oos.writeObject(new Dog("小黄",12));
//        oos.close();
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("d:\\t.dat"));
        System.out.println(ois.readInt());
        Object dog = ois.readObject();
        System.out.println(dog.getClass()+"===="+dog);
        ois.close();

    }
}


class Dog implements Serializable {
    private String name;
    private int age;
    private static final Long serialVersionUID =1L
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

```

###  标准输入输出流

​																								类型														默认设备
System.in标准输入													InputStream														键盘
System.out标准输出												PrintStream														显示器

###  打印流-PrintStream 和 PrintWriter

打印流只有输出流，没有输入流

```
package com.hspedu.printstream;

import java.io.IOException;
import java.io.PrintStream;

/**
 * @author 韩顺平
 * @version 1.0
 * 演示PrintStream （字节打印流/输出流）
 */
public class PrintStream_ {
    public static void main(String[] args) throws IOException {

        PrintStream out = System.out;
        //在默认情况下，PrintStream 输出数据的位置是 标准输出，即显示器
        /*
             public void print(String s) {
                if (s == null) {
                    s = "null";
                }
                write(s);
            }

         */
        out.print("john, hello");
        //因为print底层使用的是write , 所以我们可以直接调用write进行打印/输出
        out.write("韩顺平,你好".getBytes());
        out.close();

        //我们可以去修改打印流输出的位置/设备
        //1. 输出修改成到 "e:\\f1.txt"
        //2. "hello, 韩顺平教育~" 就会输出到 e:\f1.txt
        //3. public static void setOut(PrintStream out) {
        //        checkIO();
        //        setOut0(out); // native 方法，修改了out
        //   }
        System.setOut(new PrintStream("e:\\f1.txt"));
        System.out.println("hello, 韩顺平教育~");


    }
}

```



###  转换流-InputStreamReader 和 OutputStreamWriter(编码乱码问题)

1. InputStreamReader:Reader的子类，可以将InputStream(字节流)**包装成(转换)Reader(字符流)**
2. OutputStreamWriter:Writer的子类，实现将OutputStream(字节流)**包装成Writer(字符流)**
3. 当**处理纯文本数据**时，如果使用字符流效率更高，并且可以有效解决中文问题，所以建议将字节流转换成字符流
4. 可以在使用时**指定编码格式**(比如utf-8, gbk，gb2312, IS08859-1等)

```
public class InputStreamReader_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\a.txt";
//解读
//1. 把 FileInputStream 转成 InputStreamReader
       
//2. 指定编码 gbk
//InputStreamReader isr = new InputStreamReader(new FileInputStream(filePath), "gbk");
//3. 把 InputStreamReader 传入 BufferedReader
//BufferedReader br = new BufferedReader(isr);
//将 2 和 3 合在一起
        BufferedReader br = new BufferedReader(new InputStreamReader(
                new FileInputStream(filePath), "gbk"));
//4. 读取
        String s = br.readLine();
        System.out.println("读取内容=" + s);
//5. 关闭外层流
        br.close();
    }
}


编程将字节流FileOutputStream包装成(转换成)字符流OutputStreamWriter,
对文件进行写入(按照gbk格式，可以指定其他，比如utf-8)

// 1.创建流对象
OutputStreamWriter osw =
new OutputStreamWriter(new FileOutputStream("d:\\a.txt"), "gbk");

// 2.写入
osw.write("hello,韩顺平教育~");
// 3.关闭
osw.close();
System.out.println("保存成功~")
```

###  Properties 类（配置文件）

1)专门用于读写配置文件的集合类
配置文件的格式:
键=值
键=值
2)注意:**键值对不需要有空格，值不需要用引号一 起来。默认类型是String**
3) Properties的常见方法
	load:加载配置文件的键值对到Properties对象
	list:将数据显示到指定设备
	getProperty(key):根据键获取值
	setProperty(key,value):设置键值对到Properties对象
	store:将Properties中的键值对存储到配置文件在idea中，保存信息到配置文件，如果含有中文，会存储为unicode码

```
public class Properties02 {
	public static void main(String[] args) throws IOException {
		//使用 Properties 类来读取 mysql.properties 文件
		//1. 创建 Properties 对象
		Properties properties = new Properties();
		//2. 加载指定配置文件
		properties.load(new FileReader("src\\mysql.properties"));
		//3. 把 k-v 显示控制台
		properties.list(System.out);
		//4. 根据 key 获取对应的值
		String user = properties.getProperty("user");
		String pwd = properties.getProperty("pwd");
		System.out.println("用户名=" + user);
		System.out.println("密码是=" + pwd);
	}
}






public class Properties03 {
    public static void main(String[] args) throws IOException {
//使用 Properties 类来创建 配置文件, 修改配置文件内容
                Properties properties = new Properties();
        //创建
        //1.如果该文件没有 key 就是创建
        //2.如果该文件有 key ,就是修改
        
        /*
        Properties 父类是 Hashtable ， 底层就是 Hashtable 核心方法
        public synchronized V put(K key, V value) {
        // Make sure the value is not null
        if (value == null) {
        throw new NullPointerException();
        }
        // Makes sure the key is not already in the hashtable. Entry<?,?> tab[] = table;
        
        int hash = key.hashCode();
        int index = (hash & 0x7FFFFFFF) % tab.length;
        @SuppressWarnings("unchecked")
        Entry<K,V> entry = (Entry<K,V>)tab[index];
        for(; entry != null ; entry = entry.next) {
        if ((entry.hash == hash) && entry.key.equals(key)) {
        V old = entry.value;
        entry.value = value;//如果 key 存在，就替换
        return old;
        }
        }
        addEntry(hash, key, value, index);//如果是新 k, 就 addEntry
        return null;
        }
        */
        properties.setProperty("charset", "utf8");
        properties.setProperty("user", "汤姆");//注意保存时，是中文的 unicode 码值
        properties.setProperty("pwd", "888888");
//将 k-v 存储文件中即可
        properties.store(new FileOutputStream("src\\mysql2.properties"), null);
        System.out.println("保存配置文件成功~");
    }
  
}
```

# socket

1.套接字(Socket)开发网络应用程序被广泛采用，以至于成为事实上的标准。
2.通信的两端都要有Socket,是两台机器间通信的端点
3.网络通信其实就是Socket间的通信。

4.Socket允许程序把网络连接当成一 个流，数据在两个Socket间通过IO传输。
5.一般主动发起通信的应用程序属客户端，等待通信请求的为服务端



​	TCP协议: 传输控制协议
   1.使用TCP协议前，须先建立TCP连接，形成传输数据通道
   2.传输前，采用"三次握手"方式，是**可靠的**

3. TCP协议进行通信的两个应用进程: **客户端、服务端**

4. 在连接中可进行大数据量的传输

5. 传输完毕，**需释放已建立的连接，效率低**

  

  UDP协议:用户数据协议

  1将数据、源、目的封装成数据包，**不需要建立连接**
  2.每个**数据报的大小限制在64K内，不适合传输大量数据**
  3.因无需连接，故是**不可靠的**
  4.发送数据结束时无需释放资源(因为不是面向连接的)，**速度快**


**InetAddress相关方法**

1.获取本机InetAddress对象getLocalHost
2.根据指定主机名/域名获取ip地址对象getByName
3.获取InetAddress对象的主机名getHostName
4.获取InetAddress对象的地址getHostAddress

```
public class ip_ {
    public static void main(String[] args) throws UnknownHostException {
        //获取本机 InetAddress 对象 getLocalHost
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost);
//根据指定主机名/域名获取 ip 地址对象 getByName
        InetAddress host2 = InetAddress.getByName("拂尘");
        System.out.println(host2);
        InetAddress host3 = InetAddress.getByName("www.hsp.com");
        System.out.println(host3);
//获取 InetAddress 对象的主机名 getHostName
        String host3Name = host3.getHostName();
        System.out.println(host3Name);
//获取 InetAddress 对象的地址 getHostAddress
        String host3Address = host3.getHostAddress();
        System.out.println(host3Address);
    }
}

```

### TCP 网络通信编程

1.基于客户端一 服务端的网络通信
2.底层使用的是TCP/IP协议
3.应用场景举例:客户端发送数据，服务端接受并显示控制台
4.基于Socket的TCP编程

```

字节流
1. 编写一个服务端， 和一个客户端
2.服务器端在9999端口监听
3.客户端连接到服务端，发送"hello, server" ,并接收服务器端回发的
"hello,client",再退出
4. 服务器端接收到 客户端发送的信息，输出，并发送"hello, client",再退出


服务器端
public class SocketTCP01Server {
    public static void main(String[] args) throws IOException {
        //思路
//1. 在本机 的 9999 端口监听, 等待连接
// 细节: 要求在本机没有其它服务在监听 9999
// 细节：这个 ServerSocket 可以通过 accept() 返回多个 Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在 9999 端口监听，等待连接..");
//2. 当没有客户端连接 9999 端口时，程序会 阻塞, 等待连接
// 如果有客户端连接，则会返回 Socket 对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务端 socket =" + socket.getClass());
//
//3. 通过 socket.getInputStream() 读取客户端写入到数据通道的数据, 显示
        InputStream inputStream = socket.getInputStream();
//4. IO 读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf, 0, readLen));//根据读取到的实际长度，显示内容. }
//5. 获取 socket 相关联的输出流
            OutputStream outputStream = socket.getOutputStream();
            outputStream.write("hello, client".getBytes());
// 设置结束标记
            socket.shutdownOutput();

//6.关闭流和 socket
            outputStream.close();
            inputStream.close();
            socket.close();
            serverSocket.close();//关闭
        }
    }
}


客户端
public class SocketTCP01Client {
    public static void main(String[] args) throws IOException {
//思路
//1. 连接服务端 (ip , 端口）
//解读: 连接本机的 9999 端口, 如果连接成功，返回 Socket 对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket 返回=" + socket.getClass());
//2. 连接上后，生成 Socket, 通过 socket.getOutputStream()
// 得到 和 socket 对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
//3. 通过输出流，写入数据到 数据通道
        outputStream.write("hello, server".getBytes());
        socket.shutdownOutput();
//4. 获取和 socket 关联的输入流. 读取数据(字节)，并显示
        InputStream inputStream = socket.getInputStream();
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf, 0, readLen));
        }
//5. 关闭流对象和 socket, 必须关闭
        inputStream.close();
        outputStream.close();
        socket.close();
        System.out.println("客户端退出.....");

    }
}

```

```
字符流
1.编写个服务端，和个客户端
2.服务端在9999端口监听
3.客户端连接到服务端，发送"hello, server"并接收服务端回发的" hello,client",再退
出
4.服务端接收到客户端发送的信息，输出，井发送"hello, client",再退出

服务端
public class SocketTCP03Server {
    public static void main(String[] args) throws IOException {
//思路
//1. 在本机 的 9999 端口监听, 等待连接
// 细节: 要求在本机没有其它服务在监听 9999

// 细节：这个 ServerSocket 可以通过 accept() 返回多个 Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在 9999 端口监听，等待连接..");
//2. 当没有客户端连接 9999 端口时，程序会 阻塞, 等待连接
// 如果有客户端连接，则会返回 Socket 对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务端 socket =" + socket.getClass());
//
//3. 通过 socket.getInputStream() 读取客户端写入到数据通道的数据, 显示
        InputStream inputStream = socket.getInputStream();
//4. IO 读取, 使用字符流, 老师使用 InputStreamReader 将 inputStream 转成字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);//输出
//5. 获取 socket 相关联的输出流
        OutputStream outputStream = socket.getOutputStream();
// 使用字符输出流的方式回复信息
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello client 字符流");
        bufferedWriter.newLine();// 插入一个换行符，表示回复内容的结束
        bufferedWriter.flush();//注意需要手动的 flush

//6.关闭流和 socket
        bufferedWriter.close();
        bufferedReader.close();
        socket.close();
        serverSocket.close();//关闭
    }
}


客户端
public class SocketTCP03Client {
    public static void main(String[] args) throws IOException {
//思路
//1. 连接服务端 (ip , 端口）
//解读: 连接本机的 9999 端口, 如果连接成功，返回 Socket 对象

        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket 返回=" + socket.getClass());
//2. 连接上后，生成 Socket, 通过 socket.getOutputStream()
// 得到 和 socket 对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
//3. 通过输出流，写入数据到 数据通道, 使用字符流
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello, server 字符流");
        bufferedWriter.newLine();//插入一个换行符，表示写入的内容结束, 注意，要求对方使用 readLine()!!!!
        bufferedWriter.flush();// 如果使用的字符流，需要手动刷新，否则数据不会写入数据通道
//4. 获取和 socket 关联的输入流. 读取数据(字符)，并显示
        InputStream inputStream = socket.getInputStream();
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);
//5. 关闭流对象和 socket, 必须关闭
        bufferedReader.close();//关闭外层流
        bufferedWriter.close();
        socket.close();
        System.out.println("客户端退出.....");
    }
}

```

```
发送图片视频
1.编写一个服务端，和一一个客户端
2. 服务器端在 8888端口监听
3.客户端连接到服务端，发送一张图片e:lqie.png
4. 服务器端接收到 客户端发送的图片，保存到src下，发送"收到图片"再退出
5.客户端接收到服务端发送的"收到图片"，再退出
6.该程序要求使用StreamUtils.java,我们直接使用

工具类
public class StreamUtils {
    /**
     * 功能：将输入流转换成byte[]
     * @param is
     * @return
     * @throws Exception
     */
    public static byte[] streamToByteArray(InputStream is) throws Exception {
        ByteArrayOutputStream bos = new ByteArrayOutputStream();//创建输出流对象
        byte[] b = new byte[1024];
        int len;
        while((len=is.read(b))!=-1){
            bos.write(b, 0, len);
        }
        byte[] array = bos.toByteArray();
        bos.close();
        return array;
    }
    /**
     * 功能：将InputStream转换成String
     * @param is
     * @return
     * @throws Exception
     */

    public static String streamToString(InputStream is) throws Exception{
        BufferedReader reader = new BufferedReader(new InputStreamReader(is));
        StringBuilder builder= new StringBuilder();
        String line;
        while((line=reader.readLine())!=null){ //当读取到 null时，就表示结束
            builder.append(line+"\r\n");
        }
        return builder.toString();

    }
}


服务端
public class TCPFileUploadServer {
    public static void main(String[] args) throws Exception {
        //1. 服务端在本机监听8888端口
        ServerSocket serverSocket = new ServerSocket(8888);
        System.out.println("服务端在8888端口监听....");
        //2. 等待连接
        Socket socket = serverSocket.accept();

        InputStream inputStream = socket.getInputStream();
        BufferedInputStream bis = new BufferedInputStream(inputStream);
        byte[] bytes = StreamUtils.streamToByteArray(bis);
        //4. 将得到 bytes 数组，写入到指定的路径，就得到一个文件了
        String destFilePath = "src/socket/高山流水copy.mp3";
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
        bos.write(bytes);
        bos.close();

        // 向客户端回复 "收到图片"
        // 通过socket 获取到输出流(字符)
        BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        writer.write("收到图片");
        writer.flush();//把内容刷新到数据通道
        socket.shutdownOutput();//设置写入结束标记

        //关闭其他资源
        writer.close();
        bis.close();
        socket.close();
        serverSocket.close();
    }
}


客户端
public class TCPFileUploadClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket(InetAddress.getLocalHost(),8888);
        //创建读取磁盘文件的输入流
        //String filePath = "e:\\qie.png";
        String filePath = "src/socket/高山流水.mp3";
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(filePath));
        //bytes 就是filePath对应的字节数组
        byte[] bytes = StreamUtils.streamToByteArray(bis);
        //通过socket获取到输出流, 将bytes数据发送给服务端
        BufferedOutputStream bos = new BufferedOutputStream(socket.getOutputStream());
        bos.write(bytes);//将文件对应的字节数组的内容，写入到数据通道
        bis.close();
        socket.shutdownOutput();//设置写入数据的结束标记

        //=====接收从服务端回复的消息=====

        InputStream inputStream = socket.getInputStream();
        //使用StreamUtils 的方法，直接将 inputStream 读取到的内容 转成字符串
        String s = StreamUtils.streamToString(inputStream);
        System.out.println(s);


        //关闭相关的流
        inputStream.close();
        bos.close();
        socket.close();

    }
}

```

### netstat指令

1. netstat -an可以查看当前主机网络情况，包括端口监听情况和网络连接情况
2. netstat -an more 可以分页显示
3.要求在dos控制台下执行win+r
说明:
(1) Listening表示某个端口在监听
(2)如果有一个外部程序(客户端)连接到该端口，就会显示一条连接信息

### UDP 网络通信编程

​	基本介绍
·   1.类DatagramSocket和DatagramPacket[数据包/数据报]实现了基于UDP协议网络程序。

2. UDP数据报通过数据报套接字DatagramSocket发送和接收，系统不保证UDP数据报-定能够安全送到目的地，也不能确定什么时候可以抵达。

3. DatagramPacket对象封装了UDP数据报，在数据报中包含了发送端的IP地址和端口号以及接收端的IP地址和端口号。

4. UDP协议中每个数据报都给出了完整的地址信息，因此无须建立发送方和接收方的连接

基本流程
1.核心的两个类/对象DatagramSocket与DatagramPacket
2.建立发送端，接收端(没有服务端和客户端概念)
3.发送数据前，建立数据包/报DatagramPacket对象
4.调用DatagramSocket的发送、接收方法
5.关闭DatagramSocket

```
接收方
public class UDPReceiverA {
    public static void main(String[] args) throws IOException {
        //1. 创建一个 DatagramSocket 对象，准备在9999接收数据
        DatagramSocket socket = new DatagramSocket(9999);
        //2. 构建一个 DatagramPacket 对象，准备接收数据
        //   在前面讲解UDP 协议时，老师说过一个数据包最大 64k
        byte[] buf = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buf, buf.length);
        //3. 调用 接收方法, 将通过网络传输的 DatagramPacket 对象
        //   填充到 packet对象
        //老师提示: 当有数据包发送到 本机的9999端口时，就会接收到数据
        //   如果没有数据包发送到 本机的9999端口, 就会阻塞等待.
        System.out.println("接收端A 等待接收数据..");
        socket.receive(packet);

        //4. 可以把packet 进行拆包，取出数据，并显示.
        int length = packet.getLength();//实际接收到的数据字节长度
        byte[] data = packet.getData();//接收到数据
        String s = new String(data, 0, length);
        System.out.println(s);


        //===回复信息给B端
        //将需要发送的数据，封装到 DatagramPacket对象
        data = "好的, 明天见".getBytes();
        //说明: 封装的 DatagramPacket对象 data 内容字节数组 , data.length , 主机(IP) , 端口
        packet =
                new DatagramPacket(data, data.length, InetAddress.getByName("192.168.92.1"), 9998);

        socket.send(packet);//发送

        //5. 关闭资源
        socket.close();
        System.out.println("A端退出...");

    }
}



发送方
public class UDPSenderB {
    public static void main(String[] args) throws IOException {

        //1.创建 DatagramSocket 对象，准备在9998端口 接收数据
        DatagramSocket socket = new DatagramSocket(9998);

        //2. 将需要发送的数据，封装到 DatagramPacket对象
        byte[] data = "hello 明天吃火锅~".getBytes(); //

        //说明: 封装的 DatagramPacket对象 data 内容字节数组 , data.length , 主机(IP) , 端口
        DatagramPacket packet =
                new DatagramPacket(data, data.length, InetAddress.getByName("192.168.92.1"), 9999);

        socket.send(packet);

        //3.=== 接收从A端回复的信息
        //(1)   构建一个 DatagramPacket 对象，准备接收数据
        //   在前面讲解UDP 协议时，老师说过一个数据包最大 64k
        byte[] buf = new byte[1024];
        packet = new DatagramPacket(buf, buf.length);
        //(2)    调用 接收方法, 将通过网络传输的 DatagramPacket 对象
        //   填充到 packet对象
        //老师提示: 当有数据包发送到 本机的9998端口时，就会接收到数据
        //   如果没有数据包发送到 本机的9998端口, 就会阻塞等待.
        socket.receive(packet);

        //(3)  可以把packet 进行拆包，取出数据，并显示.
        int length = packet.getLength();//实际接收到的数据字节长度
        data = packet.getData();//接收到数据
        String s = new String(data, 0, length);
        System.out.println(s);

        //关闭资源
        socket.close();
        System.out.println("B端退出");
    }
}


```

