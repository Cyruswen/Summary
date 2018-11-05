## C++强制类型转换

C语言

- 隐式类型转换 -- 相关类型  
- 强制类型转换 -- 不相关类型  

C++

- static_cast
- reinterpret_cast
- dynamic_cast

```c
void Test()
{
	int i = 1;
    //隐式类型转换
	double d = i;
	printf("%d %.2f\n",i, d);
	int* p = &i;
    //显示类型转换
	int address = (int)p;
	printf("%x, %d\n", p, address);
}
```

**RAII**: 构造函数初始化与保存资源，析构函数自动释放资源。也称为“资源获取就是初始化”，是c++等编程语言常用的管理资源、避免内存泄露的方法。它保证在任何情况下，使用对象时先构造对象，最后析构对象。 

**RTTI**：（Run-Time Type Identification ) 通过运行时类型信息程序能够使用[基类](https://baike.baidu.com/item/%E5%9F%BA%E7%B1%BB/9589663)的[指针](https://baike.baidu.com/item/%E6%8C%87%E9%92%88/2878304)或引用来检查这些指针或引用所指的对象的实际[派生类](https://baike.baidu.com/item/%E6%B4%BE%E7%94%9F%E7%B1%BB)型。

```c++
typeid(a).name()
```

#### **static_cast**

> static_cast用于非多态类型的转换（静态转换），任何标准转换都可以用它，但是不可以用于两个不相关的类型进行转换。

```c++
void Test()
{
	int i = 1;
	double d = static_cast<double>(i);
	printf("%d %.2f\n",i, d);
}
```

#### **reinterpret_cast**

> reinterpret_cast用于将一种类型转换为不同的类型。

```c
typedef void (*Func)();

int Dosomething(int i)
{
	cout<<"Dosomething"<<endl;
	return 1;
}

void Test()
{
	Func f = reinterpret_cast<Func>(Dosomething);
	f();
}
```

> reinterpret_cast<T>( )

> T 必须是一个指针、引用、算术类型、函数指针或者成员指针。它可以把一个指针转换成一个整数，也可以把一个整数转换成一个指针（先把一个指针转换成一个整数，再把该整数转换成原类型的指针，还可以得到原先的指针值）。 

> reinterpret_cast是为了映射到一个完全不同类型的意思，这个关键词在我们需要把类型映射回原有类型时用到它。我们映射到的类型仅仅是为了故弄玄虚和其他目的，这是所有映射中最危险的。(这句话是C++编程思想中的原话) 

> 也就是说需要传参的函数在经过reinterpret_cast强制转换之后不传参数也可以调用。

reinterpret_cast和static_cast的主要区别在多重继承。例如：

```c
class A
{
	int m_a;
};

class B
{
	int m_b;
};

class C : public A, public B
{};

int main()
{
	C c;
	printf("%p  %p  %p\n", &c, reinterpret_cast<B*>(&c), static_cast<B*>(&c));
	system("pause");
}
```

![1534062993681](C:\Users\kaikai\AppData\Local\Temp\1534062993681.png)

> 上面这段代码中， 前两个输出值相同，第三个偏移了四个字节，这是因为[static_cast](https://baike.baidu.com/item/static_cast)计算了父子类[指针](https://baike.baidu.com/item/%E6%8C%87%E9%92%88)转换的[偏移量](https://baike.baidu.com/item/%E5%81%8F%E7%A7%BB%E9%87%8F)，并将之转换到正确的地址（c里面有m_a,m_b，转换为B*指针后指到m_b处），reinterpret_cast却不会做这一层转换。 

**慎用reinterpret_cast**

#### const_cast

const_cast最常用的属性就是删除变量的const属性，方便赋值。

```c
int main()
{
	volatile const int a = 2;
    //volatile避免值被编译器优化到寄存器
	int* p = const_cast<int*>(&a);
	*p = 3;
	cout<<a<<endl;
	system("pause");
}
```

#### dynamic_cast

dynamic_cast用于将一个父类对象的指针转换为子类对象的指针或引用（动态转换）

1. dynamic_cast只能用于含有虚类的函数
2. dynamic_cast会先检查是否能成功转换，能转换则转换，如果不能则返回。

 **虚函数重写时，传入的父类的指针或引用，这个指针有两种情况。**

- 本来是子类的指针切片之后的父类指针。
- 本来是父类指针。

如果是第一种情况传入的父类指针强转成子类指针没有问题，但是第二种情况父类的指针强转成子类指针就会造成越界。所以转换的时候需要检测指针的类型，这时候就有了dynamic_cast。

```c
class A
{
public:
	virtual void Func(){}
};

class B : A
{};

void fun(A* pa)
{
	//B* pb1 = static_cast<B*>(pa);
	B* pb2 = dynamic_cast<B*>(pa);
	//cout<<"pb1:"<<pb1<<endl;
	cout<<"pb2:"<<pb2<<endl;
}

int main()
{
	A a;
	B b;
	fun(&a);
	//fun(&b);
	system("pause");
	return 0;
}
```

#### explicit关键字

explicit关键字阻止经过转换构造函数进行的隐式转换的发生。

**C++ 单参数的构造函数的类支持隐式类型转换**

注意单参数构造函数才可以使用

智能指针就使用了explicit防止隐形类型转化

```c
class C
{
public:
	//不想让隐式转换的发生
	explicit C(int c)
		:_c(c)
		{}
	//C(int c)	//单参数类型的构造函数支持隐式类型的转换
	//:_c(c)
	//{}
private:
	int _c;
};

int main()
{
    C c1(10);
    C c2 = 20;	//隐式类型转换
    //1. 拿20构造一个匿名对象 C（20）
    //2. 拷贝构造
    //3. 编译器优化为一个构造函数
    return 0;
}
```



