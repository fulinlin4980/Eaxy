#  <font color=purple>一.c++与C语言的区别</font>

##  1.命名空间(namespace)

+ **装代码的容器,不同的命名空间允许使用相同的名字变量**

+ **提高标识符的使用率**
+ **避免命名污染**

### 1.创建

```c++
namespace name1
{
    //可以存在任何东西
    int num1=1;
    char* p="niasdn";
    float num2=1.2f;
    void print()
    {
            printf("你好世界");
    }

    
}
```

###  2.访问

+ 带前缀方式
  + 作用域分辨符 ::

```c++
name1::num1;
name1::print();
```



+ 空间名::成员
+ 省略前缀的方式                                                **具有作用域**
  + using namespace  空间名;

```c++
using namespace name1;
print();
```

+ 先声明再实现

```c++
namespace name2   //声明
{
    void print();
    int a;
}
void name2::print()//实现
{
    printf("你好世界\n");
}
name2::a=0;
```



##  2.标准输入输出

+ 包含头文件#include<iostream>
+ 基本输出:cout<<
+ 基本输入:cin>>

##  3.新数据类型

###  1.空指针       

```c++
int *num=nullptr;		//不在使用NULL
```

###  2.布尔类型

```c++
bool num=true;		//直接使用不需要包含头文件了
```

###  3.const类型

+ 修饰变量不能被修改
+ 修饰的变量必须赋初值

+ c++对于const的要求更严格
  + 字符串指针的赋值
  + 字符串传参

```c++
char* array1="alsjdf";		//错误写法，会报错
const char* array2="aasdf";	//正确写法
void print1(char* array);	//只能传入变量,不能传入字符转常量
void print1(const char* array);//既可以传入常量也可以传入变量
```

+ c++中的const比C语言更强大,c++中的const可以修饰类中的函数

###  4.自动类型推断

+ auto自动推断		**必须结合赋值做推断，没有赋值就无法推断**

````c++
int a=0;
char n='2';
struct STUDENT student
{
   const char* name;
    int age;
}stu2;
auto v=a;		//推断v是int型
auto b;			//错误写法，必须要赋初值
````



+ decltype()自动推断			**返回一个类型**

```c++
decltype(stu2) stu3=stu2;	//推断stu2的类型，并且创建一个变量
```

###  5.引用类型

__可以说是用来替换指针的一种比较棒的方式，可以理解为起别名__

+ 普通引用:  类型& 标识符 = 变量

```c++
int name1=101;
int &name2=name1;		//相当于给name1起一个其他的名字(name2),name1与name2是同一块内存的不同名字

```

```c++
void move(int &num)	//调用时为: int &num=a,给a齐了一个别名，num就是a,a就是num,改变num的值就是改变a的值
{
    num=12;
}
int a=90;
move(a);
```

```c++
int num=10;
//常引用可以给普通变量起别名
const int& num2=num;		//可以
const int num3=100;
//普通引用不能给常量起别名
int& num4=num3;				//不可以

```



+ 右值引用:  类型&& 标识符 = 右值;   **规避传常引用时无法修改的情况**

```c++
const int a=0;			//a是常属性变量,是左值
int&& b=123;

```

+ std::move()函数可以将左值变成右值  		

###  6.枚举类型

_c语言枚举类型与整型没有区别_,<font color=red> **c++枚举类型不能充当整型使用**</font>



```c
enum color {red,blue,black};
void print(enum color Color)
{
printf("%d",color);
}
print(123);
print(red);
```

+ c++替换方式

  ```c++
  enum class Dir {left,right,up,dowon}
  
  std::cout<<Dir::left<<std::endl;
  ```

  

##  4.函数思想

### 1.内联思想			

_inline修饰的函数,牺牲空间换速度_

+ 短小精悍

```c++
inline int max(int a,int b)
{
    return a>b?a:b;
}
```



### 2.重载思想			

_允许存在同名不同参的函数存在,与函数返回值没有关系_

+ 数目不同
+ 类型不同
+ 顺序不同(建立在类型不同基础上)

```c++
//传几个参就调用哪个函数
void max(int a,int b);
void max(int a,int b,int c);
void max(int a,char b);
```



### 3.缺省思想			

_给函数参数赋初值,可以提供不同形态的调用_

+ 要求从右到左连续赋初值，中间不能存在没有赋初值的

```c++
void Data(int a,int b=2,int c=4)
//void Data(int a,int b=9,int c)   错误写法
{
    std::<<a<<b<<c<<std::endl;
}
Data(2);
Data(2,3);
Data(2,3,5);
```



### 4.lambda表达式

##  5.动态申请内存

_C语言是malloc,calloc,realloc,free(),,,,**c++使用new,delete**_

### 1.申请内存

```c++
int *a=new int;				//不初始化
int *aa=new int(12);		//申请内存并且初始化
delete a;
delete aa;


int *array=new int[5];	//申请一段内存
int *array2=new int[5]{1,2,2,1,3};//申请一段内存，并且做初始化
delete[] array;			//释放一段内存
```

