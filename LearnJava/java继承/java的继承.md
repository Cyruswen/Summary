### java的继承

#### 1. java中继承的关键字是extends, 其实现的形式是:

> #### class Child extends Father{ }

**继承的主要作用就是对类进行扩充以及代码的复用。**

**继承的简单例子：**

```java
public class Person {
	private String name;
	private int age;
	
	public void setName(String name)
	{
		this.name = name;
	}
	
	public String getName()
	{
		return name;
	}
	
	public void setAge(int age)
	{
		this.age = age;
	}
	
	public int getAge()
	{
		return age;
	}
}

public class Student extends Person{
}

public class TestMain {
	public static void main(String[] args)
	{
		Student stu = new Student();
		stu.setName("kaikai");
		stu.setAge(18);
		System.out.println(stu.getName() + ": " + stu.getAge());
	}
}
```

根据上面的代码我们可以发现子类可以直接继承父类的方法和属性，实现代码的复用。子类最低也可以维持和父类相同的功能，。当然子类也可以对属性和方法进行扩充。如下：

```java
public class Student extends Person{
	private String ID;   //扩充了新的属性
	public void setId(String ID)
	{
		this.ID = ID;
	}
	
	public String getId()
	{
		return ID;
	}
}

public class TestMain {
	public static void main(String[] args)
	{
		Student stu = new Student();
		stu.setName("kaikai");
		stu.setAge(23);
		stu.setId("201505050418");
		System.out.println("姓名：" + stu.getName() + "\n年龄：" + stu.getAge() + "\n学号：" + stu.getId());
	}
}
```

#### 2. 继承的规( 限 )范( 制 )

- **子类在实例化对象时会首先实例化父类对象。也就是首先调用父类的构造方法再调用子类的构造方法去初始化**。

```java
public class Person {
	public Person()
	{
		System.out.println("调用父类的构造方法");
	}
}

public class Student extends Person
{
    public Student()
    {
    	super();  //在无参数的时候，super()写不写效果一样
    	System.out.println("调用子类的构造方法");
	}
}

public MainTest
{
	public static void main(String[] args)
    {
    	Student stu = new Student();
    }
}
```

执行结果：

> 调用父类的构造方法
> 调用子类的构造方法

- **java只允许单继承不允许多重继承， 但是允许多层继承，建议不超过三层。**

```java
class A{}
class B{}
class C extends A, B{}
```

上面的继承当然是错误的。那么问题来了，要是想让C既有A的属性，又有B的属性怎么办呢？

那就只能让C当孙子了。^_^

```java
class A{}
class B extends A{}
class C extends B{}
```

- **继承的时候我们需要注意的是， 子类会继承父类所有的属性（包括私有属性、构造方法、普通方法）， 所有的非私有属性子类都可以直接调用，所有私有的属性，子类需要借助其它方法调用。**

如下，显式继承和隐式继承。

```java
public class Person {
	public String name = "kaikai";
	private int age = 21;
	
	public void setAge(int age)
	{
		this.age = age;
	}
	
	public int getAge()
	{
		return age;
	}
}

public class Student extends Person{
}

public class TestMain {

	public static void main(String[] args) {
		Student stu = new Student();
		stu.setAge(22);
		System.out.println("Student Name:" + stu.name);    //显式继承，可以直接调用
         System.out.println("Student Age:" + stu.getAge());   //隐式继承， 需要调用别的方法访问
	}

}
```



**继承总结**：

1. 继承的语法以及继承的目的（扩展已有类的功能，使代码重用） 
2. 子类对象的实例化流程：不管如何操作，一定要先实例化父类对象。 
3. 不允许多重继承，只允许多层继承。 

