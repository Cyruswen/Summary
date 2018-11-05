# C/C++复习

### C/C++基础语法

1. static关键字作用
   1. 修饰变量
      - 存储位置 - 静态存储区
      - 链接属性，本文件内有效
   2. 修饰函数
      - 链接属性 - 本文件内有效
   3. 修饰成员变量和成员函数
      - 静态成员函数没有this指针， 类和对象都可以调用
      - 静态成员函数不能是虚函数
      - 静态成员变量必须在类外初始化
2. static和全局的区别
3. const的作用 
   - 修饰变量不能被修改，指针可以修改但是注意编译器优化（volatile)
   - const修饰引用、指针
   - const修饰成员函数（this指针指向的对象，所以不可以修饰全局函数和静态成员函数）
4. volatile的作用
5. 宏
   - 实现一个Add + 宏的优缺点。  关联知识（const/enum/inline替代宏）
6. 指针和引用的区别
7. sizeof/strlen
8. C语言常见的库函数 （memcpy 、 memmove  + strxxx + atoi/itoa)
9. 指针和数组相关
10. 重载的原理 -- 函数名修饰规则 -- extern c
11. 四个默认成员函数的理解 
    - 构造函数的初始化列表
12. C的内存管理和C++的内存管理
    - 什么是内存泄漏，危害是什么？内存没有释放，申请不下来内存
    - 如何检测内存泄漏？ -- >工具（valgrind)
    - 如何解决？  (良好的变成习惯、RAII)
13. String类（深浅拷贝  引用计数的写时拷贝）
14. 继承和多态
    - 菱形继承 -- 缺陷（数据冗余、二义性）
      - 如何解决：虚继承。 虚基表
    - 隐藏（重定义）/覆盖（重写）/重载
    - 什么是多态？多态的原理是什么?
15. 泛型编程
    - 什么是泛型编程？ -- 解放了生产力、提高复用率
    - 实现一个模板函数
    - 模板的分离编译
    - 模板的原理及使用
16. 智能指针
    - 什么是RAII
    - 智能指针的分类及发展历史
    - auto_ptr/unique_ptr/shared_ptr + weak_ptr
    - 循环引用
17. **其他：**
    - 异常优缺点
    - 四个强制类型的转换
    - RTTI   typeid/dynamic_cast

- STL:

  - 熟悉常见容器的使用 
    - string/vector/list/stack/queue/priorty_queue/map/set/unorderd_map/unorderd_set/bit_set
  - 常见算法的使用
    - find/sort/next_permutation
    - vector/list/map/set/unordered_map/unorderd_set原理
    - 什么是迭代器及其失效问题

- C++11

  - 说一下你熟悉的c++11语法
  - auto的作用，优缺点
    - 优点：简化代码
    - 缺点：可读性变差

  

  ![1534584900623](C:\Users\kaikai\AppData\Local\Temp\1534584900623.png)

  ```c++
  int array[] = {1,3,4,5,6,7};
  for(auto e : array)
  {
      cout<< e <<endl;
  }
  ```

  ```c++
  list<int> lt{1,2,3,4}
  for(auto e : lt)
  {
      cout<< e <<endl;
  }
  ```

  ```c++
  list<int> lt{1,2,3,4};
  //加引用才可以修改值
  for(auto& e : lt)
  {
      if(e % 2 == 0)
      {
          e *= 2;
      }
      cout<< e <<endl;
  }
  ```

  ```c++
  void countstr(vector<string>& v)
  {
      unorderd_map<string, int> coutmap;
      for(auto& e : v)
      {
          coutmap[e]++;
      }
      
      for(auto& e : coutmap)
      {
          cout<< "e.first: "<<e.first<<endl<<"e.second:"<<e.second<<endl;
      }
  }
  ```

  

### C/C++的区别

1. malloc/free 和 new/delete的区别

2. 面向对象和面向过程的理解。 面向对象的三大特性（封装、继承、多态）

   - **封装**      其实就是管理，例如火车站，封装一些方法，提供通道访问。
   - **继承**      类级别的复用
   - **多态**      静态的多态：重载                动态的多态：根据对象调用函数

   

### 计算机体系相关

1. 编译链接
2. 函数调用栈帧
3. 进程地址空间相关