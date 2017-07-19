---
layout:   post
title:    "Effective C++ 一"
subtitle: "C++"
date:     2017-07-16
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - C++
---

### Effecive C++

1. 对象class A的构造函数被声明为explicit，这可阻止它们被用来执行隐式类型转换，但它仍可被用来进行显式类型转换。

   > ```c++
   > class A {
   >   A(int a);
   > }
   > int Function(A, a);
   > Function(2); //2会隐式转换为A类型。
   >
   > class A {
   >   explicit A(int a);
   > }
   > int Function(A, a);
   > Function(2); //编译器会给出错误信息。
   > Function(A(2)); //right
   > ```

2. 条款2:尽量以const、enum、inline替换define

   > 1. 对于单纯变量，最好以const对象或enum替换define
   > 2. 对于形似函数的宏，最好改用inline函数替换#define

3. 条款3:尽可能使用const

   > 1. const允许指定一个语义约束。
   >
   >    ```c++
   >    char greeting[] = "hello";
   >    const char *p = greeting;         //non-const pointer,const data
   >    char* const p = greeting;         //const pointer, non-const data
   >    const char * const p = greeting;  //const pointer, const data
   >    ```
   >
   >
   > 2. 如果关键字const出现在星号左边，表示被指物是常量；出现在右边，表示指针自身是常量；出现在两边，表示被指物和指针两者都是常量。
   >
   >    ```c++
   >    void f1(const Widget* pw);
   >    void f2(Widget const* pw);   //两者相同
   >    ```
   >
   > 3. STL迭代器系以指针为根据塑模出来，所以迭代器的作用就像个T *指针。
   >
   >    ```c++
   >    vector<int>vec;
   >    const vector<int>::iterator iter = vec.begin(); //iter的作用就像个T * const
   >    *iter = 10;										//right
   >    iter++;											//wrong,iter是const，指针是常量
   >
   >    vector<int>::const_iterator citer = vec.begin();//citer的作用就是const T*
   >    *citer = 10;									//wrong, *citer是const，被指物是常量
   >    ++citer;										//right
   >    ```
   >
   > 4. 请记住
   >
   >    > 1. 将某些东西声明为const可帮助编译器测出错误用法。const可被施加于任何作用域的对象、函数参数、函数返回类型、成员函数本体。
   >    > 2. 编译器强制实施bitwise constness，但你编写程序时应该使用“概念上的常量性”
   >    > 3. 当const和non-const成员函数有着实质等价的实现时，令non-const版本调用const版本可避免代码重复。

4. 条款4: 确定对象被使用前已被初始化。

   > ```c++
   > class A {
   >   private:
   >   	int a;
   >   public:
   >   	A(const int x) {    //赋值
   >       a = x;
   >   	}
   > }
   >
   > class A {
   >   private:
   >   	int a;
   >   public:
   >   	A(const int x):a(x) {}  //初始化，效率更好
   > }
   > ```
   >
   > 1. 请记住
   >
   >    > 1. 为内置型对象进行手工初始化，因为C++不保证初始化她们
   >    > 2. 构造函数最好使用成员初值列，而不要在构造函数本体中使用赋值操作。初值列列出的成员变量，其排列次序应该和声明次序相同。
   >    > 3. 为免除“跨编译单元之初始化次序”问题，请以local static 对象替换non-local stattic对象。

5. 条款5: 了解C++默默编写并调用那些函数。

   > 编译器可以暗自给class创建default构造函数、copy构造函数、copy assignment操作符，以及析构函数。

6. 条款6: 若不想使用编译器自动生成的函数，就该明确拒绝。

   > 为驳回编译器自动（暗自）提供的技能，可将相应的成员函数声明为private并且不予实现。

