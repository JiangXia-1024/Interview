# Interview--Java基础

精心收录整理互联网笔试面试题，以及自己发布的文章，欢迎各位star！或者关注微信公众号【1024笔记】，免费获取海量学习资源

. 作者：江夏、

. 简书：https://www.jianshu.com/u/b3263fc54bce

. 知乎：https://www.zhihu.com/people/qing-ni-chi-you-zi-96

. GitHub：https://github.com/JiangXia-1024?tab=repositories

. 博客地址：https://blog.csdn.net/qq_41153943

## 一、Java基础
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
如果拿去买房为例的话，对于基本数据类型的变量，房子的价格就好比是被final修饰的基本数据类型的变量，一旦定死了就不能修改了（虽然现实中可以修改的）；而对于引用变量，这个地皮（栈内存地址）一旦规划作为住宅用地了，那么便不可以再做其他用途（引用不能指向其他的对象），但是在这个地址上盖什么样的房子，多少房子是可以改变的（引用对象的内容可以改变）

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

靠的是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，而程序调用的方法在运行期才动态绑定，就是引用变量所指向的具体实例对象的方法，也就是内存里正在运行的那个对象的方法，而不是引用变量的类型中定义的方法。

### 7、接口是否可继承接口?抽象类是否可实现(implements)接口?抽象类是否可继承具体类(concreteclass)?抽象类中是否可以有静态的main方法？

接口可以继承接口。抽象类可以实现(implements)接口，抽象类可以继承具体类。抽象类中可以有静态的main方法。备注：只要明白了接口和抽象类的本质和作用，这些问题都很好回答，你想想，如果你是java语言的设计者，你是否会提供这样的支持，如果不提供的话，有什么理由吗？如果你没有道理不提供，那答案就是肯定的了。只要记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。

### 8、abstract的method是否可同时是static,是否可同时是native，是否可同时是synchronized?

abstract的method不可以是static的，因为抽象的方法是要被子类实现的，而static与子类扯不上关系！native方法表示该方法要用另外一种依赖平台的编程语言实现的，不存在着被子类实现的问题，所以，它也不能是抽象的，不能与abstract混用。例如，FileOutputSteam类要硬件打交道，底层的实现用的是操作系统相关的api实现；例如，在windows用c语言实现的，所以，查看jdk的源代码，可以发现
FileOutputStream的open方法的定义如下：
`` private native void open(Stringname) throwsFileNotFoundException; ``
如果我们要用java调用别人写的c语言函数，我们是无法直接调用的，我们需要按照java的要求写一个c语言的函数，又我们的这个c语言函数去调用别人的c语言函数。由于我们的c语言函数是按java的要求来写的，我们这个c语言函数就可以与java对接上，java那边的对接方式就是定义出与我们这个c函数相对应的方法，java中对应的方法不需要写具体的代码，但需要在前面声明native。关于synchronized与abstract合用的问题，我觉得也不行，因为在我几年的学习和开发中，从来没见到过这种情况，并且我觉得synchronized应该是作用在一个具体的方法上才有意义。而且，方法上的synchronized同步所使用的同步锁对象是this，而抽象方法上无法确定this是什么。

### 9、内部类可以引用它的包含类的成员吗？

可以。如果不是静态内部类，那没有什么限制！
如果你把静态嵌套类当作内部类的一种特例，那在这种情况下不可以访问外部类的普通成员变量，而
只能访问外部类中的静态成员，例如，下面的代码：

```java
class Outer
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

```



### 10、String s = "Hello";s = s + "world!";这两行代码执行后，原始的String对象中的内容到底变了没有？

没有。因为String被设计成不可变(immutable)类，所以它的所有对象都是不可变对象。在这段代码中，s原先指向一个String对象，内容是 "Hello"，然后我们对s进行了+操作，那么s所指向的那个对象是否发生了改变呢？答案是没有。这时，s不指向原来那个对象了，而指向了另一个 String对象，内容为"Hello world!"，原来那个对象还存在于内存之中，只是s这个引用变量不再指向它了。通过上面的说明，我们很容易导出另一个结论，如果经常对字符串进行各种各样的修改，或者说，不可预见的修改，那么使用String来代表字符串的话会引起很大的内存开销。因为String对象建立之后不能再改变，所以对于每一个不同的字符串，都需要一个String对象来表示。这时，应该考虑使用StringBuffer类，它允许修改，而不是每个不同的字符串都要生成一个新的对象。并且，这两种类的对象转换十分容易。
同时，我们还可以知道，如果要使用内容相同的字符串，不必每次都new一个String。例如我们要在构造器中对一个名叫s的String引用变量进行初始化，把它设置为初始值，应当这样做：

```java
public class Demo {
private String s;
...
public Demo {
s = "Initial Value";
}
...
}

而非
s = new String("Initial Value");
```

后者每次都会调用构造器，生成新对象，性能低下且内存开销大，并且没有意义，因为String对象不可改变，所以对于内容相同的字符串，只要一个String对象来表示就可以了。也就说，多次调用上面的构造器创建多个对象，他们的 String类型属性s都指向同一个对象。上面的结论还基于这样一个事实：对于字符串常量，如果内容相同，Java认为它们代表同一个String对象。而用关键字new调用构造器，总是会创建一个新的对象，无论内容是否相同。至于为什么要把String类设计成不可变类，是它的用途决定的。其实不只String，很多Java标准类库中的类都是不可变的。在开发一个系统的时候，我们有时候也需要设计不可变类，来传递一组相关的值，这也是面向对象思想的体现。不可变类有一些优点，比如因为它的对象是只读的，所以多线程并发访问也不会有任何问题。当然也有一些缺点，比如每个不同的状态都要一个对象来代表，可能会造成性能上的问题。所以Java标准类库还提供了一个可变版本，即StringBuffer。

### 11、ArrayList和Vector的区别

这两个类都实现了List接口（List接口继承了Collection接口），他们都是有序集合，即存储在这两个集合中的元素的位置都是有顺序的，相当于一种动态的数组，我们以后可以按位置索引号取出某个元素，并且其中的数据是允许重复的，这是与HashSet之类的集合的最大不同处，HashSet之类的集合不可以按索引号去检索其中的元素，也不允许有重复的元素。ArrayList与Vector的区别主要包括两个方面：.
（1）同步性：
Vector是线程安全的，也就是说是它的方法之间是线程同步的，而ArrayList是线程序不安全的，它的方法之间是线程不同步的。如果只有一个线程会访问到集合，那最好是使用ArrayList，因为它不考虑线程安全，效率会高些；如果有多个线程会访问到集合，那最好是使用Vector，因为不需要我们自己再去考虑和编写线程安全的代码。
（2）数据增长：

ArrayList与Vector都有一个初始的容量大小，当存储进它们里面的元素的个数超过了容量时，就需要增加ArrayList与Vector的存储空间，每次要增加存储空间时，不是只增加一个存储单元，而是增加多个存储单元，每次增加的存储单元的个数在内存空间利用与程序效率之间要取得一定的平衡。Vector默认增长为原来两倍，而ArrayList的增长策略在文档中没有明确规定（从源代码看到的是增长为原来的1.5倍）。ArrayList与Vector都可以设置初始的空间大小，Vector还可以设置增长的空间大小，而ArrayList没有提供设置增长空间的方法。
总结：即Vector增长原来的一倍，ArrayList增加原来的0.5倍。

### 12、HashMap和Hashtable的区别

HashMap是Hashtable的轻量级实现（非线程安全的实现），他们都完成了Map接口，主要区别在于HashMap允许空（null）键值（key）,由于非线程安全，在只有一个线程访问的情况下，效率要高于Hashtable。HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。HashMap把Hashtable的contains方法去掉了，改成containsvalue和containsKey。因为contains方法容易让人引起误解。Hashtable继承自Dictionary类，而HashMap是Java1.2引进的Map interface的一个实现。最大的不同是，Hashtable的方法是Synchronize的，而HashMap不是，在多个线程访问Hashtable时，不需要自己为它的方法实现同步，而HashMap就必须为之提供同步。
就HashMap与HashTable的区别主要从三方面来说。
一.历史原因:Hashtable是基于陈旧的Dictionary类的，HashMap是Java 1.2引进的Map接口的一个实
现
二.同步性:Hashtable是线程安全的，也就是说是同步的，而HashMap是线程序不安全的，不是同步
的
三.值：只有HashMap可以让你将空值作为一个表的条目的key或value。

### 13、List和 Map区别?

一个是存储单列数据的集合，另一个是存储键和值这样的双列数据的集合，List中存储的数据是有顺序，并且允许重复；Map中存储的数据是没有顺序的，其键是不能重复的，它的值是可以有重复的。

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

ArrayList和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，Vector由于使用了synchronized方法（线程安全），通常性能上较ArrayList差。而LinkedList使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历，索引就变慢了，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。LinkedList也是线程不安全的，LinkedList提供了一些方法，使得LinkedList可以被当作堆栈和队列来使用。

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
在这里，转发的路径必须是同一个web容器下的URL，其不能转向到其他的web路径上去，中间传递的 是自己的容器内的request。在客户浏览器路径栏显示的仍然是其第一次访问的路径，也就是说客户是感觉不到服务器做了转发的。转发行为是浏览器只做了一次访问请求。