### 2.内存重新分配

**_new(要分配的内存的首地址)_**

+ 有利于综合管理内存

```c++
int *a=new int[100];
int *b=new(a+0) int[5];
int *c=new(a+20) int[5];
char* d=new(a+40) char[10]{"你好啊"};
```

## 6.c++string类型

_头文件<string>_

### 1.创建

```c++
std::string str;
std::string str2("asdf");
std::string str3=str2;

```

### 2.输入

```c++
std::string input;
std::cin>>input;
```

### 3.输出

```c++
std::cout<<input<<std::endl;
```

### 4.判断

```c++
std::string p1="asdff";
std::string p2="dgsdfg";
std::cout<<(p1==p2)<<std::endl;
std::cout<<(p1<p2)<<std::endl;
std::cout<<(p1>p2)<<std::endl;
std::cout<<(p1!=p2)<<std::endl;
```

### 5.连接

```c++
std::string p1="asdff";
std::string p2="dgsdfg";
std::string p3=p1+p2;
std::cout<<p3<<std::endl;
```

## 7.c++类型转换



### 1.强制类型转换

```c++
int num=int(2342.2345);
float num2=float(133);

```

### 2.c++专业基本转换

**_官方说c++类型转换更安全_**

_关键字<要转换的类型>(表达式)_

+ static_cast		**类似C语言的强制转换**
+ const_cast        **专门处理const属性的转换**
+ dynamic_cast   **多态和交叉**

```c++
int num=static_cast<int>(23.3434);		//static_cast
const int num2=10;
int num3=const<int>(num2);
```

## 8.c++结构体的区别

+ 创建变量时不需要关键字了

```c++
struct MM 
{
int a;
int b;
};
MM girl1;
MM girl2;
```

+ 可以带函数
+ 函数可以访问自己结构中的变量

```c++
struct MM
{
    //属性
    int a;
    int b;
    //行为
    void print()
    {
        std::cout<<a<<b<<std::endl;
    }
    
};

```





#  <font color=purple>二.c++类和对象</font>

## 1.类

_行为与数据的抽象_

+ 数据成员
+ 成员函数
+ 类的特性
  + 继承
  + 封装
  + 多态

## 2.对象

_类的具体化_



## 3.创建类

```c++
class MM		//类名
{
    
    int stx;		//不修饰时默认是protected属性
    public:
    std::string name;
    protected :
    int age;
    private:
    int money;
};
MM girle;			//创建对象
girle.name="小花"；  //只能访问public修饰属性

```

***自己类中的属性,自己可以任意访问***

```c++
class MM2
{
  public :
    int age;
    protected :
    std::string name;
    private:
    int money;
    
    void print()
    {
        std::cout<<age<<name<<money<<"\n"; //任意访问数据
    }
    
    
};
```



+ 权限限定词:限定内外对象对属性的访问权限,
  + public 		**公有属性:类外能够直接访问的唯一属性**
  + protected   **保护属性:**
  + private         **私有属性:**

## 4.类数据初始化

### 1.类中设置默认值    **大部分编译器支持**

```c++
class MM
{
  	public :
    std::string name="小花";
    protected:
    int age=12;
};
```

### 2.类中定义函数让用户初始化数据

```c++
class MM
{
  	public :
    void setData(std::string _name,int _age)
    {
        name=_name;
        age=_age;
    }
    protected:
    std::string name;
    int age;
};
```

### 3.通过返回引用的函数去修改数据

```c++
class MM2
{
  	public :
    std::string& getname()
    {
        return name;
    }
    int& getage()
    {
        return age;
    }
    protected:
    std::string name;
    int age;
};

 	MM2 girle2;
    girle2.geage() = 12;
    girle2.getname() = "小白";
```



## 5.c++构造函数

+ 名字: 和所在对象类型名一样

+ 返回值:无

+ 实例化类时被自动调用

+ 构造函数的参数决定实例化类时传的参数

+ 没有构造函数的类为啥可以创建

  + 不写构造函数，会存在一个默认的无参构造函数,所以可以创建无参对象

  ```c++
  class student   //无定义构造函数
  {
    	public:
      protected:
      int age;
      int sex;
  };
  student stu1;		//使用默认无参函数创建对象
  ```

  + 如果写了构造函数,默认构造函数就不存在了

  ```c++
  class student   //有定义构造函数
  {
    	public:
      student(int _age,int sex)
      {
          age=_age;
          sex=_sex;
      }
      protected:
      int age;
      int sex;
  };
  student stu1(12,1);
  student stu2;		//错误语法,必须带构造函数的参数
  ```

  

  + c++操作无参构造函数的两个关键字

    + delete:删除函数
    + default:使用默认函数

    ```c++
    class student   //有定义构造函数
    {
      	public:
        student()=default;	//将默认无参函数赋值给自定义无参函数,以用来创建无参对象
        student(int _age,int sex)
        {
            age=_age;
            sex=_sex;
        }
        protected:
        int age;
        int sex;
    };
    student stu1(12,1);
    student stu2;		//正确对象
    ```

    

