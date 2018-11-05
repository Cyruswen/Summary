### C++是如何实现多态的

1. 存在继承关系
2. 子类重写父类的虚函数
3. 父类的指针或引用指向子类对象

```c++
#include <iostream>
using namespace std;

class Myparent
{
public:
	Myparent()
	{
		cout << "我是爸爸的构造函数" << endl;
	}

	virtual void print()
	{
		cout << "我是爸爸的print" << endl;
	}
};

class Mychild : public Myparent
{
public:
	Mychild()
	{
		cout << "我是儿子的构造函数" << endl;
	}

	virtual void print()
	{
		cout << "我是儿子的print" << endl;
	}
};

class Mychildchild : public Mychild
{
public:
	Mychildchild()
	{
		cout << "我是孙子的构造函数" << endl;
	}

	virtual void print()
	{
		cout << "我是孙子的print" << endl;
	}
};

void howprint(Myparent& base)
{
	base.print();
}

int main()
{
	Myparent p;
	Mychild c;
	howprint(p);
	howprint(c);
	Mychildchild cc;
	howprint(cc);
	system("pause");
	return 0;
}
```

![](D:\图片\markimg\QQ截图20180818000800.png)