# Interview

精心收录整理互联网笔试面试题，以及自己发布的文章，欢迎各位star！或者关注微信公众号【1024笔记】，免费获取海量学习资源

. 作者：新一、

. 简书：https://www.jianshu.com/u/b3263fc54bce

. 知乎：https://www.zhihu.com/people/qing-ni-chi-you-zi-96

. GitHub：https://github.com/JangYt?tab=repositories

. 博客地址：https://blog.csdn.net/qq_41153943

## 一、Java基础
# 笔试面试题集锦

### 1、&和&&的区别

&和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true 时，整个运算结果才为true，否则，只要有一方为false，则结果为false。
既然存在两个运算符，那么他们之前肯定还是有区别的。&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式，整个条件都为false。例如，

```cpp
	int i=0;
	string g="adb";
	if(i!=0 && g.length==0){
		.....
	}
```

```cpp
	int i=0;
	string g="adb";
	if(i!=0 & g.length==0){
		.....
	}
```

因为i=0,所以表达式i!=0返回的是false，那么&&后面的表达式便不再执行。整个if条件都为false，如果将&&换成&，虽然i!=0返回的是false，但是表达式g.length==0还是要执行，整个if条件也返回的是false。
	
&还可以用作位运算符，当&操作符两边的表达式不是boolean类型时，&表示按位与操作，我们通常 使用0x0f来与一个整数进行&运算，来获取该整数的低4个bit位，例如，0x31 & 0x0f的结果为0x01。

### 2、short s1= 1; s1 = s1+1 和short s1 = 1; s1 += 1；有什么区别

对于short s1= 1; s1 = s1+1因为1是int类型，而等号左边的s1是short类型，由于s1+1运算时会自动提升表达式的类型，所以运算的结果是int型，再赋值给 short类型s1时，编译器将报告需要强制转换类型的错误，所以需要进行强转。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509105222272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509105311917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
对于short s1= 1; s1 += 1;在java中+=的作用包含两个部分，除了基本的加法运算功能之外，还可以隐形转换改变结果的类型，将计算结果的类型转换为“+=”符号左边的对象的类型。所以可以正确编译
![img](https://img-blog.csdnimg.cn/20200509105757495.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

### 3、使用final关键字修饰一个变量时,是引用不能变,还是引用的对象不能变

使用final关键字修饰一个变量时，是指引用变量不能变，但是引用变量所指向的对象中的内容还是可以改变的。

```cpp
public class Demo2 {
	//声明一个final关键字修饰的字符串
	public static final StringBuffer sb = new StringBuffer("abc");
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//sb指向新的引用对象
		sb = new StringBuffer("def");
	}

}
```

上述代码报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509143729619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

```cpp
public class Demo2 {
	//声明一个final关键字修饰的字符串
	public static final StringBuffer sb = new StringBuffer("abc");
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//sb指向新的引用对象
		//sb = new StringBuffer("def");
		System.out.println(sb);
		//修改sb引用对象的值
		sb.append("def");
		System.out.println(sb);
	}
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509144014812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
其实这个还是跟final关键字的使用有关。final关键字除了可以修饰类和方法以外，final关键字还可以用来修饰变量，其中包括基本数据类型的值变量和引用变量。
final修饰的变量其实就相当于定义了一个常量，无法被修改的变量。
如果final修饰的是一个基本数据类型的值变量，那么这个变量的值就定了，不能变了，比如final int i=10；那么就是在栈内存中对i变量赋值为10，这个值是不能改变的了；
而如果final关键字修饰的是一个引用变量，那么该变量在栈内存中存的是一个内存地址，该地址就不能变了，但是该内存地址所指向的那个对象还是可以变的。
如果拿去买房为例的话，对于基本数据类型的变量，房格就好比是被final修饰的基本数据类型的变量，一旦定死了就不能修改了（虽然现实中可以修改的）；而对于引用变量，这个地皮（栈内存地址）一旦规划作为住宅用地了，那么便不可以再做其他用途（引用不能指向其他的对象），但是在这个地址上盖什么样的房子，多少房子是可以改变的（引用对象的内容可以改变）

使用final关键字修饰一个变量时，是指引用变量不能变，但是引用变量所指向的对象中的内容还是可以改变的。

```cpp
public class Demo2 {
	//声明一个final关键字修饰的字符串
	public static final StringBuffer sb = new StringBuffer("abc");
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//sb指向新的引用对象
		sb = new StringBuffer("def");
	}

}
```

上述代码报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509143729619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

```cpp
public class Demo2 {
	//声明一个final关键字修饰的字符串
	public static final StringBuffer sb = new StringBuffer("abc");
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//sb指向新的引用对象
		//sb = new StringBuffer("def");
		System.out.println(sb);
		//修改sb引用对象的值
		sb.append("def");
		System.out.println(sb);
	}
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200509144014812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
其实这个还是跟final关键字的使用有关。final关键字除了可以修饰类和方法以外，final关键字还可以用来修饰变量，其中包括基本数据类型的值变量和引用变量。
final修饰的变量其实就相当于定义了一个常量，无法被修改的变量。
如果final修饰的是一个基本数据类型的值变量，那么这个变量的值就定了，不能变了，比如final int i=10；那么就是在栈内存中对i变量赋值为10，这个值是不能改变的了；
而如果final关键字修饰的是一个引用变量，那么该变量在栈内存中存的是一个内存地址，该地址就不能变了，但是该内存地址所指向的那个对象还是可以变的。
如果拿去买房为例的话，对于基本数据类型的变量，房格就好比是被final修饰的基本数据类型的变量，一旦定死了就不能修改了（虽然现实中可以修改的）；而对于引用变量，这个地皮（栈内存地址）一旦规划作为住宅用地了，那么便不可以再做其他用途（引用不能指向其他的对象），但是在这个地址上盖什么样的房子，多少房子是可以改变的（引用对象的内容可以改变）