7. 条款7: 为多态基类声明virtual析构函数。[多态性](http://blog.csdn.net/hackbuteer1/article/details/7475622)

   > 1. 带有多态性的base class应该声明一个vortual析构函数，如果class带有任何virtual函数，它就应该拥有一个virtual析构函数。
   > 2. class的设计目的如果不是作为base class使用，或不是为了具备多态性，就不应该声明virtual析构函数。

8. 条款8: 别让异常逃离析构函数。

   > 1. 析构函数绝对不要吐出异常。如果一个被析构函数调用的函数可能抛出异常，析构函数应该捕捉任何异常，然后吞下它们（不传播）或结束程序。
   > 2. 如果客户需要对某个操作函数运行期间抛出异常 作出反应，那么class应该提供一个普通函数（而非在析构函数中）执行该操作。

9. 条款9: 绝不在构造和析构过程中调用virtual函数。

   > 在构造和析构期间不要调用virtual函数，因为这类调用从不下降至derived class。

10. 条款10: 令operator=返回一个reference to *this.

 > ```c++
 > int x, y, z;
 > x=y=z=5; //赋值连锁形式
 > //为了实现对象的连锁赋值， 赋值操作符必须返回一个reference指向操作符的左侧实参。
 > class Widget {
 >   public:
 >   Widget& operator=(const Widget& rhs) { //返回类型是个reference
 >     return *this;  //返回左侧对象
 >   }
 > }
 > ```
 >



11. 条款11: 令operator=中处理“自我赋值”

   > ```c++
   > class Bitmap{};
   > class Widget{
   >   private:
   >   	Bitmap *pb;
   > }
   >
   > Widget &Widget::operator=(const Widget &rhs) {
   >   if (this == &rhs)    //证同测试，如果是自我复制，就不做任何事
   >       return *this;
   >   delete pb;
   >   pb = new Bitmap(*rhs.pb);
   >   return *this;
   > }
   >
   > Widget& Widget::operator=(const Widget &rhs) { //具备“异常安全性”
   >   Bitmap *pOrig = pb;      //记住原先的pb
   >   pb = new Bitmap(*rhs.pb);//令pb指向*pb的一个复件
   >   delete pOrig;            //删除原先的pb
   >   return *this;
   > }
   > void Widget::swap(Widget &rhs) //交换*this和rhs的数据。
   > Widget& Widget::operator=(const Widget &rhs) {
   >   Widget temp(rhs); //为rhs创建副本
   >   swap(temp);		//将*this数据和上述副本的数据交换
   >   return *this;
   > }
   > ```
   >
   > 1. 确保对象自我赋值时operator=有良好行为。其中技术包括比较来源对象和目标对象的地址、精心周到的语句顺序、以及copy-and-swap。
   > 2. 确定任何函数如果操作一个以上的对象，而其中多个对象是同一个对象时，其行为仍然正确。

12. 条款12: 复制对象时勿忘其每个成分

   > 1. copying函数应该确保复制“对象内的所有成员变量”及“所有base class成分”
   > 2. 不要尝试以某个copying函数实现另一个copying函数。

13. 条款13: 以对象管理资源

   > 1. auto_ptr是个类指针对象。[auto_ptr](http://www.cnblogs.com/GnagWang/archive/2010/11/19/1881811.html);
   >
   >    在新建的对象的范围内，若遇到异常或return，导致对象没有调用析构函数，导致资源泄露，auto_ptr智能指针，就会调用该对象的析构函数，释放资源。
   >
   >    ```c++
   >    std::auto_ptr<A>pInv1(createA());   //pInv1指向createA的返回物
   >    std::auto_ptr<A>pInv2(pInv1);       //现在pInv2指向对象，pInv1被设为NULL
   >    pInv1 = pInv2;                      //现在pInv1指向对象，pInv2被设为NULL
   >    ```
   >
   > 2. Auto_ptr的替代方案“引用计数型智慧指针”，持续追踪共有多少对象指向某笔资源，并在无人指向它时自动删除该资源，不过它不能打破环状引用。
   >
   >    ```c++
   >    std::tr1::shared_ptr<A>pInv1(createA());   //pInv1指向createA的返回物
   >    std::tr1::shared_ptr<A>pInv2(pInv1);       //现在pInv2,pInv1同时指向对象
   >    pInv1 = pInv2;                       //现在pInv2,pInv1同时指向对象
   >    ```
   >
   > 3. auto_ptr和shared_ptr两者都在其析构函数内做delete而不是delelte[]，那意味在动态分配而得array身上使用是不行的，虽然能通过编译。
   >
   >    ```c++
   >    std::auto_ptr<std::string>aps(new std::string[10]);
   >    std::tr1::shared_ptr<int>spi(new int[1024]);    //馊主意
   >    ```

14. 条款14: 在资源管理类中小心copying行为

   >1. 复制RAII（Resource Acquisition Is Initlization:资源取得时机便是初始化时机）对象必须一并复制它所管理的资源，所以资源的copying行为决定RAII对象的copying行为。
   >2. 普遍而常见的RAII class copying行为是：抑制copying、施行引用计数法。

15. 条款15: 在资源管理类中提供对原始资源的访问

   > 1. APIs往往要求访问原始资源，所以每一个RAII class应该提供一个“取得其所管理之资源”的方法
   > 2. 对原始资源的访问可能经由显式转换或隐式转换。一般而言显式转换比较安全。

16. 条款16: 成对使用new和delete要采用相同形式

   > ```c++
   > string *p1 = new string;
   > string *p2 = new string[100];
   >
   > delete p1;  //删除一个对象
   > delelte[] p2;  //删除一个由对象组成的数组
   > ```
   >
   > 如果你在new表达式中使用[]，必须在相应的delete表达式中也使用[]。

17. 条款17: 以独立语句将newed对象置入智能指针

   > 以独立语句将newed对象存储于智能指针内。如果不这样做，一旦异常被抛出，有可能导致难以察觉的资源泄露。

18. 条款18: 让接口容易被正确使用不易被误用。

   > ```c++
   > struct Day{
   >   explicit Day(int d):val(d){}
   >   int val;
   > };
   >
   > struct Month {
   >   explicit Month(int m):val(m){}
   >   int val;
   > };
   >
   > struct Year{
   >   explicit Year(int y):val(y){}
   >   int val;
   > };
   >
   > class Date{
   >   public :
   >   Date(const Month& m, const Day& d, const Year& y);  //通过编译，便是正确的输入。
   > }
   > ```
   >
   > ​

19. 条款19：设计class犹如设计type

   > 1. [new](http://blog.csdn.net/sayigood/article/details/3947901)，[内存分配](http://www.open-open.com/lib/view/open1371741339937.html)。

20. 条款20: 宁以pass-by-reference-to-const替换pass-by-value

   > 尽量使用pass-by-rference-to-const替换pass-by-value.前者通常比较高效，并可避免切割问题。

21. 条款21: 必须返回对象时，别妄想返回其reference。

   > 绝不要返回pointer或reference指向一个local stack对象，或返回一个reference指向一个heap-allocated对象，或返回pointer或reference指向local static对象而有可能同时多个这样的对象。
   >
   > ```c++
   > inline const A operator * (const A& lhs, const A& rhs) {
   >   return A(lhs.n * rhs.n, lhs.d*rhs.d);    //返回一个新对象。
   > }
   > ```

22. 条款22: 将成员变量声明为private

   > protected并不比public更具封装性。

23. 条款23: 宁以non-member、non-friend替换member函数。

24. 条款24: 若所有参数皆需类型转换，请为此采用non-member函数

   > ```c++
   > class A{
   >   private:
   >   	int a, b;
   >   public:
   >   	A(int a=0,int b=1);
   >   	int geta()const;
   >   	int getb()const;
   >   	const A operator * (const A & rhs) const{
   >       
   >   	}
   > }
   >
   > A a(1, 8);
   > A b(1, 2);
   > A result = a*b;
   >
   > result = a*2;  //可以，2隐式转换
   > result = 2*a;  //不可以，
   >
   > const A operator * (const A &lhs, const A &rhs) {   //non-member函数
   >   return A(lhs.geta()*rhs.geta(),lhs.getb()*rhs.getb());
   > }
   >
   > result = 2*a;  // 可以了，，调用non-member函数
   > ```

25. 条款25: 考虑写出一个不抛出异常的swap函数。

   > ```c++
   > namespace Widgetstuff {
   >   template<typename T>
   >   class Widget{
   >     void swap(Widget &a);
   >   };
   >   template<typename T>    //non-member swap函数，这里空间不属于std命名空间
   >     void swap(Widget<T> &a, Widget<T> &b) {
   >       a.swap(b);
   >     }
   > }
   > ```
   >
   > 1. 当std::swap对你的类型效率不高时，提供一个swap成员函数，并确定这个函数不抛出异常。
   > 2. 如果你提供一个member swap，也该提供一个non-member swap用来调用前者，对于class（而非特化templates），也请特化std::swap.
   > 3. 调用swap时应针对std::swap使用using声明式，然后调用swap并且不带任何“命名空间资格修饰。”