### 1.无参构造函数

<font color=red>_创建类型时被自动调用_</font>

_类型()_

```c++
class student
{
public:
    student()		//无参构造函数
    {
        std::cout << "你好" << '\n';
    }
public:
    std::string name;
protected:
    int age;
};
```



### 2.有参构造函数

<font color=red>_可以通过重载和缺省思想实现_</font>

+ 实现对象数据的初始化

```c++
class student
{
public:
    student()
    {
        std::cout << "你好" << '\n';
    }
    student(std::string _name,int _age)
    {
        name=_name;
        age=_age;
    }
public:
    std::string name;
protected:
    int age;
};
```

### 3.构造函数委托

**_类名():类名(参数一,参数二)_**

<font color=red>***允许一个构造函数调用另一个构造函数***</font>  

```c++
class student
{
public:
    student():student("消化",90)		//调用另外一个构造函数
    {
        std::cout << "你好" << '\n';
    }
    student(std::string _name,int _age)
    {
        name=_name;
        age=_age;
    }
public:
    std::string name;
protected:
    int age;
};
```



### 4.禁止隐式转换调用

```c++
class student
{
public:
    student()
    {
        std::cout << "你好" << '\n';
    }
    student(std::string _name,int _age)
    {
        name=_name;
        age=_age;
    }
public:
    std::string name;
protected:
    int age;
};

student stu1("小花",10);	//显示调用
student stu2={"小白",19}  //隐式调用
```

+ 禁止隐式调用函数:explicit

### 5.匿名对象

+ 会交换使用权

```c++
class MM
{
  public:
    MM(std::string _name)
    {
        name=_name;
    }
    std::string name;
};
MM stu1=MM("小花");		//创建一个匿名对象赋值给stu1
```



## 6.c++析构函数

+ 函数名字:**~类名**
+ 参数:无参
+ 不写析构函数,会存在一个默认的析构函数
+ 什么时候要写析构函数
  + 当类成员做动态内存申请的时候

```c++
class MM
{
  public:
    MM(const char* _name,int age)
    {
        int len=strlen(name)+1;
        _name=new char[len];
        strcpy_s(name,)
    }
    protected:
    std::string name;
    int age;
    ~MM()
    {
        delete[] _name;
    }
};
```



+ 什么时候调用
  + 对象死亡之前调用

```c++
class student
{
  public:
    ~student()		//析构函数
    {
        
    }
};
```

+ new的对象在delete时才会调用析构函数  



## 7.c++拷贝构造函数

_拷贝构造函数也是构造函数,一种特殊的构造函数_

+ 函数参数:唯一参数->对对象的引用
+ 函数作用:通过一个对象创捷另外一个对象
+ 不写拷贝构造函数会默认有一个拷贝构造函数

```c++
class MM
{
    private:
    int data;
    std::string name;
    public:
    MM(std::string _name,int _data)
    {
        data=_data;
        name=_name;
    }
    MM(const MM& other)
    {
        name=other.name;
        data=other.data;
        std::cout<<name<<' '<<data<<'\n';
    }
};
```

### 1.深浅拷贝问题

+ 浅拷贝:默认的拷贝函数是浅拷贝,拷贝函数中没有写动态内存申请的都是浅拷贝
+ 深拷贝:在拷贝构造函数中做了动态内存申请是深拷贝
+ 当类中的数据成员是指针,并且做了动态内存申请的时候,手动写了析构函数并且做了内存释放的时候

### 2.浅拷贝引发的析构问题

**原因:重复释放同一块内存**

```c++
class MM
{
public:
    MM(const char* str)
    {
        int len = strlen(str) + 1;
        pname = new char[len + 1];
        strcpy_s(pname,len,str);
    }
    ~MM()
    {
        delete[] pname;
    }
protected:
    char* pname;
};
int main()
{
    {
        MM mm("小花");
        MM girl(stu1);  		//使用默认拷贝构造函数,引发析构问题
    }
   


    return 0;
}
```



![](浅拷贝问题.png)





### 3.移动拷贝构造函数

+ 在拷贝构造函数中引用写为右值引用

~~~c++
MM(MM&& temp)
{
     
}
~~~

## 8.数组对象

+ 需要准备无参构造函数
+ 构造n个对象数组其实是在构造n个无参对象

```c++
class MM
{
  public:
    MM(std::string _name="默认")
    {
        name=_name;
        std::cout<<name<<'\n';
    }
    private:
    std::string name;
};
MM MMarray[3]={{"1"},{"2"},{"3"}};	//第一种
MM MMarray[3];						//第二种,需要缺省构造函数
```





# <font color=purple>三.c++类的组合</font>

## 1.类的组合

类的组合:以另一个类的对象当做数据成员

