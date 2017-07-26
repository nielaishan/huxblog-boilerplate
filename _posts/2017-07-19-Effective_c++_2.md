---
layout:   post
title:    "Effective C++ 二"
subtitle: "C++"
date:     2017-07-19
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - C++
---

### Effective c++

1. 条款26: 尽可能延后变量定义式的出现时间

   ```c++
   using namespace std;
   string fun(const string & passwd) {
     string encrypted;
     if (passwd.length() < minimumPasswordlength) {
       throw logic_error("password is too short");
     }
     
     
     return encrypted;
   }
   using namespace std;
   string fun(const string & passwd) {
      if (passwd.length() < minimumPasswordlength) {
      throw logic_error("password is too short");
    }
    string encrypted;   //延迟定义，需要的时候定义
    
    return encrypted;
   }
   ```

2. 条款27: 尽量少做转型动作。

   1.    static_cast:用来强迫隐式转换。

         ```c++
         class Widget{
           public:
           	explicit Widget(int size);
         }

         void dosomework(const Widget& w);
         dosomework(Widget(15));             //以一个int加上“函数风格“的转型动作创建

         dosomework(static_cast<Widget>(15)); //以"c++风格"
         ```


3. 条款28: 避免返回handles指向对象内部成分

4. 条款29: 为“异常安全”而努力是值得的。

   1. “强烈保证”往往能够以copy-and-swap实现出来。

5. 条款30: 透彻了解inline的里里外外

   1. 免除函数调用成本。
   2. inline函数背后的整体观念是，将“对此函数的每一个调用”都以函数本体替换之。
   3. virtual意味着“等待，直到运行期才确定调用哪个函数”；inline意味“执行前，先将调用动作替换被调用函数的本体”

6. 条款31: 将文件间的编译依存关系降至最低。

   1. 基于此构想的两个手段Handle classes和Interface classes

7. 条款32: 确定你的public继承塑模出is-a关系

   1. 如果你令class D（derived）以public形式继承class B（base），你便是告诉编译器，每一个类型为D的对象同时也是一个类型为B的对象，反之不成立。
   2. “public继承”意味着**is-a**，适用于base class身上的每一件事一定也适用于derived classes身上，因为每一个derived class对象也都是base class对象。

8. 条款33: 避免遮掩继承而来的名称

   1. derived class内的名称会遮掩base class内的名称。

   2. 为了让被遮掩的名称再见天日，可使用using声明式或转交函数。

      ```c++
      class Derived: public Base {
        public :
        	using Base::fun;  //using声明
        	virtual void mf1(){  //转交函数
            Base::mf1();
        	}
      }
      ```

9. 条款34: 区分接口继承和实现继承

   1. 声明一个pure virtual函数的目的是为了让derived class只继承函数的接口。

      ```c++
      class Shape{
        public:
        	virtual void draw()const=0;
        	virtual void error(const std::string &msg);
        	int objectID()const;
      }

      class Rectangle:public Shape{}
      class Ellipse:public Shape{}

      Shape *ps = new Shape; //error shape是抽象的
      Shape *ps1 = new Rectangle;  //right
      ps1->draw();  //调用Rectangle的Draw函数
      ```

   2. 声明简朴的impure virtual函数的目的，是让derived class继承该函数的借口和缺省实现。

   3. 声明non-virtual函数的目的是为了令derived class继承函数的接口及一份强制性实现。

