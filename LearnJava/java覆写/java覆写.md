## 覆写

#### 1. 什么是覆写？

**子类定义了和父类相同的方法或者属性时候，这样的操作叫做覆写。**

#### 2. 方法的覆写

>  子类定义了与父类方法名称，参数类型个数完全相同的方法。但是覆写的方法不能有比父类的方法更严格的访问权限。

如：

```java
public class Person {

	public void print()
	{
		System.out.println("Preson的print方法");
	}
}

public class Student extends Person{
    //子类对父类的print方法进行覆写
	@Override
	public void print()
	{
		System.out.println("Student的print");
	}
}

public class TestMain {

	public static void main(String[] args) {
		Student stu = new Student();
		stu.print();
	}

}
```

>  **进行覆写的时候我们需要注意的是子类覆写方法的权限不能够更加严格， 且private < default < public ， 所以当父类的方法是public时，子类覆写的方法只能是public。父类方法是default时， 子类覆写的方法可以是default或者public。**

**那么， 当父类的方法是private， 子类覆写的方法为public时会有什么结果呢？**

父类是private时，该方法对于子类来说并不能直接使用，所以子类定义新的方法属于新的定义和父类没关系。

<imag src="test.img" width="400">

**3. 属性的覆写**

因为父类中属性一般都写成private， 所以属性的覆写了解即可。

**4. super关键字**

> 使用super( )  调用可以调用父类的构造方法，也可以使用super关键字调用父类的属性。

```java
	public class Person
	{
		public String name = "kaikai";
		public int age = 22;
	}

	public class Student extends Person
	{
		public String name = "machenpei";
		public void print()
		{
			System.out.println(super.name); //调用父类的name属性
			System.out.println(this.name); //调用当前类的name属性
		}
	}
	
	public class TestMain
    {
    	public static void main(String[] args)
        {
            Student stu = new Student();
            stu.print();
        }
    }
```

**5. final关键字**

**java中final被称为终结器， final可以修饰类、方法、属性。**

- final修饰的类不能有子类。

```java
final class A{}
```

- final 修饰的方法不能被子类覆写。

```java
class A
{
    public final void print()
    {
	}
}
```

- final修饰变量的时候， 变量就成了常量， 并且必须初始化，不能被修改。开发中， 常量声明必须要大写。

```java
class A
{
	public final int AGE = 20；
}
```