+ 初始化参数列表方法: 构造函数(参数1,,参数2,...):数据成员1(参数1),数据成员2(参数2){}  <font color=red>**用途:用于对对象成员数据的初始化**</font>



```c++
//嘴巴类
class Mouse
{

	public:
		Mouse(): Mouse("嘴巴") {}
		Mouse(std::string name)
		{
			mouseName = name;


		}
		void print()
		{
			std::cout << mouseName << '\n';
		}
	protected:

		std::string mouseName;
};
//鼻子类
class Nose
{
	public:
		Nose(): Nose("鼻子") {}
		Nose(std::string name)
		{
			noseName = name;
		}
		void print()
		{
			std::cout << noseName << '\n';
		}
	protected:

		std::string noseName;
};
//眼镜类
class Eye
{
	public:
		Eye() : Eye("眼睛") {}
		Eye(std::string name)
		{
			eyeName = name;
		}
		void print()
		{
			std::cout << eyeName << '\n';
		}
	protected:

		std::string eyeName;
};
//类的组合
class Head
{
		//组合类
	public:
		Head(std::string ename,std::string 	  		         nname,std::string mname):eye(ename),nose(nname),mouse(mname){}       
    
		void print()
		{
			eye.print();
			nose.print();
			mouse.print();
		}
	protected:
		Eye eye;
		Nose nose;
		Mouse mouse;


};
/*
在上面代码中，定义了三个子类,Mouse,Eye,Nose
在Head类中，包含了这三个类的对象,这就是类的组合.

Head(std::string ename,std::string 	  		         nname,std::string mname):eye(ename),nose(nname),mouse(mname){}       
    在则段代码中,使用了初始化列表进行初始化,对象成员数据
*/
```



 <font color=red size=5>!!!:如果对象成员有了有参构造函数,那么对象成员必须要写无参构造函数,然后在组合类里使用初始化列表方法对对象成员进行数据初始化,否则组合类中无法写构造函数</font> 

```c++
class Eye1
{
	public:
		Eye1(std::string _name)
		{
			name = _name;
		}
	protected:
		std::string name;

};
class Head1
{
	public:
		Head1(){}
	protected:
		Eye1 eye1;

};
/*
这是错误代码,Head1类中有有参构造函数的对象成员eye1,但是写构造函数时没有对eye1进行数据初始化,所以无法写Head1的构造函数,所以代码错误
*/
```

## 2.c++类数据与参数同名问题

```c++
class MM
{
    public:
    MM(std:：string name)//参数名与属性名同名
    {
     name=name;
    }
    protected:
    std::string name;
}
//这种写法是错误的
```

### 1.解决方案一  

+ 类名限定

```c++
class MM
{
    public:
    MM(std:：string name)//参数名与属性名同名
    {
     MM::name=name;		//类名限定参数
    }
    protected:
    std::string name;
}
```

### 2.解决方案二

+ 初始化参数列表			<font color=red>仅限构造函数</font> 

```c++
class MM
{
    public:
    MM(std:：string name):name(name){}//括号外默认是成员数据,括号外默认是参数
    protected:
    std::string name;
}
```



### 3.解决方案三

+ this指针    <font color=red>每一个对象都自带的,代表对象的地址</font> 

```c++

```



## 3.c++类中类

_内中定义另一个类_

+ 受权限限定
+ 访问:外面类名做限定

```c++
class MM
{
public:
	class Boy
	{

	public:
	protected:

	};
protected:
	//类中类
	
};
MM::Boy a;//类名限定
```

## 4.c++结构体与类

c++类中的东西结构体里面都可以用,一旦在结构体中用构造函数,需要把结构体当做类去使用。

+ 不写权限，默认是public,类中默认是private
+ c++允许存在空的类，或者结构体,内存占一个字节

```c++
class mm
{
    
};
struct Mm
{
    
};

```

# <font color=purple>四.c++特殊成员</font>

## 1.常成员

### 1.常对象

_被const修饰的对象_

+ 只能调用被const修饰的函数

### 2.常数据成员

_被const修饰的数据_

+ 不能被修改
+ 必须使用初始化参数列表进行初始化

```c++
class MM
{
    public:
    MM(std::string name,int num):num(num)//正确写法
    {
        this->name=name;
        this->num=num;//错误写法
    }
    void print()
    {
        this->num=1;//错误写法,const修饰数据不能被修改
    }
  protected:
    std::string name;
    const int num;
};

```



### 3.常成员函数

_被const修饰的函数_

+ 在当前函数不能修改数据成员,可以访问数据
+ **可以和普通函数形成重载**,普通函数优先调用普通变量成员,常对象只能调用常成员函数

写法:

```c++
class MM
{
  public:
    void print(){}//普通函数
    void print() const//常成员函数
    {}
};
```

<font color=red>**<font color=black>养成良好习惯:</font>不修改数据的函数,都可以定义为const成员函数**</font> 

## 2.static成员

### 1.静态对象

+ 静态对象是最后被释放的

### 2.类static数据

+ 必须在类外做初始化