10. 条款35: 考虑virtaul函数以外的其他选择。[Tempalte medthod设计模式](http://bdxnote.blog.163.com/blog/static/8444235200852941337781/)、[Strategy模式](http://www.cnblogs.com/jiese/p/3181099.html).**之后还要继续复习**

11. virtual函数的替代方案包括NVI及strategy设计模式的多种形式。
12. 将机能从成员函数一到class外部函数，带来一个缺点，非成员函数无法访问class的non-public成员。
13. Tr1::function对象的行为就像一般函数指针。

14. 条款36: 绝不重新定义继承而来的non-virtual。

15. 条款37: 绝不重新定义继承而来的缺省参数值

   1. 对象的静态和动态类型

      ```c++
      class Shape  {
        public :
        	enum ShapeColor{Red, Green, Blue };
        	virtual void draw(ShapeColor color=Red) const = 0;
        
      }

      class Rectangle: public Shape {
        public :
        	virtual void draw(ShapeColor color=Green) const;
      }

      class Circle: public Shape {
        public :
        	virtual void draw(ShapeColor color)const;
      }
        Shape *ps;      //以下三个都是静态类型为Shape *
        Shape *pc = new Circle;     //pc的动态类型：Circle *
        Shape *pr = new Rectangle	//pr的动态类型：Rectangle *
          
        ps = pc;       //ps的动态类型如今是Circle *
        ps = pr;       //ps的动态类型如今是Rectangle *

        pc->draw(Shape::Red);  //调用Circle::draw(Shape::Red)
        pr->draw(Shape::Red);  //Rectangle::draw(Shape::Red)

        pr->draw();  //Rectangle::draw(Shape::Red) !, 由于pr的静态类型时shape *，所以此一调用的缺省参数来自Shape class而非Rectangle class；
        /*
        	若改为以下形式，采用NVI（non-virtual interface）
        	这个设计很清楚地使得draw函数绝对不被color缺省参数总是Red
        */
        class Shape  {
          public :
          	enum ShapeColor{Red, Green, Blue };
          	void draw(ShapeColor color=Red) const {
              doDraw(color);
          	}
          private:
          	virtual doDraw(Shapecolor color) const = 0;
        }

        class Rectangle: public Shape {
          public :
          private:
          	virtual void doDraw(Shapecolor color) const;
        }

        class Circle: public Shape {
          public :
          	virtual void draw(ShapeColor color)const;
        }
      ```

        Virtual 函数系动态绑定而来，意思是调用一个virtual函数时，究竟调用哪一份函数实现代码，取决于发出调用的那个对象的动态类型
      ```

      ```


13. 条款38: 通过复合塑模出has-a或“根据某物实现出”

14. 条款39: 明智而审慎地使用private继承

   1. 如果D以private形式继承B，意思是D对象根据B对象实现而得。
   2. private继承意味着is-implemented-in-terms-of（根据某物实现出）。
   3. 附加：[静态成员](http://www.cnblogs.com/lzjsky/archive/2011/01/24/1943199.html).

15. 条款40: 明智而审慎地使用多重继承。

16. 条款41: 了解隐式接口和编译期多态。

   1. class和template都支持接口和多态。
   2. 对class而言接口是显式的，以函数签名为中心。多态则是通过virtual函数发生于运行期。
   3. 对template而言接口是隐式的，奠基于有效表达式。多态则是通过template具现化和函数重载解析发生于编译期。

17. 条款42: 了解typename的双重意义。

   1. template<class T>class Widget;

      template<typename T>class Widget;

      class和template在此时两者没有不同。

   2. [typename](http://dev.yesky.com/13/2221013.shtml).

      在你涉及到一个在 template（模板）中的 nested dependent type name（嵌套依赖类型名）的任何时候，你必须把单词 typename 放在紧挨着它的前面。

      ```c++
      #include<iostream>
      #include<cstdio>
      #include<vector>
      using namespace std;
      template <typename T>

      void print(const T &container) {
      	typename T::const_iterator iter(container.begin());
      	++iter;
      	int value = *iter;
      	cout<<value<<endl;
      }

      int main() {
      	vector<int>p;
      	for (int i=0; i<3; i++)
      		p.push_back(i);

      	print(p);
      	return 0;
      }
      ```

   3. 声明tempalte参数时，前缀关键字class和typename可互换

   4. 请使用关键字typename标识嵌套从属类型名称；但不得在base class list（基类列）或member initialization list（成员初值列）内以她作为base class修饰符。

18. 条款43: 学习处理模板化基类内的名称。

   1. [using](http://www.cnblogs.com/yuaqua/archive/2011/10/22/2219991.html).
   2. 可在derived class template内通过“this->”指涉base class template内的成员名称，或藉由一个明白写出的“base class 资格修饰符”完成。

19. 条款44: 将与参数无关的代码抽离template

20. 条款45: 运用成员函数模板接受所有兼容类型

   ```c++
   template <typename T>
   class SmartPtr{
     public :
     	template<typename U>
         SmartPtr(const SmartPtr<U>& other):heldPtr(other.get()) {  //根据SmartPtr<U>生成一个SmartPtr<T>
         }  
     	T* get() const {
         return heldPtr;
     	}
     private:
     	T *heldPtr;
   }
   ```

   1. 请使用member function template生成“可接受所有兼容类型”的函数
   2. 如果你声明member template用于“泛化copy构造”和“泛化assignment操作”，你还是需要声明正常的copy构造函数和copy assignment操作符。

21. 条款46: 需要类型转换时请为模板定义非成员函数

   当我们编写一个class template，而它所提供之“与此template相关的”函数支持“所有参数之隐式类型转换”时，请将那些函数定义为“class template内部的friend函数”。

22. 条款47: 请使用traits class表现类型信息（没看）

23. 条款48: 认识template元编程

   ```c++
   #include<iostream>
   #include<cstdio>
   using namespace std;
   template <unsigned n>
   struct F{
   	enum { value = n*F<n-1>::value };
   };

   template<>
   struct F<0> {
   	enum { value = 1 };
   };
   int main() {
   	cout<<F<5>::value<<endl;   //打印120
   }
   /*
   	每个F template具现体都是一个struct，每个struct都使用enum hack声明一个名为value的TMP变量，value用来保存当前计算所得的阶乘值
   */
   ```

   1. Tempalte metaprogramming（TMP，模板元编程）可将工作由运行期移往编译器。
   2. TMP可被用来生成“基于政策选择组合”的客户定制代码。

24. 条款49: 了解new-handler的行为

25. 条款50: 了解new和delete的合理替换时机

   有许多理由需要写个自定的new和delete，包括改善效能、对heap运用错误进行调试、收集heap使用信息。

26. 条款51: 编写new和delete时需固守常规

   1. operate new应该内含一个无穷循环，并在其中尝试分配内存，如果它无法满足内存需求，就应该调用new-handler。它也应该有能力处理0bytes申请。
   2. operator delelte应该在收到null指针时不做任何事。

27. 条款52: 写了placement new也要写placement delete

   1. 当你声明placement new和placement delete，请确定不要无意识地遮掩它们的正常版本。


