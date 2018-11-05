## this关键字的作用

##### this关键字主要有以下三种用途

1. this调用本类属性
2. this调用本类方法
3. this表示当前对象

#### 1. this调用本类属性

我们可以看如下代码：

```java
public class Person {
	private String name;
	private int age;
	
	public Person(String name, int age)
	{
		name = name;
		age = age;
	}
	
	public void printInfo()
	{
		System.out.println("name: " + name + " age: " + age);
	}
}
```

我们发现参数与类中属性重名的时候，类中属性无法正常赋值。这个时候我们加上this关键字就可以解决这个问题。所以，java中访问累的属性，一定要加上this关键字。

```java
public Person(String name, int age)
	{
		this.name = name;
		this.age = age;
	}
```

#### 2. this调用本类方法

- **调用普通方法**

```java
public class Person {
	private String name;
	private int age;
	
	public Person(String name, int age)
	{
		this.name = name;
		this.age = age;
		this.printSth();
	}
	
	public void printSth()
	{
		System.out.println("************************");
	}
}
```

在继承中，强烈建议调用类的方法时加上this, 虽然也可以不加，但是在涉及到继承的时候有用。

- **this在构造函数中的使用**

观察下面的代码

```java
public class Person {
	private String name;
	private int age;
	
	public Person()  //无参构造函数
	{
		System.out.println("new了一个新对象");
	}
	
	public Person(String name)
	{
		System.out.println("new了一个新对象");
		this.name = name;
	}
	
	public Person(String name, int age)
	{
		System.out.println("new了一个新对象");
		this.name = name;
		this.age = age;
	}
    
    public void printInfo()
	{
		System.out.println("name: " + name + " age: " + age);
	}
}


public class TestMain {

	public static void main(String[] args) {
		Person per1 = new Person();
		Person per2 = new Person("kaikai");
		Person per3 = new Person("kaikai", 23);
		per1.printInfo();
		per2.printInfo();
		per3.printInfo();
	}
}
```

java，支持构造方法相互调用。但是使用时要注意以下两点。

> 1. this调用构造方法的语句必须在构造方法首行。
> 2. 使用this调用构造方法，一定要注意留出口，不要陷入死循环。

```java
public Person()
	{
		System.out.println("new了一个新对象");
	}
	
	public Person(String name)
	{
		this();
		this.name = name;
	}
	
	public Person(String name, int age)
	{
		this(name);
		this.age = age;
	}
```

#### 使用this表示当前对象。

```java
class Person
{
	public void printSth()
	{
		System.out.println("Print方法：" + this);
	}
}

public class TestMain {

	public static void main(String[] args) {
		Person per1 = new Person();
		System.out.println("Main方法：" + per1);
		per1.printSth();
		Person per2 = new Person();
		System.out.println("Main方法：" + per2);
		per2.printSth();
	}
}

```

我们发现，一个对象调用本类的方法，那类里的this就表示调用方法的对象。



如上，万事如意。