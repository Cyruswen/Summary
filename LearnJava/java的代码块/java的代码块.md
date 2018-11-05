### java的代码块

根据代码块定义的位置以及关键字代码块分为

- **普通代码块**
- **构造代码块**
- **静态代码块**
- **同步代码块**（暂时不看，后来介绍）

#### 1. 普通代码块

**定义在方法中的代码块。**

```java
public class TestMain {

	public static void main(String[] args) {
		{ //直接使用{}定义普通方法块
			int x = 10;
			System.out.println("x: " + x);
		}
		int x = 100;
		System.out.println("x: " + x);
	}
	
}
```

**如果方法中代码太长，为了避免变量重名，使用普通代码块。（有点类似C++中的命名空间）**

#### 2. 构造代码块

**构造块：定义在类中的代码块。**

```java
public class Person {
	{//定义在类中，不加修饰符构造块
		System.out.println("Person类的构造块");
	}
	
	public Person()
	{
		System.out.println("Person类的构造方法");
	}
}
```

执行结果：

> Person类的构造块
> Person类的构造方法

我们可以知道，代码块的执行优先于构造方法执行，每产生一个对象，先调用一次代码块，再调用构造方法。

#### 3.静态代码块

**静态代码块：static修饰的代码块**

- **在非主类中的静态代码块**

```java
public class Person
{
	{
		System.out.println("Person类的构造块");
	}
	
	public Person()
	{
		System.out.println("Person类的构造方法");
	}
	
	static
	{
		System.out.println("Person类的静态块");
	}
}

public class MainTest {

	public static void main(String[] args) {
		System.out.println("----- start -----");
		new Person();
		new Person();
		System.out.println("----- end ------");
	}
	
}

```

执行结果：

> ----- start -----
> Person类的静态块
> Person类的构造块
> Person类的构造方法
> Person类的构造块
> Person类的构造方法
> ----- end ------

我们可以发现：

1. 静态块的优先级高于构造块
2. 无论产生多少实例化的对象，静态块都执行一次。（这就是static的属性）

- **定义在主类中的代码块**

```java
public class MainTest {
	{
		System.out.println("MainTest的构造块");
	}
	
	public MainTest()
	{
		System.out.println("MainTest类的构造方法");
	}
	
	static
	{
		System.out.println("MainTest类的静态方法");
	}
	
	public static void main(String[] args)
	{
		System.out.println("----- start -----");
		new MainTest();
		new MainTest();
		System.out.println("----- end ------");
	}
}
```

执行结果：

> MainTest类的静态方法
> ----- start -----
> MainTest的构造块
> MainTest类的构造方法
> MainTest的构造块
> MainTest类的构造方法
> ----- end ------

**在主类中定义的静态块，优先于main方法执行**