+ 访问可以不需要对象做限定,但是要类名做限定

+ 静态数据是所有对象共有的,

+ 受权限限定

```c++
class MM
{
  public:
    static int a;
    protected:
    static int b;
};
MM::a=0;//在类外做初始化
MM::a;//a可以被访问
MM::b;//b不可以被访问
```

### 3.静态成员函数

_被static修饰的函数_

+ 不能使用this指针

+ 静态成员函数访问静态数据没有问题,访问非静态数据的时候必须指定对象
  + 传参
  + 在里面创建对象

```c++
class MM
{
  public:
    static void print()//可以传一个对象作为参数 MM& Data
    {
        std::cout<<num;//错误,访问非静态数据需要指定对象
        std::cout<<count;//可以访问静态数据
        std::count<<Data.num;//可以,使用传参方式
    }
    protected:
    static int count;
    int num;
};
MM::count=0;//类做初始化
```

## 3.单例设计模式

_解决问题的固定套路:**设计模式**_

1. 构造函数私有化
2. 提供一个全局的静态方法,访问唯一对象
3. 类中定义一个静态指针,指向唯一对象

```c++

```



## 4.友元

**1. 有元关系,无论友元函数还是友元类只是单纯提供对象在特定场所具有无视权限的功能**

_friend修饰_

### 1.友元函数

1. 不属于类,在外面定义时不需要类名做限定

```c++
class MM
{
  public:
    MM(int num):num(num){}
    friend void print();
    protected:
    int num;
};
void print()		//定义不需要类名做限定
{
    MM temp(3);
    std::cout<<temp.num<<'\n';
}
```



_friend 修饰的函数_

+ 普通函数成为友元函数

```c++
class MM
{
  public:
    MM(int num):num(num){}
    friend void print();
    protected:
    int num;
};
void print()		//定义不需要类名做限定
{
    MM temp(3);
    std::cout<<temp.num<<'\n';
}
```



+ 以另一个类的成员函数当做有元函数   **注意实现顺序问题**

```c++

```





### 2.友元类

_friend修饰的类_



# <font color=purple>五.运算符重载</font>

_赋予运算符具有操作自定义类型的能力  _

实质:函数调用

+ 基本语法: operator 加上运算符组成函数名
+ 函数返回值类型:运算符最终运算结果结束后的结果类型决定
+ 参数:操作数决定 
+ .= () -> []只能重载为类的成员函数
+ 运算符重载必须包含一个自定义类型(结构体或类)
+ . .* ?: ::不能被重载
+ 习惯:
  + 单目运算符用成员函数重载
  + 双目运算符用友元重载

## 1.成员函数重载

+ 参数个数:等于需要运算符操作的参数个数-1

```c++
class A
{
  public:
    A(){}
    A(std::string name):name(name){}
    A operator+(A& temp){}//加法运算符重载  ,参数个数-1 
    protected:
    std::string name;
};
A one("小花");
A two("小黄");
A sum=one+two;//运算符重载          隐式调用
A sum2=one.operator+(two)//        显示调用
```

## 2.友元函数重载

_被 friend修饰的重载函数_

+ 参数个数:等于运算符需要操作的参数个数

```c++
class A
{
  public:
    A(){}
    friend A operator-(A& one,A& two);//两个操作数
    protected:
    std::string name;
};
A operator-(A& one,A& two)//友元函数类外实现
{
    return 
}
```

## 3.流重载

_对输入输出流对象进行重载_

+ cin:	 istream类的对象
+ cout: ostream类的对象

<font color=red>**流 重载必须要用友元重载，并且一定要用引用**</font> 

```c++

```





## 4.前置和后置重载



_针对++运算符_

+ **占位符:** 函数参数，但只包含类型名          _C语言不允许_

```c++
void print(int a,int)//第二个参数是占位符
{
    
    std::cout<<"我是你爸爸";
}
print(1,3);//占位符也需要传参数
```

### 1.前置重载

_没有占位符是前置_

```c++
class MM
{
    public:
    MM(std::string name,int num):name(name),num(num){}
    void print()
    {
        std::cout<<name<<' '<<num<<'\n';
    }
    MM operator++()//前置
    {
        num++;
        return *this;
    }
    protected:
    std::string name;
    int num;
};
```



### 2.后置重载

_有占位符是后置_

```c++
class MM
{
    public:
    MM(std::string name,int num):name(name),num(num){}
    void print()
    {
        std::cout<<name<<' '<<num<<'\n';
    }
    MM operator++()//前置
    {
        this->num++;
        return *this;
    }
    MM operator++( int)//
    {
       
        return MM(this->name,this->num++);
    }
    
    protected:
    std::string name;
    int num;
};
```

## 5.对象的隐式转换

_直接通过对象获取属性/特征_

+ 基本语法: 

```c++
operator 隐式转换的类型()
{
    return 数据成员;//隐式转换的类型要和数据成员的类型一致
}
```

+ 目的:快速获取对象的属性