![forword转发](https://img-blog.csdnimg.cn/20200514202933727.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

重定向过程:客户浏览器发送http请求一一>web服务器接受后发送302状态码响及对应新的location给客户浏览器——>客户端浏览器发现是302状态码，会自动再发送一
个新的http请求,请求url是新的location地址一一>服务器根据此请求寻找资源并发送给客户端浏览器在这里location可以重定向到任意URL，
既然是浏览器重新发出了请求，则就没有什么request传递的概念了。在客户浏览器地址栏显示的是其重定向的路径，客户可以观察到地址的变化的。重定向行为是浏览器做了至少两次的访问请求的。

![redirct重定向](https://img-blog.csdnimg.cn/20200514202710823.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
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

### 18、面试题系列之接口是否可继承接口?抽象类是否可实现(implements)接口?抽象类是否可继承具体类?抽象类中是否可以有静态的main方法？
有一个面试四连击的题目：接口是否可继承接口?抽象类是否可实现(implements)接口?抽象类是否可继承具体类?抽象类中是否可以有静态的main方法？
上面这个题目我们来慢慢的剖析一下。先从基本的概念说起。
#### 一、接口
官方解释：Java接口是一系列方法的声明，是一些方法特征的集合，一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的行为（功能）。
又到了我最喜欢打比方的环节了：我们身边最常见的接口就是电脑的usb接口了。我们可以想想，我们电脑的usb接口是不是就那么几个但是没有任何的具体的功能？但是当我们把u盘插到usb接口的时候，我们可以进行数据的传输；
当我们把鼠标插入usb接口的时候，我们可以左键打开网页、文件夹等更多的功能；当我们把键盘插入到usb接口的时候我们可以打字，等等。虽然接入不同的设备可以进行不同的操作，但是上述的设备操作都是和电脑的数据交互。
所以电脑在设置usb接口的时候，并没有实现具体的读写数据的功能，而是但不同的设备接入usb接口就可以实现不同的数据读写功能。这就是接口的好处，试想：如果每个接口都有特定的功能，鼠标要插这个接口，键盘插那个接
口。那电脑就全是接口了，大大的浪费了资源，而且还不好看。


接口的特点以及重点：
1、并不能直接去实例化一个接口，因为接口中的方法都是抽象的，是没有方法体的。但是，我们可以使用接口类型的引用指向一个实现了该接口的对象(键盘、鼠标，....)，并且可以调用这个接口中的方法。
2、一个类可以实现不止一个接口。键盘可以连接戴尔的接口、华硕的接口、联想的接口。
3、接口也可以继承，并且可以多继承。一个接口可以继承于另一个接口，或者另一些接口。比如现在的很多人电脑的usb接口不够用，所以有了usb接口拓展。
4、接口中所有的方法都是抽象的和public的，所有的属性都是public,static,final的。
5、一个类如果要实现某个接口的话，那么它必须要实现这个接口中的所有方法。我们在使用编辑器编写的时候就会自动提示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020052017470116.png)
否则的话会报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020052017485660.png)
接口的实例：

```cpp
public interface Demo8 {
	void say();
	int add();
}
```

```cpp
public class Demo7 implements Demo8 {
	public static void main(String[] args) {
		Demo7 demo7 = new Demo7();
		demo7.say();
		System.out.println(demo7.add());
	}
	public void say() {
		System.out.println("你好啊");
	}
	public int add() {
	    int i=1;
	    int j=2;
		return i+j;
	}
}
```

```cpp
public interface Demo9 extends Demo8{
	void print(String name);
}
```
一个类实现 一个接口，如果这个接口继承了另一个接口，那么这个类除了实现这个接口的所有方法以外，还要实现被继承的那个接口的所有方法：

```cpp

public class Demo10 implements Demo9 {

	public static void main(String[] args) {
		

	}

	@Override
	public void say() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public int add() {
		// TODO Auto-generated method stub
		return 0;
	}

	@Override
	public void print(String name) {
		// TODO Auto-generated method stub
		
	}

}
```

#### 二、抽象类
在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类。

抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。具有抽象方法的类一定为抽象类。

由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。也是因为这个原因，通常在设计阶段决定要不要设计抽象类。

父类包含了子类集合的常见的方法，但是由于父类本身是抽象的，所以不能使用这些方法。

在Java中抽象类表示的是一种继承关系，一个类只能继承一个抽象类，而一个类却可以实现多个接口。

抽象类用来描述一种类型应该具备的基本特征与功能， 具体如何去完成这些行为由子类通过方法重写来完成，这点与接口很像，所以它们会被作为一类的面试题进行考察如:
猫科均会吼叫，但属于猫科的猫与老虎、豹子等它们吼叫的声音确实不同。所以猫科这就是一个类，它只规定了猫科这类的动物有吼叫功能，但并不明确吼叫的细节，吼叫的细节的内容应该由猫与老虎这样的猫科子类重写吼叫的方法具体实现。
即抽象方法指只有功能声明，没有功能主体实现的方法，与接口中的方法类似，但是抽象方法中除了可以有抽象方法还可以有具体的方法。

抽象类的实例：

```cpp
public abstract class Demo11 {

	   private String name;
	   private String address;
	   private int number;
	   public Demo11(String name, String address, int number)
	   {
	      System.out.println("Constructing an Employee");
	      this.name = name;
	      this.address = address;
	      this.number = number;
	   }
	   public double computePay()
	   {
	     System.out.println("Inside Employee computePay");
	     return 0.0;
	   }
	   public void mailCheck()
	   {
	      System.out.println("Mailing a check to " + this.name
	       + " " + this.address);
	   }
	   public String toString()
	   {
	      return name + " " + address + " " + number;
	   }
	   public String getName()
	   {
	      return name;
	   }
	   public String getAddress()
	   {
	      return address;
	   }
	   public void setAddress(String newAddress)
	   {
	      address = newAddress;
	   }
	   public int getNumber()
	   {
	     return number;
	   }
}
```
可以看到尽管该类是抽象类，但是它仍然有 3 个成员变量，7 个成员方法和 1 个构造方法。但是如果想实例化该类，则会报错：提示不能实例化Demo11
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520180905402.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520181024117.png)
所以抽象类只能通过被继承：

```cpp
public class Demo12 extends Demo11
{
	   private double salary; //Annual salary
	   public Demo12(String name, String address, int number, double
	      salary)
	   {
	       super(name, address, number);
	       setSalary(salary);
	   }
	   public void mailCheck()
	   {
	       System.out.println("Within mailCheck of Salary class ");
	       System.out.println("Mailing check to " + getName()
	       + " with salary " + salary);
	   }
	   public double getSalary()
	   {
	       return salary;
	   }
	   public void setSalary(double newSalary)
	   {
	       if(newSalary >= 0.0)
	       {
	          salary = newSalary;
	       }
	   }
	   public double computePay()
	   {
	      System.out.println("Computing salary pay for " + getName());
	      return salary/52;
	   }
	}
```

```cpp
package Demo1;

public class Demo10 {

	public static void main(String[] args) {
		
		  Demo12 demo12 = new Demo12("张三", "北京", 3, 3600.00);
	      Demo11 demo11 = new Demo12("李四", "上海", 2, 2400.00);
	 
	      System.out.println("Call mailCheck using Salary reference --");
	      demo12.mailCheck();
	 
	      System.out.println("\n Call mailCheck using Employee reference--");
	      demo12.mailCheck();
	}

}

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520181605164.png)
所以尽管不能实例化一个抽象类，但是可以实例化一个继承了抽象类的子类，然后将抽象类的引用指向子类的对象。

如果一个类中它拥有抽象方法，那么这个类就必须是抽象类，抽象类可以没有抽象方法，但是如果有抽象方法的类，必须被申明为抽象类。

```cpp
public abstract class Demo11
{
   private String name;
   private String address;
   private int number;
   //抽象方法
   public abstract double computePay();
}
```
如果一个抽象类中有抽象方法，那么任何继承它的子类都必须重写父类的抽象方法，或者子类也可以声明自身为抽象类。但是最终，必须有子类实现该抽象方法，否则，从最初的父类到最终的子类都不能用来实例化对象，那么就没有任何的意义了。
另外构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。

抽象类可实现接口，并且可以不实现接口中的方法，但是继承抽象类的实体类必须实现接口中的方法。

```cpp
public abstract class Demo11 implements Demo9{