![](https://img-blog.csdnimg.cn/20200509151033193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

### 4、Integer与int的区别

int是java提供的8种基本数据类型之一。Java为每个基本数据库类型提供了封装类，而Integer就是java为int提供
的封装类。int的默认值为0，而Integer的默认值为null，即Integer可以区分出未赋值和值为0的区别，
int则无法表达出未赋值的情况。
例如：要想表达出没有工资和工资为0的区别，则只能使用Integer。在JSP的开发中，Integer的默认为null，所以用el表达式在文本框中显示时，值为空白字符串，而int默认的默认值为0，所以用el表达式在文本框中显示时，结果为0，所以，int不适合作为web层的表单数据的类型。
在Hibernate中，如果将OID定义为Integer类型，那么Hibernate就可以根据其值是否为null而判断一
个对象是否是临时的，如果将OID定义为了int类型，还需要在hbm映射文件中设置其unsaved-value属
性为0。
另外，Integer提供了多个与整数相关的操作方法，例如，将一个字符串转换成整数，Integer中还定
义了表示整数的最大值和最小值的常量。

### 5、Overload和Override的区别？Overload的方法是否可以改变返回值的类型?

#### **5.1、overload**

Overload的中文意思是重载，它表示同一个类中可以有多个名称相同的方法，但这些方法的参数列表各不相同，即参数的个数或类型至少有一个不同，但返回值和方法属性必须相同。在调用的时候，VM就会根据不同的参数列表，来执行对应的合适的方法。
比如：

```cpp
public class Demo4 {

	public static void main(String[] args) {
		Demo4 demo4 = new Demo4();
		demo4.say();
		demo4.say("你好啊");
		demo4.say("张三","你在干嘛");
		demo4.say(4, "李四");
		demo4.say("李四",5);
	}
	
	public void say() {
		System.out.println("Hello world");
	}
	public void say(String wordString) {
		System.out.println("Hello "+ wordString);
	}
	
	public void say(String name,String word) {
		System.out.println(name+"说："+word);
	}
	
	public void say(int word,String name) {
		System.out.println(name+"说："+word);
	}
	
	public void say(String name,int word) {
		System.out.println(name+"说："+word);
	}
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512101442239.png)
上面代码中的方法就是重载。
我看有些文章里面写到对于重载的返回值类型也可以是不同的，还有的说是可以相同，也可以不同。那么我们先看代码：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512101738391.png)
这里报错完全一样的方法在Demo4中，所以可以看出，参数列表相同，仅仅靠返回值不同，是不能实现重载的。在java中明确声明在一个类中，两个方法的方法名和参数列表一样，返回值类型不同这是不允许的。
有的说在参数列表不同的情况下（已经是重载了），返回值类型可以是相同，可以是不同的。再来看代码：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200512102223457.png)
的确上述的代码，并没有报错。但是我们想想，上面的两个say方法，一个返回的是说的内容（返回值类型是string），一个返回的是说了几句话(返回值类型是int)，这两个方法的功能是不一样的。所以他们已经是两个不一样的方法了，只是方法名一样，但是并不是方法的重载（我也不能说我说的都对，只是个人觉得的，目前也没有在一本权威的书本上面看到这类的答案，所以如果有小伙伴觉得不对，或者看到了权威的说法，欢迎指正）。

#### 5.2、Override

Override重写(覆盖)，表示子类中的方法可以与父类中的某个方法的名称和参数完全相同，通过子类创建的实 例对象调用这个方法时，将调用子类中的定义方法，这相当于把父类中定义的那个完全相同的方法给覆盖了，
这也正是面向对象编程的中多态性的一种表现。子类覆盖父类的方法时，只能比父类抛出更少的异常，或者是抛出父类抛出的异常的子异常，因为子类可以解决父类的一些问题，所以不能比父类有更多的问题。
子类方法的访问权限只能比父类的更大，不能更小。如果父类的方法是private类型，那么子类并不能对父类的private关键字修饰的方法进行覆盖，相当于子类中增加了一个全新的方法。因为我们知道provite关键字修饰的变量或者方法都是只能本类可以访问使用，其他的任何的都不可以。所以
当一个子类继承了父类，那么这个子类其实是拥有父类所有的成员属性和方法，包括父类里有private属性的变量和方法，子类也是继承的，但是子类并不能使用，也就是说，它继承了，但是并没有使用权，
打个比方就好比，你爸的钱虽然都是你的（都可以继承），但是你只能使用你爸放在家里的钱（public修饰的变量方法），你爸存在银行卡里面的钱你并不能使用（private修饰的），但你是可以继承的。

```cpp
public class Demo4 {
	public String say(String wordString) {
		return wordString;
	}
	private String say(String wordString,int i) {
		return wordString;
	}
	
	public int say(int wordString) {
		return wordString;
	}
	}
```

```cpp
package Demo1;

public class Demo5 extends Demo4 {

	public static void main(String[] args) {
		Demo5 demo5 = new Demo5();
		String s1 = demo5.say("你好");
		int i = demo5.say(23);
		String s2 = demo5.say("你好",23);
		System.out.println(s1);
		System.out.println(i);
		System.out.println(s2);
	}
	
	public String say(String wordString) {
		return wordString;
	}
	
	private String say(String wordString,int i) {
		return wordString;
	}
	
	public int say(int wordString) {
		return wordString;
	}

}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051210532382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

#### 5.3、overwrite

overwrite重写的意思：java官方文档没有该词的出现，所以java中就没有它的存在，但是也有人把overwrite解释为override。
但是在C++中将Override和overwrite进行了区分。
Override：覆盖
是指派生类函数覆盖基类函数，特征是：
（1）不同的范围（分别位于派生类与基类）；
（2）函数名字相同；
（3）参数相同；
（4）基类函数必须有virtual 关键字。
Overwrite：重写
是指派生类的函数屏蔽了与其同名的基类函数，规则如下：
（1）如果派生类的函数与基类的函数同名，但是参数不同。此时，不论有无virtual关键字，基类的函数将被隐藏。
（2）如果派生类的函数与基类的函数同名，并且参数也相同，但是基类函数没有virtual关键字。此时，基类的函数被隐藏。
所以如果是java的话根本不需要考虑overwrite，记住overload和override即可。

#### 5.4、总结

override：
    1、覆盖的方法的标志必须要和被覆盖的方法的标志完全匹配，才能达到覆盖的效果；
	2、覆盖的方法的返回值必须和被覆盖的方法的返回一致；
    3、覆盖的方法所抛出的异常必须和被覆盖方法的所抛出的异常一致，或者是其子类；    
	4、如果某一方法在父类中是访问权限是priavte，那么就不能在子类对其进行覆盖， 否则在其子类中只是新定义了一个方法，并没有对其进行覆盖。 
	
Overload：
    1、在使用重载时只能通过不同的参数样式。例如，不同的参数类型，不同的参数个数，不同的参数顺序（注意这里同一方法内的几个参数类型必须不一样，例如可以是fun(int,ﬂoat)，但是不能为 fun(int,int)）；    
	2、不能通过访问权限、返回类型、抛出的异常进行重载；    
	3、方法的异常类型和数目不会对重载造成影响；


参考：https://stackoverflow.com/questions/837864/java-overloading-vs-overriding

### 6、Java中实现多态的机制是什么？

靠的是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，而程序调用的方法在运行
期才动态绑定，就是引用变量所指向的具体实例对象的方法，也就是内存里正在运行的那个对象的方
法，而不是引用变量的类型中定义的方法。

### 7、接口是否可继承接口?抽象类是否可实现(implements)接口?抽象类是否可继承具体类(concreteclass)?抽象类中是否可以有静态的main方法？

接口可以继承接口。抽象类可以实现(implements)接口，抽象类可以继承具体类。抽象类中可以有静
态的main方法。
备注：只要明白了接口和抽象类的本质和作用，这些问题都很好回答，你想想，如果你是java语言的
设计者，你是否会提供这样的支持，如果不提供的话，有什么理由吗？如果你没有道理不提供，那答案
就是肯定的了。
只要记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。

### 8、abstract的method是否可同时是static,是否可同时是native，是否可同时是synchronized?

abstract的method不可以是static的，因为抽象的方法是要被子类实现的，而static与子类扯不上关
系！
native方法表示该方法要用另外一种依赖平台的编程语言实现的，不存在着被子类实现的问题，所以，
它也不能是抽象的，不能与abstract混用。例如，FileOutputSteam类要硬件打交道，底层的实现用的
是操作系统相关的api实现；例如，在windows用c语言实现的，所以，查看jdk的源代码，可以发现
FileOutputStream的open方法的定义如下：
`` private native void open(Stringname) throwsFileNotFoundException; ``
如果我们要用java调用别人写的c语言函数，我们是无法直接调用的，我们需要按照java的要求写一个
c语言的函数，又我们的这个c语言函数去调用别人的c语言函数。由于我们的c语言函数是按java的要求
来写的，我们这个c语言函数就可以与java对接上，java那边的对接方式就是定义出与我们这个c函数相
对应的方法，java中对应的方法不需要写具体的代码，但需要在前面声明native。
关于synchronized与abstract合用的问题，我觉得也不行，因为在我几年的学习和开发中，从来没见
到过这种情况，并且我觉得synchronized应该是作用在一个具体的方法上才有意义。而且，方法上的
synchronized同步所使用的同步锁对象是this，而抽象方法上无法确定this是什么。

### 9、内部类可以引用它的包含类的成员吗？

可以。如果不是静态内部类，那没有什么限制！
如果你把静态嵌套类当作内部类的一种特例，那在这种情况下不可以访问外部类的普通成员变量，而
只能访问外部类中的静态成员，例如，下面的代码：

`` class Outer
{
static int x;
static class Inner
 {
    voidtest()
   {
       syso(x);
   }
 }
}
``

### 10、String s = "Hello";s = s + "world!";这两行代码执行后，原始

的String对象中的内容到底变了没有？

没有。因为String被设计成不可变(immutable)类，所以它的所有对象都是不可变对象。在这段代码
中，s原先指向一个String对象，内容是 "Hello"，然后我们对s进行了+操作，那么s所指向的那个对象是
否发生了改变呢？答案是没有。这时，s不指向原来那个对象了，而指向了另一个 String对象，内容
为"Hello world!"，原来那个对象还存在于内存之中，只是s这个引用变量不再指向它了。
通过上面的说明，我们很容易导出另一个结论，如果经常对字符串进行各种各样的修改，或者说，不
可预见的修改，那么使用String来代表字符串的话会引起很大的内存开销。因为String对象建立之后不
能再改变，所以对于每一个不同的字符串，都需要一个String对象来表示。这时，应该考虑使用
StringBuffer类，它允许修改，而不是每个不同的字符串都要生成一个新的对象。并且，这两种类的对
象转换十分容易。
同时，我们还可以知道，如果要使用内容相同的字符串，不必每次都new一个String。例如我们要在
构造器中对一个名叫s的String引用变量进行初始化，把它设置为初始值，应当这样做：

`` public class Demo {
private String s;
...
public Demo {
s = "Initial Value";
}
...
}``

而非
`` s = new String("Initial Value");``
后者每次都会调用构造器，生成新对象，性能低下且内存开销大，并且没有意义，因为String对象不可
改变，所以对于内容相同的字符串，只要一个String对象来表示就可以了。也就说，多次调用上面的构
造器创建多个对象，他们的 String类型属性s都指向同一个对象。
上面的结论还基于这样一个事实：对于字符串常量，如果内容相同，Java认为它们代表同一个String对
象。而用关键字new调用构造器，总是会创建一个新的对象，无论内容是否相同。
至于为什么要把String类设计成不可变类，是它的用途决定的。其实不只String，很多Java标准类库中
的类都是不可变的。在开发一个系统的时候，我们有时候也需要设计不可变类，来传递一组相关的值，
这也是面向对象思想的体现。不可变类有一些优点，比如因为它的对象是只读的，所以多线程并发访问
也不会有任何问题。当然也有一些缺点，比如每个不同的状态都要一个对象来代表，可能会造成性能上
的问题。所以Java标准类库还提供了一个可变版本，即StringBuffer。

### 11、ArrayList和Vector的区别

这两个类都实现了List接口（List接口继承了Collection接口），他们都是有序集合，即存储在这两个
集合中的元素的位置都是有顺序的，相当于一种动态的数组，我们以后可以按位置索引号取出某个元
素，并且其中的数据是允许重复的，这是与HashSet之类的集合的最大不同处，HashSet之类的集合不
可以按索引号去检索其中的元素，也不允许有重复的元素。
ArrayList与Vector的区别主要包括两个方面：.
（1）同步性：
Vector是线程安全的，也就是说是它的方法之间是线程同步的，而ArrayList是线程序不安全的，它的
方法之间是线程不同步的。如果只有一个线程会访问到集合，那最好是使用ArrayList，因为它不考虑线
程安全，效率会高些；如果有多个线程会访问到集合，那最好是使用Vector，因为不需要我们自己再去
考虑和编写线程安全的代码。
（2）数据增长：
ArrayList与Vector都有一个初始的容量大小，当存储进它们里面的元素的个数超过了容量时，就需要
增加ArrayList与Vector的存储空间，每次要增加存储空间时，不是只增加一个存储单元，而是增加多个
存储单元，每次增加的存储单元的个数在内存空间利用与程序效率之间要取得一定的平衡。Vector默认
增长为原来两倍，而ArrayList的增长策略在文档中没有明确规定（从源代码看到的是增长为原来的1.5
倍）。ArrayList与Vector都可以设置初始的空间大小，Vector还可以设置增长的空间大小，而ArrayList
没有提供设置增长空间的方法。
总结：即Vector增长原来的一倍，ArrayList增加原来的0.5倍。

### 12、HashMap和Hashtable的区别

HashMap是Hashtable的轻量级实现（非线程安全的实现），他们都完成了Map接口，主要区别在于
HashMap允许空（null）键值（key）,由于非线程安全，在只有一个线程访问的情况下，效率要高于
Hashtable。
HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。
HashMap把Hashtable的contains方法去掉了，改成containsvalue和containsKey。因为contains方法
容易让人引起误解。
Hashtable继承自Dictionary类，而HashMap是Java1.2引进的Map interface的一个实现。
最大的不同是，Hashtable的方法是Synchronize的，而HashMap不是，在多个线程访问Hashtable
时，不需要自己为它的方法实现同步，而HashMap就必须为之提供同步。
就HashMap与HashTable主要从三方面来说。
一.历史原因:Hashtable是基于陈旧的Dictionary类的，HashMap是Java 1.2引进的Map接口的一个实
现
二.同步性:Hashtable是线程安全的，也就是说是同步的，而HashMap是线程序不安全的，不是同步
的
三.值：只有HashMap可以让你将空值作为一个表的条目的key或value。

### 13、List和 Map区别?

一个是存储单列数据的集合，另一个是存储键和值这样的双列数据的集合，List中存储的数据是有顺
序，并且允许重复；Map中存储的数据是没有顺序的，其键是不能重复的，它的值是可以有重复的。

### 14、List、Map、Set三个接口，存取元素时，各有什么特点？

首先，List与Set具有相似性，它们都是单列元素的集合，所以，它们有一个共同的父接口，叫
Collection。Set里面不允许有重复的元素，即不能有两个相等（注意，不是仅仅是相同）的对象，即假
设Set集合中有了一个A对象，现在我要向Set集合再存入一个B对象，但B对象与A对象equals相等，则B
对象存储不进去，所以，Set集合的add方法有一个boolean的返回值，当集合中没有某个元素，此时
add方法可成功加入该元素时，则返回true，当集合含有与某个元素equals相等的元素时，此时add方
法无法加入该元素，返回结果为false。Set取元素时，不能细说要取第几个，只能以Iterator接口取得所
有的元素，再逐一遍历各个元素。
List表示有先后顺序的集合，注意，不是那种按年龄、按大小、按价格之类的排序。当我们多次调用
add(Obje)方法时，每次加入的对象就像火车站买票有排队顺序一样，按先来后到的顺序排序。有时
候，也可以插队，即调用add(intindex,Obj e)方法，就可以指定当前对象在集合中的存放位置。一个对
象可以被反复存储进List中，每调用一次add方法，这个对象就被插入进集合中一次，其实，并不是把
这个对象本身存储进了集合中，而是在集合中用一个索引变量指向这个对象，当这个对象被add多次
时，即相当于集合中有多个索引指向了这个对象，如图x所示。List除了可以用Iterator接口取得所有的
元素，再逐一遍历各个元素之外，还可以调用get(index i)来明确说明取第几个。
Map与List和Set不同，它是双列的集合，其中有put方法，定义如下：put(obj key,obj value)，每次
存储时，要存储一对key/value，不能存储重复的key，这个重复的规则也是按equals比较相等。取则可
以根据key获得相应的value，即get(Object key)返回值为key所对应的value。另外，也可以获得所有的
key的结合，还可以获得所有的value的结合，还可以获得key和value组合成的Map.Entry对象的集合。
List以特定次序来持有元素，可有重复元素。Set无法拥有重复元素,内部排序。Map保存key-value值，
value可多值。

### 15、ArrayList、Vector、LinkedList的存储性能和特性

ArrayList和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元
素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快
而插入数据慢，Vector由于使用了synchronized方法（线程安全），通常性能上较ArrayList差。而
LinkedList使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历，索引就变慢了，但是插
入数据时只需要记录本项的前后项即可，所以插入速度较快。
LinkedList也是线程不安全的，LinkedList提供了一些方法，使得LinkedList可以被当作堆栈和队列来
使用。

### 16、jsp有哪些内置对象?作用分别是什么
1. request 用户端请求，此请求会包含来自GET/POST请求的参数; 
request表示HttpServletRequest对象。它包含了有关浏览器请求的信息，并且提供了几个用于获取cookie, header,和session数据的有用的方法。
2. response 网页传回用户端的回应;
  response表示HttpServletResponse对象，并提供了几个用于设置送回浏览器的响应的方法（如cookies,头信息等）
3. pageContext 网页的属性是在这里管理;
  pageContext表示一个javax.servlet.jsp.PageContext对象。它是用于方便存取各种范围的名字空间、servlet相关的对象的API，并且包装了通用的
4. out 用来传送回应的输出;
  out对象是javax.jsp.JspWriter的一个实例，并提供了几个方法使你能用于向浏览器回送输出结果。
  ##### servlet相关功能的方法。
5. session 与请求有关的会话期;
  session表示一个请求的javax.servlet.http.HttpSession对象。Session可以存贮用户的状态信息
6. application servlet 正在执行的内容;
  applicaton 表示一个javax.servle.ServletContext对象。这有助于查找有关servlet引擎和servlet环境的信息
7. config servlet的构架部件;
  config表示一个javax.servlet.ServletConfig对象。该对象用于存取servlet实例的初始化参数。
8. page JSP网页本身;
  page表示从该页面产生的一个servlet实例
9. exception 针对错误网页，未捕捉的例外;
  #### JSP共有以下6种基本动作
1. jsp:include：在页面被请求的时候引入一个文件。
2. jsp:useBean：寻找或者实例化一个JavaBean。
3. jsp:setProperty：设置JavaBean的属性。
4. jsp:getProperty：输出某个JavaBean的属性。
5. jsp:forward：把请求转到一个新的页面。
6. jsp:plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记

### 17、Servlet API中forward()与redirect()的区别
#### 概念
forward()与redirect()是servlet的两种主要的跳转方式。forward又叫转发，redirect叫做重定向。
转发过程:客户浏览器发送http请求——>web服务器接受此请求—>调用内部的一个方法在容器内部完成请求处理和转发动作一>将目标资源发送给客户端；
在这里，转发的路径必须是同一个web容器下的URL，其不能转向到其他的web路径上去，中间传递的 是自己的容器内的request。在客户浏览器路径栏显示的仍然是其
第一次访问的路径，也就是说客户是感觉不到服务器做了转发的。转发行为是浏览器只做了一次访问请求。

重定向过程:客户浏览器发送http请求一一>web服务器接受后发送302状态码响及对应新的location给客户浏览器——>客户端浏览器发现是302状态码，会自动再发送一
个新的http请求,请求url是新的location地址一一>服务器根据此请求寻找资源并发送给客户端浏览器在这里location可以重定向到任意URL，
既然是浏览器重新发出了请求，则就没有什么request传递的概念了。在客户浏览器地址栏显示的是其重定向的路径，客户可以观察到地址的变化的。重定向行为是浏览器
做了至少两次的访问请求的。
#### 区别：
1. 从地址栏显示来说：    
   forward是服务器内部的重定向，服务器请求资源,服务器直接访问目标地址的URL,把那个URL的响应内容读取过来,然后把这些内容再发给浏览器。浏览器根本不知道服务器发送的内容从哪里来的,所以它的地址栏还是原来的地址。    
   redirect是服务端根据逻辑,发送一个状态码,告诉浏览器重新去请求那个地址。所以地址栏显示的是新的URL。
   所以redirect等于客户端向服务器端发出两次request，同时也接受两次response;而forword只有一次请求。
2. 从数据共享来说    
   forward:forward方法只能在同一个Web应用程序内的资源之间转发请求，是服务器内部的一种操作。由于在整个定向的过程中用的是同一个request，因此forward会将request的信息带到被重定向的jsp或者servlet中使用，所以可以共享数据。
   redirect:redirect是服务器通知客户端,让客户端重新发起请求。redirect不仅可以重定向到当前应用程序的其他资源,还可以重定向到同一个站点上的其他应用程序中的资源,甚至是使用绝对URL重定向到其他站点的资源。所以不能共享数据。
3. 从应用场景来说    
   forward:一般适用于用户登陆的时候,根据角色转发到相应的模块。    
   redirect:一般适用于用户注销登陆时返回主页面和跳转到其它的网站等.  
4. 从效率来说    
   forward:效率高。   
   redirect:效率低. 
5. 从本质来说：
   forword转发是服务器上的行为，而redirect重定向是客户端的行为