```c++
class MM
{
    public:
    MM(std::string name,int num):name(name),num(num){}
    operator 
  	protected std::string()
    {
        return name;
    }
    operator int()
    {
        return num;
    }
    std::string name;
    int num;
};
MM girle1("小花", 19);
std::string name=girle1;
std::cout<<name;
```



## 6.文本重载

_后缀重载_

+ 函数名: operator""
+ 返回值
+ 参数名:

# <font color=purple>六.继承</font>

## 1.基础概念

<font color=lightgreen>_直接理解为生物上的继承,通常子类中不会产生新的属性或者行为LIGHTMAGENTA_</font>

## 2.继承

### 1.c++继承要点

+ 继承方式:public protected private



+ 权限问题：
  + 权限限定词只会加深父类属性在子类中的呈现
  + 父类中的私有属性在子类中不能直接访问

+ 构造函数写法:
  + 必须要采用**初始化参数列表方式**调用父类构造函数初始化父类属性

  + <font color=red>**为了子类能够写出无参构造函数，父类构造函数必须存在无参调用形式**</font>
  + 一般情况下子类的构造函数传参一般包含**自身参数**和**父类中的参数**

<font color=blue size=4>**在C++中，子类在继承父类时，会继承父类的所有成员变量和成员函数，包括私有成员。当子类的对象被创建时，它的父类部分会被自动构造。因此，<font color=red>子类的构造函数必须初始化父类的成员变量，否则会导致编译错误或者未定义的行为。</font>**</font>



<font color=red size=3>**子类构造会默认自动调用父类构造函数,以完成对继承来的父类的属性和方法得到初始化**</font>





|   继承方式    | public继承 | protected继承 | private继承 |
| :-----------: | ---------- | ------------- | ----------- |
|  父类public   | public     | protected     | private     |
| 父类protected | protected  | protected     | private     |
|  父类private  | 不可访问   | 不可访问      | 不可访问    |



+ 父类:

```c++
class father
{
    public:
    int num1;
    protected:
    int num2;
    private:
    int num3;
};
```



+ 子类   //父类中的私有属性不能被访问

```c++
class son1:protected father
{
    
};
```

## 3.多继承

_两个及以上的父类_

### 1.构造函数写法

**调用父类构造函数顺序只与继承顺序有关**

```c++
class father1
{
public:
	father1(std::string name1="父亲1") :first_1_name(name1) {}
protected:
	std::string first_1_name;
	
};
class father2
{
public:
	father2(std::string name1="父亲2") :first_2_name(name1) {}
protected:
	std::string first_2_name;


};
class son :public father1,public father2//与继承顺序有关
  //先调用father1，后调用发father2
{
public:
	son(){}
	son() :father1("小花"), father2("小白") {}

protected:
	
};

```



### 2.构造函数与析构顺序问题

### 3.虚继承

![](屏幕截图 2023-05-07 175936.png)

_菱形继承_:用virtual修饰继承得到解决

**错误继承方式：**

```c++
class A
{
public:
	int a;
};
class B :public A
{

};
class C : public A
{

};
class D :public B, public C
{
	void print()
	{
		std::cout << a;//a属性不明确
	}
};

```

**正确继承方式：**

```c++
class A
{
public:
    A(int a),a(a){}
	int a;
};
class B :virtual public A//使用virtual修饰
{
public:
    B(int a):A(a),a(a){}
};
class C : virtual public A//使用virtual修饰
{
	  C(int a):A(a),a(a){}
};
class D :public B, public C
{
    public：
        D(int a):B(1),C(2),A(a){}
	void print()
	{
		std::cout<<A::a<<std::endl;
        std::cout<<B::a<<std::endl;
        std::cout<<C::a<<std::endl;
        std::cout<<D::a<<std::endl;
	}
};

int main()
{
    D d(3);
    //将会打印
    /*
    3
    3
    3
    3
    */
}
```



## 4.继承中的同名问题

_优先调用近的_

## 5.虚函数

_virtual修饰的函数_

### 1.虚函数对于类的影响

+ 会增加一个指针类型的字节 

```c++
#include <iostream>
class MM
{
public:
	virtual void print()
	{
		std::cout << "虚函数" << std::endl;
	}
	virtual void printB()
	{
		std::cout << "3" << std::endl;
	}
protected:
	//int age;

};
int main()
{
	MM vir;
	long long** p = (long long**) (&vir);
	typedef void (*pfun)();
	pfun pone= (void (*)())p[0][0];//访问虚函数表
	pone();
	pfun ptwo = (void (*)())p[0][1];
	ptwo();
}
```



### 2.虚函数表

_虚函数地址会存在在一个二维数组里面,这个二维数组就是虚函数表_

### 3.纯虚函数

+ 写法:

```c++
class MM
{
  public:
    virtual void printf()=0;
};
```



+ 抽象类:具有至少一个纯虚函数的类就是抽象类
  + 不能创建对象
  + 但是可以创建对象指针