	   private String name;
	   private String address;
	   private int number;
	   public Demo11(String name, String address, int number)
	   {
	      System.out.println("Constructing an Employee");
	      this.name = name;
	      this.address = address;
	      this.number = number;
	   }
	   public double computePay()
	   {
	     System.out.println("Inside Employee computePay");
	     return 0.0;
	   }
	   public void mailCheck()
	   {
	      System.out.println("Mailing a check to " + this.name
	       + " " + this.address);
	   }
	   public String toString()
	   {
	      return name + " " + address + " " + number;
	   }
	   public String getName()
	   {
	      return name;
	   }
	   public String getAddress()
	   {
	      return address;
	   }
	   public void setAddress(String newAddress)
	   {
	      address = newAddress;
	   }
	   public int getNumber()
	   {
	     return number;
	   }
}
```
![
](https://img-blog.csdnimg.cn/20200520182642272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)

另外抽象类也可以继承实体类：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520182910987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMTUzOTQz,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520182924166.png)
抽象类中也可以有静态的main方法。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200520183059554.png)
#### 3、答案
所以接口可以继承接口。抽象类可以实现(implements)接口，抽象类可以继承具体类。抽象类中可以有静态的main方法。

### 19、char型变量中能不能存贮一个中文汉字?为什么?

char型变量是用来存储Unicode编码的字符的，unicode编码字符集中包含了汉字，所以，char型变量中当然可以存储汉字啦。不过，如果某个特殊的汉字没有被包含在unicode编码字符集中，那么，这个char型变量中就不能存储这个特殊汉字。补充说明：unicode编码占用两个字节，所以，char类型的变量也是占用两个字节。

### 20、用最有效率的方法算出2乘以8等于几?

2<< 3，(左移三位)因为将一个数左移n位，就相当于乘以了2的n次方，那么，一个数乘以8只要将其左移3位即可，而位运算cpu直接支持的，效率最高，所以，2乘以8等於几的最效率的方法是2<< 3。

### 21、静态变量和实例变量的区别？

###### 在语法定义上的区别：

静态变量前要加static关键字，而实例变量前则不加。

###### 在程序运行时的区别：

实例变量属于某个对象的属性，必须创建了实例对象，其中的实例变量才会被分配空间，才能使用这个实例变量。静态变量不属于某个实例对象，而是属于类，所以也称为类变量，只要程序加载了类的字节码，不用创建任何实例对象，静态变量就会被分配空间，静态变量就可以被使用了。总之，实例变量必须创建对象后才可以通过这个对象来使用，静态变量则可以直接使用类名来引用。
例如，对于下面的程序，无论创建多少个实例对象，永远都只分配了一个staticVar变量，并且每创建一个实例对象，这个staticVar就会加1；但是，每创建一个实例对象，就会分配一个instanceVar，即可能分配多个instanceVar，并且每个instanceVar的值都只自加了1次。

```java
int arr[][] ={{1,2,3},{4,5,6,7},{9}};
boolean found = false;
for(int i=0;i<arr.length&&!found;i++)    {
    for(intj=0;j<arr[i].length;j++){
       System.out.println(“i=” + i + “,j=” + j);
       if(arr[i][j] ==5) {
           found =true;
           break;
      }
   }
}
```

### 22、是否可以从一个static方法内部发出对非static方法的调用？

不可以。因为非static方法是要与对象关联在一起的，必须创建一个对象后，才可以在该对象上进行方法调用，而static方法调用时不需要创建对象，可以直接调用。也就是说，当一个static方法被调用时，可能还没有创建任何实例对象，如果从一个static方法中发出对非static方法的调用，那个非static方法是关联到哪个对象上的呢？这个逻辑无法成立，所以，一个static方法内部发出对非static方法的调
用。

### 23、Integer与int的区别

int是java提供的8种原始数据类型之一。Java为每个原始类型提供了封装类，Integer是java为int提供的封装类。int的默认值为0，而Integer的默认值为null，即Integer可以区分出未赋值和值为0的区别，int则无法表达出未赋值的情况。

例如：要想表达出没有参加考试和考试成绩为0的区别，则只能使用Integer。在JSP开发中，Integer的默认为null，所以用el表达式在文本框中显示时，值为空白字符串，而int默认的默认值为0，所以用el表达式在文本框中显示时，结果为0，所以，int不适合作为web层的表单数据的类型。

在Hibernate中，如果将OID定义为Integer类型，那么Hibernate就可以根据其值是否为null而判断一个对象是否是临时的，如果将OID定义为了int类型，还需要在hbm映射文件中设置其unsaved-value属性为0。

另外，Integer提供了多个与整数相关的操作方法，例如，将一个字符串转换成整数，Integer中还定
义了表示整数的最大值和最小值的常量。

### 24、Math.round(11.5)等於多少?Math.round(-11.5)等于多少?
Math类中提供了三个与取整有关的方法：ceil、floor、round，这些方法的作用与它们的英文名称的含义相对应。

例如，ceil的英文意义是天花板，该方法就表示向上取整，Math.ceil(11.3)的结果为12,Math.ceil(-11.3)的结果是-11；

floor的英文意义是地板，该方法就表示向下取整，Math.ceil(11.6)的结果为11,Math.ceil(-11.6)的结果是-12；

最难掌握的是round方法，它表示“四舍五入”，算法为Math.floor(x+0.5)，即将原来的数字加上0.5后再向下取整，所以，Math.round(11.5)的结果为12，Math.round(-11.5)的结果为-11。

### 25、Java中实现多态的机制是什么？

Java中的多态靠的是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，而程序调用的方法在运行期才动态绑定，就是引用变量所指向的具体实例对象的方法，也就是内存里正在运行的那个对象的方法，而不是引用变量的类型中定义的方法。

### 26、abstractclass和interface语法上有什么区别?

1、抽象类可以有构造方法，接口中不能有构造方法。
2、抽象类中可以有普通成员变量，接口中没有普通成员变量
3、抽象类中可以包含非抽象的普通方法，接口中的所有方法必须都是抽象的，不能有非抽象的普通方
法。

4、抽象类中的抽象方法的访问类型可以是public，protected和（默认类型,虽然eclipse下不报错，但应该也不行），但接口中的抽象方法只能是public类型的，并且默认即为public abstract类型。

5、抽象类中可以包含静态方法，接口中不能包含静态方法

6、抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是public static final类型，并且默认即为public static final类型。

7、一个类可以实现多个接口，但只能继承一个抽象类。

### 27、abstract的method是否可同时是static,是否可同时是native，是否可同时是synchronized?

abstract的method不可以是static的，因为抽象的方法是要被子类实现的，而static与子类扯不上关系！

native方法表示该方法要用另外一种依赖平台的编程语言实现的，不存在着被子类实现的问题，所以，
它也不能是抽象的，不能与abstract混用。例如，FileOutputSteam类要硬件打交道，底层的实现用的
是操作系统相关的api实现；例如，在windows用c语言实现的，所以，查看jdk的源代码，可以发现
FileOutputStream的open方法的定义如下：

```
private native void open(Stringname) throws FileNotFoundException;
```

如果我们要用java调用别人写的c语言函数，我们是无法直接调用的，我们需要按照java的要求写一个c语言的函数，又我们的这个c语言函数去调用别人的c语言函数。由于我们的c语言函数是按java的要求来写的，我们这个c语言函数就可以与java对接上，java那边的对接方式就是定义出与我们这个c函数相对应的方法，java中对应的方法不需要写具体的代码，但需要在前面声明native。

关于synchronized与abstract合用的问题，个人从来没见到过这种情况，并且我觉得synchronized应该是作用在一个具体的方法上才有意义。而且，方法上的synchronized同步所使用的同步锁对象是this，而抽象方法上无法确定this是什么。

### 28、内部类可以引用它的包含类的成员吗？有没有什么限制？

完全可以。如果不是静态内部类，那没有什么限制！
如果把静态嵌套类当作内部类的一种特例，那在这种情况下不可以访问外部类的普通成员变量，而只能访问外部类中的静态成员。

例如，下面的代码：

```java
class Outer
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
```

### 29、如何去掉一个Vector集合中重复的元素？

```java
Vector newVector = new Vector();
For (int i=0;i<vector.size();i++)
{
   Object obj = vector.get(i);
   if(!newVector.contains(obj);
      newVector.add(obj);
}
```

还有一种简单的方式，利用了Set不允许重复元素：

```java
HashSetset = new HashSet(vector);
```

### 30、Collection和Collections的区别

Collection是集合类的上级接口，继承他的接口主要有Set和List。

Collections是针对集合类的一个帮助类，他提供一系列静态方法实现对各种集合的搜索、排序、线程
安全化等操作。

### 31、Set里的元素是不能重复的，那么用什么方法来区分重复与否呢?是用==还是equals()?它们有何区别?

Set里的元素是不能重复的，元素重复与否是使用equals()方法进行判断的。

### 32、==和equal区别

==是用来比较两个变量的值是否相等，也就是用于比较变量所对应的内存中所存储的数值是否相同，要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作符。

而equals方法是用于比较两个独立对象的内容是否相同，就好比去比较两个人的长相是否相同，它比较的两个对象是独立的。

比如：两条new语句创建了两个对象，然后用a/b这两个变量分别指向了其中一个对象，这是两个不同的对象，它们的首地址是不同的，即a和b中存储的数值是不相同的，所以，表达式a==b将返回false，而这两个对象中的内容是相同的，所以，表达式a.equals(b)将返回true。

==操作符专门用来比较两个变量的值是否相等，也就是用于比较变量所对应的内存中所存储的数值是否相同，要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作符。

如果一个变量指向的数据是对象类型的，那么，这时候涉及了两块内存，对象本身占用一块内存（堆内存），变量也占用一块内存，例如Objet obj = new Object();变量obj是一个内存，new Object()是另一个内存，此时，变量obj所对应的内存中存储的数值就是对象占用的那块内存的首地址。对于指向对象类型的变量，如果要比较两个变量是否指向同一个对象，即要看这两个变量所对应的内存中的数值是否相等，这时候就需要用==操作符进行比较。

equals方法是用于比较两个独立对象的内容是否相同，就好比去比较两个人的长相是否相同，它比较的两个对象是独立的。例如，对于下面的代码：

```
String a=new String("foo");

String b=new String("foo");
```

两条new语句创建了两个对象，然后用a,b这两个变量分别指向了其中一个对象，这是两个不同的对象，它们的首地址是不同的，即a和b中存储的数值是不相同的，所以，表达式a==b将返回false，而这两个对象中的内容是相同的，所以，表达式a.equals(b)将返回true。

在实际开发中，我们经常要比较传递进行来的字符串内容是否等，例如，String input = …;input.equals(“quit”)，许多人稍不注意就使用==进行比较了，这是错误的，随便从网上找几个项目实战的教学视频看看，里面就有大量这样的错误。记住，字符串的比较基本上都是使用equals方法。

如果一个类没有自己定义equals方法，那么它将继承Object类的equals方法，Object类的equals方法的实现代码如下：

```
boolean equals(Object o){

return this==o;

}
```

这说明，如果一个类没有自己定义equals方法，它默认的equals方法（从Object 类继承的）就是使用==操作符，也是在比较两个变量指向的对象是否是同一对象，这时候使用equals和使用==会得到同样的结果，如果比较的是两个独立的对象则总返回false。如果你编写的类希望能够比较该类创建的两个实例对象的内容是否相同，那么你必须覆盖equals方法，由你自己写代码来决定在什么情况即可认为两个对象的内容是相同的。

### 33、集合类都有哪些？主要方法？

最常用的集合类是 List 和 Map。 List的具体实现包括 ArrayList和 Vector，它们是可变大小的列表，比较适合构建、存储和操作任何类型对象的元素列表。 List适用于按数值索引访问元素的情形。

Map 提供了一个更通用的元素存储方法。 Map集合类用于存储元素对（称作"键"和"值"），其中每个键映射到一个值。它们都有增删改查的方法。

对于set，大概的方法是add,remove, contains等

对于map，大概的方法就是put,remove，contains等

List类会有get(int index)这样的方法，因为它可以按顺序取元素，而set类中没有get(int index)这样的方法。List和set都可以迭代出所有元素，迭代时先要得到一个iterator对象，所以，set和list类都有一个iterator方法，用于返回那个iterator对象。map可以返回三个集合，一个是返回所有的key的集合，另外一个返回的是所有value的集合，再一个返回的key和value组合成的EntrySet对象的集合，map也有
get方法，参数是key，返回值是key对应的value，这个自由发挥，也不是考记方法的能力，这些编程过程中会有提示，结合他们三者的不同说一下用法就行。

### 34、String s = new String("xyz");创建了几个StringObject？是否可以继承String类?

两个或一个都有可能，”xyz”对应一个对象，这个对象放在字符串常量缓冲区，常量”xyz”不管出现多少遍，都是缓冲区中的那一个。NewString每写一遍，就创建一个新的对象，它使用常量”xyz”对象的内容来创建出一个新String对象。如果以前就用过’xyz’，那么这里就不会创建”xyz”了，直接从缓冲区拿，这时创建了一个StringObject；但如果以前没有用过"xyz"，那么此时就会创建一个对象并放入缓冲区，这种情况它创建两个对象。至于String类是否继承，答案是否定的，因为String默认final修饰，是不可继承的。

### 35、String和StringBuffer的区别
JAVA平台提供了两个类：String和StringBuffer，它们可以储存和操作字符串，即包含多个字符的字符数据。这个String类提供了数值不可改变的字符串。而这个StringBuffer类提供的字符串可以进行修改。当你知道字符数据要改变的时候你就可以使用StringBuffer。典型地，你可以使用StringBuffers来动态构造字符数据。

### 36、下面这条语句一共创建了多少个对象：Strings="a"+"b"+"c"+"d";

对于如下代码：

```java
String s1 = "a";
String s2 = s1 + "b";
String s3 = "a" + "b";
System.out.println(s2 == "ab");
System.out.println(s3 == "ab");
```

第一条语句打印的结果为false，第二条语句打印的结果为true，这说明javac编译可以对字符串常量直接相加的表达式进行优化，不必要等到运行期再去进行加法运算处理，而是在编译时去掉其中的加号，直接将其编译成一个这些常量相连的结果。题目中的第一行代码被编译器在编译时优化后，相当于直接定义了一个”abcd”的字符串，所以，上面的代码应该只创建了一个String对象。

对于如下代码：

```
String s ="a" + "b" +"c" + "d";
System.out.println(s== "abcd");
```

最终打印的结果应该为true。

### 37、try {}里有一个return语句，那么紧跟在这个try后的finally{}里的code会不会被执行，什么时候被执行，在return前还是后?

我们知道finally{}中的语句是一定会执行的，那么这个可能正常脱口而出就是return之前，return之
后可能就出了这个方法了，鬼知道跑哪里去了，但更准确的应该是在return中间执行，请看下面程序代
码的运行结果：

```
public classTest {
  public static void main(String[]args) {
   System.out.println(newTest().test());;
 }
  static int test()
 {
   intx = 1;
   try
   {
     returnx;
   }
   finally
   {
     ++x;
   }
 }
}
```

---------执行结果 ---------
1
运行结果是1，为什么呢？主函数调用子函数并得到结果的过程，好比主函数准备一个空罐子，当子函
数要返回结果时，先把结果放在罐子里，然后再将程序逻辑返回到主函数。所谓返回，就是子函数说，
我不运行了，你主函数继续运行吧，这没什么结果可言，结果是在说这话之前放进罐子里的。

### 38、final, finally, finalize的区别。

final 用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。内部类要访问局部变量，局部变量必须定义成final类型。

finally是异常处理语句结构的一部分，表示总是执行。

finalize是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等。但是JVM不保证此方法总被调用

### 39、运行时异常与一般异常有何异同？

异常表示程序运行过程中可能出现的非正常状态，运行时异常表示虚拟机的通常操作中可能遇到的异常，是一种常见运行错误。java编译器要求方法必须声明抛出可能发生的非运行时异常，但是并不要求必须声明抛出未被捕获的运行时异常。

### 40、error和exception有什么区别?

error 表示恢复不是不可能但很困难的情况下的一种严重问题。比如说内存溢出。不可能指望程序能处理这样的情况。exception表示一种设计或实现问题。也就是说，它表示如果程序运行正常，从不会发生的情况。

### 41、简单说说Java中的异常处理机制的简单原理和应用。

异常是指java程序运行时（非编译）所发生的非正常情况或错误，与现实生活中的事件很相似，现实生活中的事件可以包含事件发生的时间、地点、人物、情节等信息，可以用一个对象来表示，Java使用面向对象的方式来处理异常，它把程序中发生的每个异常也都分别封装到一个对象来表示的，该对象中包含有异常的信息。

Java对异常进行了分类，不同类型的异常分别用不同的Java类表示，所有异常的根类为
java.lang.Throwable，Throwable下面又派生了两个子类：

Error和Exception，Error表示应用程序本身无法克服和恢复的一种严重问题，程序只有奔溃了，例如，说内存溢出和线程死锁等系统问题。

Exception表示程序还能够克服和恢复的问题，其中又分为系统异常和普通异常：系统异常是软件本身缺陷所导致的问题，也就是软件开发人员考虑不周所导致的问题，软件使用者无法克服和恢复这种问题，但在这种问题下还可以让软件系统继续运行或者让软件挂掉，例如，数组脚本越界（ArrayIndexOutOfBoundsException），空指针异常（NullPointerException）、类转换异常
（ClassCastException）；

普通异常是运行环境的变化或异常所导致的问题，是用户能够克服的问题，例如，网络断线，硬盘空间不够，发生这样的异常后，程序不应该死掉。

java为系统异常和普通异常提供了不同的解决方案，编译器强制普通异常必须try..catch处理或用throws声明继续抛给上层调用方法处理，所以普通异常也称为checked异常，而系统异常可以处理也可以不处理，所以，编译器不强制用try..catch处理或用throws声明，所以系统异常也称为unchecked异常。

### 42、Java 中堆和栈有什么区别？

JVM 中堆和栈属于不同的内存区域，使用目的也不同。栈常用于保存方法帧和局部变量，而对象总是在堆上分配。栈通常都比堆小，也不会在多个线程之间共享，而堆被整个 JVM 的所有线程共享。

栈：在函数中定义的一些基本类型的变量和对象的引用变量都是在函数的栈内存中分配，当在一段代码块定义一个变量时，Java 就在栈中为这个变量分配内存空间，当超过变量的作用域后，Java 会自动释放掉为该变量分配的内存空间，该内存空间可以立即被另作它用。

堆：堆内存用来存放由 new 创建的对象和数组，在堆中分配的内存，由 Java 虚拟机的自动垃圾回收器来管理。在堆中产生了一个数组或者对象之后，还可以在栈中定义一个特殊的变量，让栈中的这个变量的取值等于数组或对象在堆内存中的首地址，栈中的这个变量就成了数组或对象的引用变量，以后就可以在程序中使用栈中的引用变量来访问堆中的数组或者对象，引用变量就相当于是为数组或者对象起
的一个名称。

### 43、能将 int 强制转换为 byte 类型的变量吗？如果该值大于 byte类型的范围，将会出现什么现象？

我们可以做强制转换，但是 Java 中 int 是 32 位的，而 byte 是 8 位的，所以，如果强制转化，int 类型的高 24 位将会被丢弃，因为byte 类型的范围是从 -128 到 128。这里笔误：-128到127

### 44、**Redis常用的五种数据类型**

**1.String（字符串）**

String是简单的 key-value 键值对，value 不仅可以是 String，也可以是数字。它是Redis最基本的数据类型，一个redis中字符串value最多可以是512M。

**2.Hash（哈希）**

Redis hash 是一个键值对集合，对应Value内部实际就是一个HashMap，Hash特别适合用于存储对象。

**3.List（列表）**

Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素导列表的头部（左边）或者尾部（右边）。

底层实现为一个双向链表，即可以支持反向查找和遍历，更方便操作，不过带来了部分额外的内存开销，Redis内部的很多实现，包括发送缓冲队列等也都是用的这个数据结构。

**4.Set（集合）**

Redis的Set是String类型的无序集合，它的内部实现是一个 value永远为null的HashMap，实际就是通过计算hash的方式来快速排重的，这也是set能提供判断一个成员是否在集合内的原因。

**5.zset(有序集合)**

Redis zset 和 set 一样也是String类型元素的集合,且不允许重复的成员，不同的是每个元素都会关联一个double类型的分数，用来排序。

###  45、**接口有什么用**

1、通过接口可以实现不相关类的相同行为，而不需要了解对象所对应的类。

2、通过接口可以指明多个类需要实现的方法。

3、通过接口可以了解对象的交互界面，而不需了解对象所对应的类。

另：Java是单继承，接口可以使其实现多继承的功能。

### 46、Java中堆内存和栈内存详解

Java把内存分成两种，一种叫做栈内存，一种叫做堆内存。

在函数中定义的一些基本类型的变量和对象的引用变量都是在函数的栈内存中分配。**当在一段代码块中定义一个变量时，java就在栈中为这个变量分配内存空间，当超过变量的作用域后，java会自动释放掉为该变量分配的内存空间，该内存空间可以立刻被另作他用。**

**堆内存用于存放由new创建的对象和数组。**在堆中分配的内存，由java虚拟机自动垃圾回收器来管理。在堆中产生了一个数组或者对象后，还可以在栈中定义一个特殊的变量，这个变量的取值等于数组或者对象在堆内存中的首地址，在栈中的这个特殊的变量就变成了数组或者对象的引用变量，以后就可以在程序中使用栈内存中的引用变量来访问堆中的数组或者对象，引用变量相当于为数组或者对象起的一个别名，或者代号。

引用变量是普通变量，定义时在栈中分配内存，引用变量在程序运行到作用域外释放。而数组＆对象本身在堆中分配，即使程序运行到使用new产生数组和对象的语句所在地代码块之外，数组和对象本身占用的堆内存也不会被释放，**数组和对象在没有引用变量指向它的时候，才变成垃圾，不能再被使用，但是仍然占着内存，在随后的一个不确定的时间被垃圾回收器释放掉**。这个也是java比较占内存的主要原因，实际上，栈中的变量指向堆内存中的变量，这就是 Java 中的指针!

**java中内存分配策略及堆和栈的比较**

　　**1 内存分配策略**

　　按照编译原理的观点,程序运行时的内存分配有三种策略,分别是静态的,栈式的,和堆式的.

　　静态存储分配是指在编译时就能确定每个数据目标在运行时刻的存储空间需求,因而在编译时就可以给他们分配固定的内存空间.这种分配策略要求程序代码中不允许有可变数据结构(比如可变数组)的存在,也不允许有嵌套或者递归的结构出现,因为它们都会导致编译程序无法计算准确的存储空间需求.

　　栈式存储分配也可称为动态存储分配,是由一个类似于堆栈的运行栈来实现的.和静态存储分配相反,在栈式存储方案中,程序对数据区的需求在编译时是完全未知的,只有到运行的时候才能够知道,但是规定在运行中进入一个程序模块时,必须知道该程序模块所需的数据区大小才能够为其分配内存.和我们在数据结构所熟知的栈一样,栈式存储分配按照先进后出的原则进行分配。

　　静态存储分配要求在编译时能知道所有变量的存储要求,栈式存储分配要求在过程的入口处必须知道所有的存储要求,而堆式存储分配则专门负责在编译时或运行时模块入口处都无法确定存储要求的数据结构的内存分配,比如可变长度串和对象实例.堆由大片的可利用块或空闲块组成,堆中的内存可以按照任意顺序分配和释放.

　　**2 堆和栈的比较**

　　上面的定义从编译原理的教材中总结而来,除静态存储分配之外,都显得很呆板和难以理解,下面撇开静态存储分配,集中比较堆和栈:

　　从堆和栈的功能和作用来通俗的比较,堆主要用来存放对象的，栈主要是用来执行程序的.而这种不同又主要是由于堆和栈的特点决定的:

　　在编程中，例如C/C++中，所有的方法调用都是通过栈来进行的,所有的局部变量,形式参数都是从栈中分配内存空间的。实际上也不是什么分配,只是从栈顶向上用就行,就好像工厂中的传送带(conveyor belt)一样,Stack Pointer会自动指引你到放东西的位置,你所要做的只是把东西放下来就行.退出函数的时候，修改栈指针就可以把栈中的内容销毁.这样的模式速度最快, 当然要用来运行程序了.需要注意的是,在分配的时候,比如为一个即将要调用的程序模块分配数据区时,应事先知道这个数据区的大小,也就说是虽然分配是在程序运行时进行的,但是分配的大小多少是确定的,不变的,而这个"大小多少"是在编译时确定的,不是在运行时.

　　堆是应用程序在运行的时候请求操作系统分配给自己内存，由于从操作系统管理的内存分配,所以在分配和销毁时都要占用时间，因此用堆的效率非常低.但是堆的优点在于,编译器不必知道要从堆里分配多少存储空间，也不必知道存储的数据要在堆里停留多长的时间,因此,用堆保存数据时会得到更大的灵活性。事实上,面向对象的多态性,堆内存分配是必不可少的,因为多态变量所需的存储空间只有在运行时创建了对象之后才能确定.在C++中，要求创建一个对象时，只需用 new命令编制相关的代码即可。执行这些代码时，会在堆里自动进行数据的保存.当然，为达到这种灵活性，必然会付出一定的代价:在堆里分配存储空间时会花掉更长的时间!这也正是导致我们刚才所说的效率低的原因,看来列宁同志说的好,人的优点往往也是人的缺点,人的缺点往往也是人的优点(晕~).

　　**3 JVM中的堆和栈**

　　JVM是基于堆栈的虚拟机.JVM为每个新创建的线程都分配一个堆栈.也就是说,对于一个Java程序来说，它的运行就是通过对堆栈的操作来完成的。堆栈以帧为单位保存线程的状态。JVM对堆栈只进行两种操作:以帧为单位的压栈和出栈操作。

　　我们知道,某个线程正在执行的方法称为此线程的当前方法.我们可能不知道,当前方法使用的帧称为当前帧。当线程激活一个Java方法,JVM就会在线程的 Java堆栈里新压入一个帧。这个帧自然成为了当前帧.在此方法执行期间,这个帧将用来保存参数,局部变量,中间计算过程和其他数据.这个帧在这里和编译原理中的活动纪录的概念是差不多的.

　　从Java的这种分配机制来看,堆栈又可以这样理解:堆栈(Stack)是操作系统在建立某个进程时或者线程(在支持多线程的操作系统中是线程)为这个线程建立的存储区域，该区域具有先进后出的特性。

　　每一个Java应用都唯一对应一个JVM实例，每一个实例唯一对应一个堆。应用程序在运行中所创建的所有类实例或数组都放在这个堆中,并由应用所有的线程共享.跟C/C++不同，Java中分配堆内存是自动初始化的。Java中所有对象的存储空间都是在堆中分配的，但是这个对象的引用却是在堆栈中分配,也就是说在建立一个对象时从两个地方都分配内存，在堆中分配的内存实际建立这个对象，而在堆栈中分配的内存只是一个指向这个堆对象的指针(引用)而已。

　　**4 Java 中的堆和栈**

　　Java把内存划分成两种：一种是栈内存，一种是堆内存。

　　在函数中定义的一些基本类型的变量和对象的引用变量都在函数的栈内存中分配。

　　当在一段代码块定义一个变量时，Java就在栈中为这个变量分配内存空间，当超过变量的作用域后，Java会自动释放掉为该变量所分配的内存空间，该内存空间可以立即被另作他用。

　　堆内存用来存放由new创建的对象和数组。

　　在堆中分配的内存，由Java虚拟机的自动垃圾回收器来管理。

　　在堆中产生了一个数组或对象后，还可以在栈中定义一个特殊的变量，让栈中这个变量的取值等于数组或对象在堆内存中的首地址，栈中的这个变量就成了数组或对象的引用变量。

　　引用变量就相当于是为数组或对象起的一个名称，以后就可以在程序中使用栈中的引用变量来访问堆中的数组或对象。

　　具体的说：

　　**栈与堆都是Java用来在Ram中存放数据的地方。与C++不同，Java自动管理栈和堆，程序员不能直接地设置栈或堆。**

　　Java的堆是一个运行时数据区,类的(对象从中分配空间。这些对象通过new、newarray、anewarray和multianewarray等指令建立，它们不需要程序代码来显式的释放。堆是由垃圾回收来负责的，堆的优势是可以动态地分配内存大小，生存期也不必事先告诉编译器，因为它是在运行时动态分配内存的，Java的垃圾收集器会自动收走这些不再使用的数据。但缺点是，由于要在运行时动态分配内存，存取速度较慢。

　　栈的优势是，存取速度比堆要快，仅次于寄存器，栈数据可以共享。但缺点是，存在栈中的数据大小与生存期必须是确定的，缺乏灵活性。栈中主要存放一些基本类型的变量(,int, short, long, byte, float, double, boolean, char)和对象句柄。

　　栈有一个很重要的特殊性，就是存在栈中的数据可以共享。假设我们同时定义：

　　int a = 3;

　　int b = 3;

　　编译器先处理int a = 3;首先它会在栈中创建一个变量为a的引用，然后查找栈中是否有3这个值，如果没找到，就将3存放进来，然后将a指向3。接着处理int b = 3;在创建完b的引用变量后，因为在栈中已经有3这个值，便将b直接指向3。这样，就出现了a与b同时均指向3的情况。这时，如果再令a=4;那么编译器会重新搜索栈中是否有4值，如果没有，则将4存放进来，并令a指向4;如果已经有了，则直接将a指向这个地址。因此a值的改变不会影响到b的值。要注意这种数据的共享与两个对象的引用同时指向一个对象的这种共享是不同的，因为这种情况a的修改并不会影响到b, 它是由编译器完成的，它有利于节省空间。而一个对象引用变量修改了这个对象的内部状态，会影响到另一个对象引用变量。

### 47、**List和Set比较，各自的子类比较**

**对比一：****Arraylist与LinkedList的比较**

1、ArrayList是实现了基于动态数组的数据结构,因为地址连续，一旦数据存储好了，查询操作效率会比较高（在内存里是连着放的）。

2、因为地址连续， ArrayList要移动数据,所以插入和删除操作效率比较低。  

3、LinkedList基于链表的数据结构,地址是任意的，所以在开辟内存空间的时候不需要等一个连续的地址，对于新增和删除操作add和remove，LinedList比较占优势。

4、因为LinkedList要移动指针,所以查询操作性能比较低。

**适用场景分析：**

当需要对数据进行对此访问的情况下选用ArrayList，当需要对数据进行多次增加删除修改时采用LinkedList。

**对比二：****ArrayList与Vector的比较**

1、Vector的方法都是同步的，是线程安全的，而ArrayList的方法不是，由于线程的同步必然要影响性能。因此，ArrayList的性能比Vector好。 
2、当Vector或ArrayList中的元素超过它的初始大小时，Vector会将它的容量翻倍，而ArrayList只增加50%的大小，这样。ArrayList就有利于节约内存空间。

3、大多数情况不使用Vector，因为性能不好，但是它支持线程的同步，即某一时刻只有一个线程能够写Vector，避免多线程同时写而引起的不一致性。

4、Vector可以设置增长因子，而ArrayList不可以。

**适用场景分析：**

1、Vector是线程同步的，所以它也是线程安全的，而ArrayList是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用ArrayList效率比较高。

2、如果集合中的元素的数目大于目前集合数组的长度时，在集合中使用数据量比较大的数据，用Vector有一定的优势。

**对比三：****HashSet与TreeSet的比较**

1.TreeSet 是二叉树实现的，Treeset中的数据是自动排好序的，不允许放入null值 。

2.HashSet 是哈希表实现的，HashSet中的数据是无序的，可以放入null，但只能放入一个null，两者中的值都不能重复，就如数据库中唯一约束 。

3.HashSet要求放入的对象必须实现HashCode()方法，放入的对象，是以hashcode码作为标识的，而具有相同内容的String对象，hashcode是一样，所以放入的内容不能重复。但是同一个类的对象可以放入不同的实例。

**适用场景分析：**

HashSet是基于Hash算法实现的，其性能通常都优于TreeSet。我们通常都应该使用HashSet，在我们需要排序的功能时，我们才使用TreeSet。

### 48、**HashMap和ConcurrentHashMap的区别**

1、HashMap不是线程安全的，而ConcurrentHashMap是线程安全的。

2、ConcurrentHashMap采用锁分段技术，将整个Hash桶进行了分段segment，也就是将这个大的数组分成了几个小的片段segment，而且每个小的片段segment上面都有锁存在，那么在插入元素的时候就需要先找到应该插入到哪一个片段segment，然后再在这个片段上面进行插入，而且这里还需要获取segment锁。

3、ConcurrentHashMap让锁的粒度更精细一些，并发性能更好。

### 49、**HashTable和ConcurrentHashMap的区别**

它们都可以用于多线程的环境，但是当Hashtable的大小增加到一定的时候，性能会急剧下降，因为迭代时需要被锁定很长的时间。因为ConcurrentHashMap引入了分割(segmentation)，不论它变得多么大，仅仅需要锁定map的某个部分，而其它的线程不需要等到迭代完成才能访问map。简而言之，在迭代的过程中，ConcurrentHashMap仅仅锁定map的某个部分，而Hashtable则会锁定整个map。

### 50、**String,StringBuffer和StringBuilder的区别**

1、运行速度，或者说是执行速度，在这方面运行速度快慢为：StringBuilder > StringBuffer > String。

2、线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的。

**适用场景分析：**

String：适用于少量的字符串操作的情况

StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况

StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况

### 51、**wait和sleep的区别**

1、sleep()方法是属于Thread类中的，而wait()方法，则是属于Object类中的。

2、sleep()方法导致了程序暂停执行指定的时间，让出cpu给其他线程，但是他的监控状态依然保持着，当指定的时间到了又会自动恢复运行状态。所以在调用sleep()方法的过程中，线程不会释放对象锁。

3、调用wait()方法的时候，线程会放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象调用notify()方法后本线程才进入对象锁定池准备获取对象锁进入运行状态。

### 52、**JVM的内存结构**

根据 JVM 规范，JVM 内存共分为虚拟机栈、堆、方法区、程序计数器、本地方法栈五个部分。

**1、Java虚拟机栈：**

线程私有；每个方法在执行的时候会创建一个栈帧，存储了局部变量表，操作数栈，动态连接，方法返回地址等；每个方法从调用到执行完毕，对应一个栈帧在虚拟机栈中的入栈和出栈。

**2、堆：**

线程共享；被所有线程共享的一块内存区域，在虚拟机启动时创建，用于存放对象实例。

**3、方法区：**

线程共享；被所有线程共享的一块内存区域；用于存储已被虚拟机加载的类信息，常量，静态变量等。

**4、程序计数器：**

线程私有；是当前线程所执行的字节码的行号指示器，每条线程都要有一个独立的程序计数器，这类内存也称为“线程私有”的内存。

**5、本地方法栈：**

线程私有；主要为虚拟机使用到的Native方法服务。

### 53、**强引用，软引用和弱引用的区别**

**强引用：**

只有这个引用被释放之后，对象才会被释放掉，只要引用存在，垃圾回收器永远不会回收，这是最常见的New出来的对象。

**软引用：**

内存溢出之前通过代码回收的引用。软引用主要用户实现类似缓存的功能，在内存足够的情况下直接通过软引用取值，无需从繁忙的真实来源查询数据，提升速度；当内存不足时，自动删除这部分缓存数据，从真正的来源查询这些数据。

**弱引用：**

第二次垃圾回收时回收的引用，短时间内通过弱引用取对应的数据，可以取到，当执行过第二次垃圾回收时，将返回null。弱引用主要用于监控对象是否已经被垃圾回收器标记为即将回收的垃圾，可以通过弱引用的isEnQueued方法返回对象是否被垃圾回收器标记。

### 54、**数组在内存中如何分配**

1、简单的值类型的数组，每个数组成员是一个引用（指针），引用到栈上的空间（因为值类型变量的内存分配在栈上）

2、引用类型，类类型的数组，每个数组成员仍是一个引用（指针），引用到堆上的空间（因为类的实例的内存分配在堆上）

### 55、**java的多态表现在哪里**

**简单的理解多态**

多态，简而言之就是同一个行为具有多个不同表现形式或形态的能力。比如说，有一杯水，我不知道它是温的、冰的还是烫的，但是我一摸我就知道了。我摸水杯这个动作，对于不同温度的水，就会得到不同的结果。这就是多态。

那么，java中是怎么体现多态呢？我们来直接看代码：

```java
public class Water {
   public void showTem(){
       System.out.println("我的温度是: 0度");
   }
}

public class IceWater extends Water {
   public void showTem(){
       System.out.println("我的温度是: 0度");
   }
}

public class WarmWater extends Water {
   public void showTem(){
       System.out.println("我的温度是: 40度");
   }
}

public class HotWater extends Water {
   public void showTem(){
       System.out.println("我的温度是: 100度");
   }
}

public class TestWater{
   public static void main(String[] args) {
       Water w = new WarmWater();
       w.showTem();

       w = new IceWater();
       w.showTem();

       w = new HotWater();
       w.showTem();

   }
}
```

运行结果：

```java
我的温度是: 40度
我的温度是: 0度
我的温度是: 100度
```

这段代码中最关键的就是这一句

```java
Water w = new WarmWater();
```

这句代码体现的就是向上转型。后面我会详细讲解这一知识点。

**多态的分类**

已经简单的认识了多态了，那么我们来看一下多态的分类。

多态一般分为两种：**重写式多态和重载式多态**。重写和重载这两个知识点前面的文章已经详细将结果了，这里就不多说了。

重载式多态，也叫编译时多态。也就是说这种多态再编译时已经确定好了。重载大家都知道，方法名相同而参数列表不同的一组方法就是重载。在调用这种重载的方法时，通过传入不同的参数最后得到不同的结果。

> 但是这里是有歧义的，有的人觉得不应该把重载也算作多态。因为很多人对多态的理解是：**程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，这种情况叫做多态。** 这个定义中描述的就是我们的第二种多态—重写式多态。并且，重载式多态并不是面向对象编程特有的，而多态却是面向对象三大特性之一（如果我说的不对，记得告诉我。。）。
>
> 我觉得大家也没有必要在定义上去深究这些，我的理解是：**同一个行为具有多个不同表现形式或形态的能力**就是多态，所以我认为重载也是一种多态，如果你不同意这种观点，我也接受。

重写式多态，也叫运行时多态。这种多态通过动态绑定（dynamic binding）技术来实现，是指在执行期间判断所引用对象的实际类型，根据其实际的类型调用其相应的方法。也就是说，只有程序运行起来，你才知道调用的是哪个子类的方法。 
这种多态通过函数的重写以及向上转型来实现，我们上面代码中的例子就是一个完整的重写式多态。我们接下来讲的所有多态都是重写式多态，因为它才是面向对象编程中真正的多态。

> 动态绑定技术涉及到jvm，暂时不讲（因为我也不懂，哈哈哈哈），感兴趣的可以自己去研究一下，我暂时还没有时间去研究jvm。。

**多态的条件**

**继承**。在多态中必须存在有继承关系的子类和父类。

**重写**。子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。

**向上转型**。在多态中需要将子类的引用赋给父类对象，只有这样该引用才能够具备技能调用父类的方法和子类的方法。

继承也可以替换为实现接口。

继承和重写之前都说过了，接下来我们来看一下转型是什么。

向上转型与向下转型

**向上转型**

子类引用的对象转换为父类类型称为向上转型。通俗地说就是是将子类对象转为父类对象。此处父类对象可以是接口。

**转型过程中需要注意的问题**

向上转型时，子类单独定义的方法会丢失。比如上面Dog类中定义的run方法，当animal引用指向Dog类实例时是访问不到run方法的，animal.run()会报错。

子类引用不能指向父类对象。Cat c = (Cat)new Animal()这样是不行的。

**向上转型的好处**

减少重复代码，使代码变得简洁。

提高系统扩展性。

**向下转型**

与向上转型相对应的就是向下转型了。向下转型是把父类对象转为子类对象。(请注意！这里是有坑的。)

**向下转型注意事项**

向下转型的前提是父类对象指向的是子类对象（也就是说，在向下转型之前，它得先向上转型）

向下转型只能转型为本类对象（猫是不能变成狗的）。

**总结**

1. 多态，简而言之就是同一个行为具有多个不同表现形式或形态的能力。
2. 多态的分类：运行时多态和编译时多态。
3. 运行时多态的前提：继承（实现），重写，向上转型
4. 向上转型与向下转型。
5. 继承链中对象方法的调用的优先级：this.show(O)、super.show(O)、this.show((super)O)、super.show((super)O)。

多态主要有两种表现形式：重载和重写

**重载：**

是发生在同一类中，具有相同的方法名，主要是看参数的个数，类型，顺序不同实现方法的重载的，返回值的类型可以不同。

**重写：**

是发生在两个类中（父类和子类），具有相同的方法名，主要看方法中参数，个数，类型必须相同，返回值的类型必须相同。

### 56、**BIO、NIO和AIO的区别**

Java BIO ： 同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善。

Java NIO ： 同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。

Java AIO 异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理。

NIO比BIO的改善之处是把一些无效的连接挡在了启动线程之前，减少了这部分资源的浪费（因为我们都知道每创建一个线程，就要为这个线程分配一定的内存空间）

AIO比NIO的进一步改善之处是将一些暂时可能无效的请求挡在了启动线程之前，比如在NIO的处理方式中，当一个请求来的话，开启线程进行处理，但这个请求所需要的资源还没有就绪，此时必须等待后端的应用资源，这时线程就被阻塞了。

**适用场景分析：**

 BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解，如之前在Apache中使用。

 NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持，如在 Nginx，Netty中使用。

 AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持，在成长中，Netty曾经使用过，后来放弃。

### 57、**java中常说的堆和栈，分别是什么数据结构；另外，为什么要分为堆和栈来存储数据**


栈是一种具有后进先出性质的数据结构，也就是说后存放的先取，先存放的后取。

堆是一种经过排序的树形数据结构，每个结点都有一个值。通常我们所说的堆的数据结构，是指二叉堆。堆的特点是根结点的值最小（或最大），且根结点的两个子树也是一个堆。由于堆的这个特性，常用来实现优先队列，堆的存取是随意的。

**为什么要划分堆和栈**

1、从软件设计的角度看，栈代表了处理逻辑，而堆代表了数据。这样分开，使得处理逻辑更为清晰。

2、堆与栈的分离，使得堆中的内容可以被多个栈共享。一方面这种共享提供了一种有效的数据交互方式(如：共享内存)，另一方面，堆中的共享常量和缓存可以被所有栈访问，节省了空间。

3、栈因为运行时的需要，比如保存系统运行的上下文，需要进行地址段的划分。由于栈只能向上增长，因此就会限制住栈存储内容的能力。而堆不同，堆中的对象是可以根据需要动态增长的，因此栈和堆的拆分，使得动态增长成为可能，相应栈中只需记录堆中的一个地址即可。

4、体现了Java面向对象这一核心特点

### 58、**为什么要用线程池**

**什么是线程池**

线程池是指在初始化一个多线程应用程序过程中创建一个线程集合，然后在需要执行新的任务时重用这些线程而不是新建一个线程。

**使用线程池的好处**

1、线程池改进了一个应用程序的响应时间。由于线程池中的线程已经准备好且等待被分配任务，应用程序可以直接拿来使用而不用新建一个线程。

2、线程池节省了CLR 为每个短生存周期任务创建一个完整的线程的开销并可以在任务完成后回收资源。

3、线程池根据当前在系统中运行的进程来优化线程时间片。

4、线程池允许我们开启多个任务而不用为每个线程设置属性。

5、线程池允许我们为正在执行的任务的程序参数传递一个包含状态信息的对象引用。

6、线程池可以用来解决处理一个特定请求最大线程数量限制问题。

### 59、**悲观锁和乐观锁的区别，怎么实现**

悲观锁：一段执行逻辑加上悲观锁,不同线程同时执行时,只能有一个线程执行,其他的线程在入口处等待,直到锁被释放。

乐观锁：一段执行逻辑加上乐观锁,不同线程同时执行时,可以同时进入执行,在最后更新数据的时候要检查这些数据是否被其他线程修改了(版本和执行初是否相同),没有修改则进行更新,否则放弃本次操作。

悲观锁的实现：

```java
//0.开始事务
begin;/begin work;/start transaction; (三者选一就可以)
//1.查询出商品信息
select status from t_goods where id=1 for update;
//2.根据商品信息生成订单
insert into t_orders (id,goods_id) values (null,1);
//3.修改商品status为2
update t_goods set status=2;
//4.提交事务
commit;/commit work;
```

乐观锁的实现

```java
1.查询出商品信息
select (status,status,version) from t_goods where id=#{id}
2.根据商品信息生成订单
3.修改商品status为2
update t_goods 
set status=2,version=version+1
where id=#{id} and version=#{version};
```

### 60、进程、线程

#### 进程

狭义：进程是正在运行的程序的实例。

广义：进程是一个具有一定独立功能的程序，关于某个数据集合的一次运行活动。

进程是操作系统动态执行的基本单元，在传统的操作系统中， 进程即是基本的分配单元，也是基本的执行单元。

#### 线程

线程是操作系统能够进行运算调试的最小单位。它被包含在进程中，是进程中的实际动作单位。一个线程指的是进程中的一个单一顺序的控制流，一个进程中可以并发多个线程，每个线程执行不同的任务。

1.1.3 多线程的优点

1. 可以把占据时间较长的任务放到后台去处理
2. 程序的运行速度加快

#### 使用多线程

##### 继承Thread

步骤：

1. 创建一个类，这个类需要继承Thread
2. 重写Thread类的run方法（业务代码）
3. 实例化创建好的线程类
4. 调用实例化对象的start方法启动线程

```java
package chap1;

public class Demo02 {
    public static void main(String[] args) {
        Thread t = new Demo02Thread();
        t.start();  // 启动线程
        System.out.println("运行了main方法");
    }
}

class Demo02Thread extends Thread{
    @Override
    public void run() {
        System.out.println("运行了run方法");
    }
}
```

线程运行具有以下特点

1. 随机性

```java
package chap1;

public class Demo03 {
    public static void main(String[] args) {
        Thread t = new Demo03Thread();
        t.start();
        try {
            for (int i = 0; i < 10; i++) {
                System.out.println("运行main方法");
                Thread.sleep(100);
            }
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
}

class Demo03Thread extends Thread{
    @Override
    public void run() {
        try {
            for (int i = 0; i < 10; i++) {
                System.out.println("运行run方法");
                Thread.sleep(100);
            }
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
}
```

在多线程编程中，代码的执行结果与代码的执行顺序或调用顺序是无关的。线程是一个子任务，CPU以不确定的方式或者是以随机的时间来调用线程中的run方法。

如果直接调用线程对象的run方法，不是启动线程，而是由main主线程来调用run方法。

2. start的执行顺序与线程的启动顺序不一致

```java
package chap1;

public class Demo04 {
    public static void main(String[] args) {
        Thread t1 = new Demo04Thread(1);
        Thread t2 = new Demo04Thread(2);
        Thread t3 = new Demo04Thread(3);
        Thread t4 = new Demo04Thread(4);
        Thread t5 = new Demo04Thread(5);
        t1.start();
        t2.start();
        t3.start();
        t4.start();
        t5.start();
    }
}

class Demo04Thread extends Thread{
    private int val;
    public Demo04Thread(int val){
        this.val = val;
    }

    @Override
    public void run() {
        System.out.println("val=" + val);
    }
}
```

##### 实现Runnable接口

步骤：

1. 创建一个类，这个类需要实现Runnable接口
2. 重写Runnable接口的run方法
3. 实例化创建的这个类
4. 实例化一个Thread对象，并把第3步创建的对象通过Thread的构造方法进行传递 
5. 调用Thread对象的start方法

```java
package chap1;

public class Demo05 {
    public static void main(String[] args) {
        Runnable r = new Demo05Thread();
        Thread t = new Thread(r);
        t.start();
        System.out.println("运行了main方法");
    }
}

class Demo05Thread implements Runnable{
    @Override
    public void run() {
        System.out.println("运行了run方法");
    }
}
```

使用Thread继承的方式开发多线程应用程序是有局限的，Java是单继承，为了改变这种限抽，可以使用Runnable接口方式来实现多线程。

##### Callable接口

Runnable是执行工作的独立任务，但是它不返回任何值。如果希望任务在完成的同时能够返回一个值，可以通过实现Callable接口。在JDK5.0中引入的Callable接口是一种具有类型参数的泛型，它的类型参数表示从方法call中返回的值的类型。

```
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class Demo05 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        Callable<Integer> callable = new Demo05Callable();
        FutureTask<Integer> task = new FutureTask<>(callable);
        Thread t1 = new Thread(task);
        t1.start();
        System.out.println("线程返回的值是：" + task.get());
    }
}

class Demo05Callable implements Callable<Integer>{
    @Override
    public Integer call() throws Exception {
        System.out.println(Thread.currentThread().getName() + "调用了callable接口的实现类");
        int val = (int)(Math.random() * 10);
        System.out.println("准备返回的值是：" + val);
        return val;
    }
}
```

### 61、在JAVA中如何跳出当前的多重嵌套循环？

在Java中，要想跳出多重循环，可以在外面的循环语句前定义一个标号，然后在里层循环体的代码中使用带有标号的break语句，即可跳出外层循环。比如：

```java
for(int i=0;i<10;i++){
 for(intj=0;j<10;j++){
   System.out.println(“i=” + i + “,j=” + j);
   if(j == 5) break ok;
 }
}
```

另外还有一个标号的方式，它是让外层的循环条件表达式的结果可以受到里层循环体代码的控制，例如，要在二维数组中查找到某个数字。

```
int arr[][] ={{1,2,3},{4,5,6,7},{9}};
boolean found = false;
for(int i=0;i<arr.length&&!found;i++)    {
    for(intj=0;j<arr[i].length;j++){
       System.out.println(“i=” + i + “,j=” + j);
       if(arr[i][j] ==5) {
           found =true;
           break;
      }
   }
}
```

### 62、short s1= 1; s1 = （s1+1是int类型，而等号左边的是short类型，所以需要强转）1 + 1;有什么错? short s1 = 1; s1 += 1;有什么错?(没有错)

对于short s1= 1; s1 = s1 + 1;由于s1+1运算时会自动提升表达式的类型，所以结果是int型，再赋值给short类型s1时，编译器将报告需要强制转换类型的错误。
对于short s1= 1; s1 += 1;由于 +=是java语言规定的运算符，java编译器会对它进行特殊处理，因此可以正确编译。

### 63、char型变量中能不能存贮一个中文汉字?为什么?

char型变量是用来存储Unicode编码的字符的，unicode编码字符集中包含了汉字，所以，char型变量中当然可以存储汉字啦。不过，如果某个特殊的汉字没有被包含在unicode编码字符集中，那么，这个char型变量中就不能存储这个特殊汉字。补充说明：unicode编码占用两个字节，所以，char类型的变量也是占用两个字节。

### 64、使用final关键字修饰一个变量时，是引用不能变，还是引用的对象不能变？

使用final关键字修饰一个变量时，是指引用变量不能变，引用变量所指向的对象中的内容还是可以改变的。例如，对于如下语句：

```
finalStringBuffer a=new StringBuffer("immutable");
```

执行如下语句将报告编译期错误：

```
a=new StringBuffer("");
```

但是，执行如下语句则可以通过编译：

```
a.append(" broken!");
```

有人在定义方法的参数时，可能想采用如下形式来阻止方法内部修改传进来的参数对象：

```
public void method(final StringBuffer param){
}
```

实际上，这是办不到的，在该方法内部仍然可以增加如下代码来修改参数对象：

```
param.append("a");
```

### 65、静态变量和实例变量的区别？

在语法定义上的区别：静态变量前要加static关键字，而实例变量前则不加。
在程序运行时的区别：实例变量属于某个对象的属性，必须创建了实例对象，其中的实例变量才会被分配空间，才能使用这个实例变量。静态变量不属于某个实例对象，而是属于类，所以也称为类变量，只要程序加载了类的字节码，不用创建任何实例对象，静态变量就会被分配空间，静态变量就可以被使用了。总之，实例变量必须创建对象后才可以通过这个对象来使用，静态变量则可以直接使用类名来引用。
例如，对于下面的程序，无论创建多少个实例对象，永远都只分配了一个staticVar变量，并且每创建一个实例对象，这个staticVar就会加1；但是，每创建一个实例对象，就会分配一个instanceVar，即可能分配多个instanceVar，并且每个instanceVar的值都只自加了1次。

```java
int arr[][] ={{1,2,3},{4,5,6,7},{9}};
boolean found = false;
for(int i=0;i<arr.length&&!found;i++)    {
    for(intj=0;j<arr[i].length;j++){
       System.out.println(“i=” + i + “,j=” + j);
       if(arr[i][j] ==5) {
           found =true;
           break;
      }
   }
}
```

### 66、是否可以从一个static方法内部发出对非static方法的调用？

不可以。

因为非static方法是要与对象关联在一起的，必须创建一个对象后，才可以在该对象上进行方法调用，而static方法调用时不需要创建对象，可以直接调用。也就是说，当一个static方法被调用时，可能还没有创建任何实例对象，如果从一个static方法中发出对非static方法的调用，那个非static方法是关联到哪个对象上的呢？这个逻辑无法成立，所以，一个static方法内部发出对非static方法的调用。

### 67、List,Set, Map是否继承自Collection接口?

List，Set是，Map不是！

### 68、List、Map、Set三个接口，存取元素时，各有什么特点？

首先，List与Set具有相似性，它们都是单列元素的集合，所以，它们有一个共同的父接口，叫Collection。

Set里面不允许有重复的元素，即不能有两个相等（注意，不是仅仅是相同）的对象，即假设Set集合中有了一个A对象，现在我要向Set集合再存入一个B对象，但B对象与A对象equals相等，则B对象存储不进去，所以，Set集合的add方法有一个boolean的返回值，当集合中没有某个元素，此时add方法可成功加入该元素时，则返回true，当集合含有与某个元素equals相等的元素时，此时add方法无法加入该元素，返回结果为false。Set取元素时，不能细说要取第几个，只能以Iterator接口取得所有的元素，再逐一遍历各个元素。

List表示有先后顺序的集合，注意，不是那种按年龄、按大小、按价格之类的排序。当我们多次调用add(Obje)方法时，每次加入的对象就像火车站买票有排队顺序一样，按先来后到的顺序排序。有时候，也可以插队，即调用add(intindex,Obj e)方法，就可以指定当前对象在集合中的存放位置。一个对象可以被反复存储进List中，每调用一次add方法，这个对象就被插入进集合中一次，其实，并不是把这个对象本身存储进了集合中，而是在集合中用一个索引变量指向这个对象，当这个对象被add多次时，即相当于集合中有多个索引指向了这个对象。List除了可以用Iterator接口取得所有的元素，再逐一遍历各个元素之外，还可以调get(index i)来明确说明取第几个。

Map与List和Set不同，它是双列的集合，其中有put方法，定义如下：put(obj key,obj value)，每次存储时，要存储一对key/value，不能存储重复的key，这个重复的规则也是按equals比较相等。取则可以根据key获得相应的value，即get(Object key)返回值为key所对应的value。另外，也可以获得所有的key的结合，还可以获得所有的value的结合，还可以获得key和value组合成的Map.Entry对象的集合。

List以特定次序来持有元素，可有重复元素。Set无法拥有重复元素,内部序。Map保存key-value值，value可多值。

### 69、ArrayList,Vector,LinkedList的存储性能和特性

ArrayList和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，Vector由于使用了synchronized方法（线程安全），通常性能上较ArrayList差。而LinkedList使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历，索引就变慢了，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。LinkedList也是线程不安全的，LinkedList提供了一些方法，使得LinkedList可以被当作堆栈和队列来使用。

### 70、如何去掉一个Vector集合中重复的元素

```
Vector newVector = new Vector();
For (int i=0;i<vector.size();i++)
{
Object obj = vector.get(i);
   if(!newVector.contains(obj);
      newVector.add(obj);
}
```

还有一种简单的方式，利用了Set不允许重复元素：

```
HashSetset = new HashSet(vector);
```

### 71、集合类都有哪些？主要方法？
最常用的集合类是 List 和 Map。 

List的具体实现包括 ArrayList和 Vector，它们是可变大小的列表，比较适合构建、存储和操作任何类型对象的元素列表。

List适用于按数值索引访问元素的情形。Map 提供了一个更通用的元素存储方法。 Map集合类用于存储元素对（称作"键"和"值"），其中每个键映射到一个值。它们都有增删改查的方法。

对于set，大概的方法是add,remove, contains等对于map，大概的方法就是put,remove，contains等List类会有get(int index)这样的方法，因为它可以按顺序取元素，而set类中没有get(int index)这样的方法。List和set都可以迭代出所有元素，迭代时先要得到一个iterator对象，所以，set和list类都有一个iterator方法，用于返回那个iterator对象。

map可以返回三个集合，一个是返回所有的key的集合，另外一个返回的是所有value的集合，再一个返回的key和value组合成的EntrySet对象的集合，map也有get方法，参数是key，返回值是key对应的value。

### 72、a.hashCode() 有什么用？与 a.equals(b) 有什么关系？
hashCode() 方法对应对象整型的 hash 值。它常用于基于 hash 的集合类，如 Hashtable、HashMap、LinkedHashMap等等。它与 equals() 方法关系特别紧密。根据 Java 规范，两个使用equal() 方法来判断相等的对象，必须具有相同的 hash code。

### 73、字节流与字符流的区别

要把一段二进制数据数据逐一输出到某个设备中，或者从某个设备中逐一读取一段二进制数据，不管输入输出设备是什么，我们要用统一的方式来完成这些操作，用一种抽象的方式进行描述，这个抽象描述方式起名为IO流，对应的抽象类为OutputStream和InputStream，不同的实现类就代表不同的输入和输出设备，它们都是针对字节进行操作的。计算机中的一切最终都是二进制的字节形式存在。对于经常用到的中文字符，首先要得到其对应的字节，然后将字节写入到输出流。读取时，首先读到的是字节，可是我们要把它显示为字符，我们需要将字节转换成字符。由于这样的需求很广泛，Java专门提供了字符流包装类。底层设备永远只接受字节数据，有时候要写字符串到底层设备，需要将字符串转成字节再进行写入。字符流是字节流的包装，字符流则是直接接受字符串，它内部将串转成字节，再写入底层设备，这为我们向IO设备写入或读取字符串提供了一点点方便。字符向字节转换时，要注意编码的问题，因为字符串转成字节数组，其实是转成该字符的某种编码的字节形式，读取也是反之的道理

### 74、什么是java序列化，如何实现java序列化？或者请解释Serializable接口的作用。

我们有时候将一个java对象变成字节流的形式传出去或者从一个字节流中恢复成一个java对象，例如，要将java对象存储到硬盘或者传送给网络上的其他计算机，这个过程我们可以自己写代码去把一个java对象变成某个格式的字节流再传输。但是，jre本身就提供了这种支持，我们可以调用OutputStream的writeObject方法来做，如果要让java帮我们做，要被传输的对象必须实现serializable接口，这样，javac编译时就会进行特殊处理，编译的类才可以被writeObject方法操作，这就是所谓的序列化。需要被序列化的类必须实现Serializable接口，该接口是一个mini接口，其中没有需要实现方法，implements Serializable只是为了标注该对象是可被序列化的。例如，在web开发中，如果对象被保存在了Session中，tomcat在重启时要把Session对象序列化到硬盘，这个对象就必须实现Serializable接口。如果对象要经过分布式系统进行网络传输，被传输的对象就必须实现Serializable接口。

### 75、**一个".java"源文件中是否可以包括多个类（不是内部类）？有什么限制？** 

可以有多个类，但只能有一个public的类，并且public的类名必须与文件名相一致。

### 76、Java有没有goto?

java中的保留字，现在没有在java中使用。

### 77、switch语句能否作用在byte上，能否作用在long上，能否作用在String上?

在switch（expr1）中，expr1只能是一个整数表达式或者枚举常量（更大字体），整数表达式可以是int基本类型或Integer包装类型，由于，byte,short,char都可以隐含转换为int，所以，这些类型以及这些类型的包装类型也是可以的。显然，long和String类型都不符合switch的语法规定，并且不能被隐式转换成int类型，所以，它们不能作用于swtich语句中。 

### 78、静态变量和实例变量的区别？

在语法定义上的区别：静态变量前要加static关键字，而实例变量前则不加。

在程序运行时的区别：实例变量属于某个对象的属性，必须创建了实例对象，其中的实例变量才会被分配空间，才能使用这个实例变量。静态变量不属于某个实例对象，而是属于类，所以也称为类变量，只要程序加载了类的字节码，不用创建任何实例对象，静态变量就会被分配空间，静态变量就可以被使用了。总之，实例变量必须创建对象后才可以通过这个对象来使用，静态变量则可以直接使用类名来引用。

例如，对于下面的程序，无论创建多少个实例对象，永远都只分配了一个staticVar变量，并且每创建一个实例对象，这个staticVar就会加1；但是，每创建一个实例对象，就会分配一个instanceVar，即可能分配多个instanceVar，并且每个instanceVar的值都只自加了1次。

```
public class VariantTest

{

		public static int staticVar = 0; 

		public int instanceVar = 0; 

		public VariantTest()

		{

			staticVar++;

			instanceVar++;

			System.out.println(“staticVar=” + staticVar + ”,instanceVar=” + instanceVar);

		}

}
```

### 79、是否可以从一个static方法内部发出对非static方法的调用？

不可以。因为非static方法是要与对象关联在一起的，必须创建一个对象后，才可以在该对象上进行方法调用，而static方法调用时不需要创建对象，可以直接调用。也就是说，当一个static方法被调用时，可能还没有创建任何实例对象，如果从一个static方法中发出对非static方法的调用，那个非static方法是关联到哪个对象上的呢？这个逻辑无法成立，所以，一个static方法内部发出对非static方法的调用。

### 80、Integer与int的区别

int是java提供的8种原始数据类型之一。Java为每个原始类型提供了封装类，Integer是java为int提供的封装类。int的默认值为0，而Integer的默认值为null，即Integer可以区分出未赋值和值为0的区别，int则无法表达出未赋值的情况，例如，要想表达出没有参加考试和考试成绩为0的区别，则只能使用Integer。在JSP开发中，Integer的默认为null，所以用el表达式在文本框中显示时，值为空白字符串，而int默认的默认值为0，所以用el表达式在文本框中显示时，结果为0，所以，int不适合作为web层的表单数据的类型。

在Hibernate中，如果将OID定义为Integer类型，那么Hibernate就可以根据其值是否为null而判断一个对象是否是临时的，如果将OID定义为了int类型，还需要在hbm映射文件中设置其unsaved-value属性为0。

另外，Integer提供了多个与整数相关的操作方法，例如，将一个字符串转换成整数，Integer中还定义了表示整数的最大值和最小值的常量。

### 81、Overload和Override的区别。Overloaded的方法是否可以改变返回值的类型?

Overload是重载的意思，Override是覆盖的意思，也就是重写。

重载Overload表示同一个类中可以有多个名称相同的方法，但这些方法的参数列表各不相同（即参数个数或类型不同）。

重写Override表示子类中的方法可以与父类中的某个方法的名称和参数完全相同，通过子类创建的实例对象调用这个方法时，将调用子类中的定义方法，这相当于把父类中定义的那个完全相同的方法给覆盖了，这也是面向对象编程的多态性的一种表现。子类覆盖父类的方法时，只能比父类抛出更少的异常，或者是抛出父类抛出的异常的子异常，因为子类可以解决父类的一些问题，不能比父类有更多的问题。子类方法的访问权限只能比父类的更大，不能更小。如果父类的方法是private类型，那么，子类则不存在覆盖的限制，相当于子类中增加了一个全新的方法。

至于Overloaded的方法是否可以改变返回值的类型这个问题，要看你倒底想问什么呢？这个题目很模糊。如果几个Overloaded的方法的参数列表不一样，它们的返回者类型当然也可以不一样。但我估计你想问的问题是：如果两个方法的参数列表完全一样，是否可以让它们的返回值不同来实现重载Overload。这是不行的，我们可以用反证法来说明这个问题，因为我们有时候调用一个方法时也可以不定义返回结果变量，即不要关心其返回结果，例如，我们调用map.remove(key)方法时，虽然remove方法有返回值，但是我们通常都不会定义接收返回结果的变量，这时候假设该类中有两个名称和参数列表完全相同的方法，仅仅是返回类型不同，java就无法确定编程者倒底是想调用哪个方法了，因为它无法通过返回结果类型来判断。 

override可以翻译为覆盖，从字面就可以知道，它是覆盖了一个方法并且对其重写，以求达到不同的作用。对我们来说最熟悉的覆盖就是对接口方法的实现，在接口中一般只是对方法进行了声明，而我们在实现时，就需要实现接口声明的所有方法。除了这个典型的用法以外，我们在继承中也可能会在子类覆盖父类中的方法。在覆盖要注意以下的几点：

1、覆盖的方法的标志必须要和被覆盖的方法的标志完全匹配，才能达到覆盖的效果；

2、覆盖的方法的返回值必须和被覆盖的方法的返回一致；

3、覆盖的方法所抛出的异常必须和被覆盖方法的所抛出的异常一致，或者是其子类；

4、被覆盖的方法不能为private，否则在其子类中只是新定义了一个方法，并没有对其进行覆盖。

overload对我们来说可能比较熟悉，可以翻译为重载，它是指我们可以定义一些名称相同的方法，通过定义不同的输入参数来区分这些方法，然后再调用时，VM就会根据不同的参数样式，来选择合适的方法执行。在使用重载要注意以下的几点：

1、在使用重载时只能通过不同的参数样式。例如，不同的参数类型，不同的参数个数，不同的参数顺序（当然，同一方法内的几个参数类型必须不一样，例如可以是fun(int,float)，但是不能为fun(int,int)）；

2、不能通过访问权限、返回类型、抛出的异常进行重载；

3、方法的异常类型和数目不会对重载造成影响；

4、对于继承来说，如果某一方法在父类中是访问权限是priavte，那么就不能在子类对其进行重载，如果定义的话，也只是定义了一个新方法，而不会达到重载的效果。

### 82、构造器Constructor是否可被override?

构造器Constructor不能被继承，因此不能重写Override，但可以被重载Overload。 

### 83、接口是否可继承接口? 抽象类是否可实现(implements)接口? 抽象类是否可继承具体类(concrete class)? 抽象类中是否可以有静态的main方法？

接口可以继承接口。抽象类可以实现(implements)接口，抽象类是否可继承具体类。抽象类中可以有静态的main方法。

 只有记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。