```c++
#include <iostream>
class MM
{
public:
	virtual void print() = 0;
};
int main()
{
	MM* one=nullptr;
	
}
```

# <font color=purple>七.多态</font>

_c++类中对象指针(引用)同一种行为的不同结果_

## 1.实现多态的必要因素

+ 存在对象的不正常初始化
  + 父类指针被子类初始化
+ **必须具备同名函数,并且父类中存在虚函数**
+ **一定是public继承** 



<font color=red size=4>**多态的概念并不重要,重要的是知道哪一种行为会调用哪一个函数即可**</font> 





```c++
#include <iostream>
class MM
{
public:
	virtual void printVirtual()
	{
		std::cout << "父类虚函数" << std::endl;
	}
	void print()
	{
		std::cout << "父类普通函数" << std::endl;
	}
};
class boy :public MM
{
public:
	 void printVirtual()
	{
		std::cout << "子类虚函数" << std::endl;
	}
	void print()
	{
		std::cout << "子类普通函数" << std::endl;
	}
	
};
int main()
{
	
	MM* p = new boy;
	p->print();//父类				//多态
	p->printVirtual();//子类
}
```

<font color=red size=6>**有virtual调用看对象类型,无virtual看指针类型**</font>

## 2.虚析构函数

_父类指针被子类初始化时的释放问题_

```c++
class MM
{
  public:
    MM()
    {
        std::cout<<"MM构造"<<std::endl;
    }
    ~MM()//应该写成 virtual ~MM()  //虚析构函数
    {
        std::cout<<"MM析构"<<std::endl;
    }
};
class boy: public MM
{
  public:
    boy()
    {
        std::cout<<"boy构造"<<std::endl;
    }
    ~boy()
    {
        std::cout<<"boy析构"<<std::endl;
    }
};
int main()
{
    MM* p=new boy;
    delete p;
    return 0;
    /*会打印
    MM构造
    boy构造
    MM析构
    *///发现boy并没有释放这个时候就需要虚析构函数了
}
```

## 3.ADT过程

 _父类使用**纯虚函数**实现接口定义(虚函数),子类必须实现才可创建对象的过程_

```c++
class MM
{
    public:
    virtual void printx()=0;
    virtual void printfy()=0;
};
class boy:public MM
{
    public:
    void printx()
    {
        
    }
    void printy()
    {
        
    }
};
```



## 4.继承中的两个关键字

+ final :禁止子类重写被修饰的方法,写在函数后面
+ override:重写检查,写在子类要重写的函数的后面,如果重写函数的名字写错了,就会提示报错



**存在下行转换和上行转换两种形式**



## 5.工厂模式

# 八.c++IO流

## 1.标准输入输出流

要点:流对象的类型->运算符重载

+ 标准输入输出流对象

  + cin：标准输入，可以被重定向
  + cout:标准输出,可以被重定向
  + cerr:标准错误,不可以被重定向
  + clog:标准错误:可以被重定向

  cree和clog用起来和cout没有区别

+ 流对象调用成员函数的方式:主要掌握字符和字符串的输入输出方式

  + int    get():输入字符
  + put():打印字符
  + getline():输入字符串
  + write():打印字符串  

+ 流控制字符:类似C语言的格式控制字符

  + 头文件包含:<iomanip>
  + 流控制字符基本上都有一个成员函数得方式
    + setbase():设置进制
    + setprecision():设置有效位数
    + fixed:结合setprecision()控制小数位位数
    + settiosflangs(ios::mode):设置对齐方式
      + ios::left:左对齐
      + ios::right:右对齐
    + setw(4):设置输出数据的宽度

```c++
std::cout<<std::fixed<<std::setprecision(4)<<123.234355<<std::endl;//输出小数位数为四位的数

//输出为  123.2343
```

## 2.文件流

**头文件:** <fstream>

+ fstream类：可读可写

  + ofdtream类：写操作
  + ifstream类：读操作
  + 打开文件:

  ```c++
  void open(const char* filename,ios::openmode mode);
  ```

  

  + ios::in             ：读·
  + ios::out           :写,不存在则创建
  + ios::app          :追加，具有创建功能
  + ios::ate            :打开已有文件,文件指针在文件末尾
  + ios::trunc        :文件不存在,创建文件
  + ios::binary      :二进制
  + ios::nocreate :不创建
  + ios::replace    :不做替换
  + 组合方式:用|
    + ios::in|ios::out|ios::binary

+ 关闭文件:void close();

+ 文件状态函数:

  + 文件是否为空:

    + bool is_open();
    + !文件对象

  + 是否到达文件末尾

    is_eof();

+ 读写操作

  + 文件流对象结合:<<,>>
  + 字符的方式读写
    + get();
    + put();
  + 调用成员函数完成
    + write():写操作
    + read():读操作
    + 

+ 文件指针移动

  + ifstream类对象

    + ifstream& seekg(long int pos)
    + ifstream& seek(long int pos,ios::base::seekdir pos)

  + ofstream类对象

    + ofstream& seekg(long int pos)
    + ofstream& seek(long int pos,ios::base::seekdir pos)

+ ios::base::seekdir

  + ios::beg:开始位置
  + ios::end :结束位置
  + ios::cur:当前位置
  + 

## 3.字符串流

字符流头文件:sstream

+ istringstream
+ ostringstream

一般我们使用的类是stringstream类

+ string str():获取字符流对象中的字符串
+ void str(const string& str):重置字符流对象中的字符串

一般使用场景有以下两个

+ 数据的类型转换
+ 字符串的切割

```c++

```



数字转字符串:to_string(number);

字符串转数字:



 一个流多次做类型转换一定要clear();

​    

​    

​    

# <font color=purple>九.异常处理 </font> 



## 1.异常处理的机制

_c++异常处理机制是暂缓问题的处理,放到被调函数中去处理_

暂缓不是不处理,是暂缓处理,如果不处理,会引发异常,会调用系统默认函数abort函数终止程序

## 2.什么是异常

任何东西都可以当作是异常,错误是异常的一种

## 3.c++异常关键字

+ try:检查异常
+ throw:抛出异常
+ catch：捕获处理异常



**try和catch的大括号是不能省略的,两者成对出现**

```c++
//抛出异常不做处理

#include <iostream>
int getNumber(int a,int b)
{
    if (b == 0)
    {
        std::cout << "除数不能为零" << std::endl;
        throw std::string("除数不能为零");
    }
    else
    {
        return a / b;
    }
}
int main()
{
    getNumber(1, 0);//会调用标准库的abort函数发送错误信息
    return 0;
}

```

```c++
int main()
{
    try
    {
        getNumber(1,0);
    }
    catch(std::string)  //捕获抛出的数据类型
    {
        std::cout<<"除数不能为零"<<std::endl;
    }
    return 0;
}
```



![](屏幕截图 2023-05-14 140051.png)

​    

    ## 4.无异常函数

```c++
//老版本
//不存在异常 
int Max(int a,int b) throw()//抛出空
{
    return a>b?a:b;
}
//新版本
int Max(int a,int b) noexcept
{
    return a>b?a:b;
}
```



## 5.c++异常处理的其他操作

```c++
//try对应多个catch
{
    
}
catch(int&)
{
    
}
catch(std::string)
{
    
}

try
{
    
}
catch(...)//捕获所有类型的异常 
{
    
}
//抛出自定义类
try
{
    
}
catch(自定义类)
{
    
}
```



    ## 6.c++标准库中的异常

标准库中异常要点:

+ 了解标准库的异常类体系
+ 学会重写类

​    

# <font color=purple>十.c++模板</font>



_把类型当作未知量,在调用时当作参数传入的编程方式_

## 1.函数模板

+ 基本函数模板

```c++
//基本函数模板
template <typename Type1,typename Type2>
Type1 Max(Type1 a,Type2 b)
{
	std::cout<<a<<std::endl;
	std::cout<<b<<std::endl;
	return 0;
}
int main()
{	//显示调用
	Max<int,std::string>(4,"asdf");
    //隐式调用
    Max(2,"年后");//字符串默认推const char*
}

```

+ 类中成员是函数模板

```c++

```

### 3.c++模板其他操作

+ **操作自定义类型:** 

```c++
template <typename type,int size> //size 只能传常量或const 修饰的变量
type* createArray()
{
    type* p=new type[size];
    return p;
}
int main()
{
    int* ps=createArray<int,10>();//只可以显示调用
}
```

### 4.函数模板缺省

```c++
template <typename type=int,typename type2=std::string> //缺省
void print()
{
	std::cout<<type<<std::endl;
    std::cout<<type2<<std::endl;
}
int main()
{
    print("小花",10);//调用方式一
    print();//调用方式2
    print<>(10,"小花");//调用方式3,参数必须与缺省类型一样
    print<char,int>('2',10);//调用方式4
    
}
```



​    

### 5.模板函数与普通函数重载

```c++
template <typename type1,typename type2>
void print(type1 num1,type2 num2)
{
    std::cout<<num1<<std::endl;
    std::cout<<num2<<std::endl;
}
void print(int a,int b)
{
    std::cout<<__FUNCTION__<<std::endl;//宏 打印当前的函数名 __FUNCSIG__ 打印函数签名
     std::cout<<a<<std::endl;
    std::cout<<b<<std::endl;
}
int main()
{
    print<int,int>(2,3);//调用模板函数
    print(2,3);//优先调用普通函数
    
}
```

### 6.模板函数与模板函数重载

+ **优先调用传参数少的函数**

## 2.类模板

+ 类模板不是一个完整的类,使用类型时必须用 类名<未知类型> 的用法
  + 多文件中不能分文件写,必须写在一起你
+ 必须现实调用,不能隐式调用



    ## 3.c++类模板的其他操作

### 1.特化操作(特化  :)

 

​    

​    

​    
