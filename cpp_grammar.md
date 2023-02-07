

# C++语法

## 虚函数与纯虚函数

```c++
// 虚函数 在基类中定义后还可以在子类中覆盖定义，在程序运行时决定调用子类或是基类中的函数
// 纯虚函数 在基类中声明 在子类中定义 拥有纯虚函数的类被称为抽象类 不可被实例化
//virtual实现了动态联编，它可以在运行时判断指针指向的对象，并自动调用相应的函数
class A
{
public:
    A();
    ~A();
    virtual int fun1();// 虚函数
    virtual int fun2()=0;// 纯虚函数
};

int A::fun1()
{
    s1;
    s2;
    return 0;
}

class B:A
{
public:
    B();
    ~B();
    int fun2();
}
int B::fun2()
{
    s1;
    s2;
    return 0;
}

// 动态连编与静态连编

```



## 静态函数
```c++
#include <stdio.h>
using namespace std;

class Stu
{
	public:
	// 创建静态成员方法 创建并返回Stu对象
		static Stu* getStu(void)
		{
			static Stu *stu = NULL; 
			return stu;
		}
		Stu();
		~Stu();
		void print(int id, int score);
};

int main()
{
	Stu::getStu()->print(1, 99);// 使用静态方法得到Stu对象并调用成员方法print()
	return 0;
}

void Stu::print(int id, int score)
{
	printf("%d ", id);
	printf("%d ", score);
}
```

## 函数指针和指针函数
```c++
//指针函数
T* func(T para1, T para2 )
{
      expression1;
	return (T*)var; 
}
//函数指针
T (*func)(T para1, T para2)
{
	expression1;
	return (T)var; 
}
fun = [&]func;
x = (*func)(T para1, T para2);
// 可以用来为函数设置别名
```

## 常用预定义宏

```c++
// __LINE__ 当前行号
// __FILE__ 当前文件名
// __TIME__ 编译文件时间
// __DATE__ 编译文件日期
// __func__ 所在函数名
```

## 宏定义语法

```c++
#define FUN(s) #s //将宏参数变为字符串 
#define FUN(a, b) int(a##e##b) // 将两个宏参数粘合在一起 

FUN(2, 3); // 2e3
FUN(s); // "s"
#define TODO do { /*TODO*/ } while(0) // 防止宏的使用者编译出错
```

## goto语句

```c++
// goto语句依次执行标签语句
// 遇到goto时跳转到相应标签语句执行
loop:
	p1;
	p2;
loop2:
	p3;
	p4;
	goto loop3;
...
loop3:
	p4;
	p5;
	goto exit;
...
exit:
	exit(1);
```

## 函数指针

```c++
// 函数指针定义
// 返回值 (指针变量名)(参数列表1, 参数列表2, ...)
// {
//    函数体;
// }

e.g. 
void (*max_p)(int x, int y)
{
	return (x>y)?x:y;
}
/*函数指针和指针函数*/
//指针函数
T* func(T param1, T param2)
{
      expression1;
	return (T*)var; 
}

//函数指针
T (*func)(T para1, T para2)
{
	expression1;
	return (T)var; 
}

fun = [&]func;
x = (*func)(T para1, T para2);
// 可以用来为函数设置别名
```

## C++多维数组

```c++
// method1
int *array;
array = (int *)malloc(sizeof(int)* 5);
// method2
int array[5]；
array[1] = 1;
// 二维数组
// method1
int array[2][2];
*((*array + 1) + 1) = 1;
array[1][1] = 1;
```

## 指针和`const`

### 指向常量的指针
```c++
/*指向对象的cosnt指针*/
int age = 18;
const int* pt = &age;
/*指向const对象的指针*/
int sloth = 3;
int* const finger = &sloth;
/*指向const对象的const指针*/
double trouble = 2.0E30;
const double* const stick = &trouble;

// 防止修改pt指向的值
int age = 18;
const int* pt = &age;
// 修改pt指向的变量值
*pt += 2; // invalid
*pt = 20; // invalid
age = 20; // valid
// 防止修改指针的值
int sloth = 3;
const int* ps = &sloth;

int* const finger = &sloth;// 无法修改finger指向的地址，但可以通过*finger修改finger指向的变量的值

// 将const变量的地址赋值给指向const的指针
const float g_earth = 9.8;
const float *pe = g_earth;
// 将const的地址赋值给常规指针
const float g_moon = 1.63;
float* pm = &g_moon; // invalid
```

### 指向指针的指针
```c++
// 一级间接关系时 非const地址或指针允许赋给const指针
int age = 39;
int *pd = &age;
const int* pt = pd;
// 二级间接关系
const int* pp2;
int *p1;
const int n = 13;
pp2 = &p1;
*pp2 = &n; // 将p1指向n， 即p1的地址赋值给p1
*p1 = 10; // 改变了const变量n的值
```

## 函数和指针
### 数组指针和指针数组

```c++
// 数组指针
int array[3] = { x, y, z };
int(*pd1)[3] = &array;
std::cout << (*pd1)[0];
std::cout << (*pd1)[1];
// 指针数组
int *pd1[3]; // 存放变量指针
```

## 函数和结构体

### 使用cin实现循环输入

```c++
// method1
int x = 0, y = 0;
while(std::cin >> x >> y)// 连续赋值 输入类型与所给变量类型不匹配，返回false，否则返回true
    break;
// method2 q
for(int i = 0;i < limit; i++)
{
    int temp = -1;
    cout << "Enter a number #" << i+1 << ": ";
    cin >> temp;
    if(temp < 0)
        break;
    ar[i] = temp;
}
```

## 函数和二维数组
### 通过数组指针使用数组元素

```c++
  int data[3][4];// data为数组第一个元素的地址
  data[1][2] == *(*(data + 1) + 2);
  
```
### 二维数组作为函数参数

```c++
int data[3][4];
int init2DArray(int (*arr2)[4], int size);
int init2DArray(int arr2[][4], int size);
// 通过数组指针使用数组元素
int data[3][4];// data为数组第一个元素的地址
data[1][2] == *(*(data + 1) + 2);
```
## 函数模板

```c++
// 函数模板声明
template <typename T>
void swap(T, T);
template <> void swap<int>(int, int);// 显式实例化声明 使用模板生成函数实例
template void swap<int>(int, int);// 显式具体化声明 不使用模板生成函数定义

// 后置函数声明
auto swap(int, int) -> void;
```

## 名称空间

```c++
namespace space1
{
    int p1 = 0;
    int show()
    {
        std::cout << "space1::show()" << '\n';
    }
    namespace space1_1
    {
    	int p1 = 0;
        int show()
        {
            std::cout << "space1_1::show()" << '\n';
        }
	}
}

namespace space2
{
    int p1 = 1;
    int show()
    {
        std::cout << "space2::show()" << '\n';
    }
}
```

## 类转换函数

```c++
class Stu
{
private:
    int m_Id;
public:
    //转换函数，将类类型转化为自定义类型
    operator int() const
    {
        return m_id;
    }
};

//e.g.
Stu stu();
int id = stu;// 取得Stu类成员的值+
```



# Chapter 10 对象和类

## 1.POP和OOP

- 面向过程(POP):运行步骤,表示数据
- 面向对象(OOP):描述数据和接口，实现数据和接口操作

## 2.抽象和类

- 类型声明
  - 指定对象需要的内存
  - 指定内存的结构
  - 指定对象的执行操作
- 类的定义
- 接口
- 客户--服务器模型

## 3.构造函数和析构函数

- 构造函数

  - 默认构造函数:用于未提供显式初始值

  ```c++
  Student stu;// 默认构造函数初始化对象
  /*三种方式创建对象*/
  Student stu(0, "Jack");
  Student stu = Stu(0, "Jack");
  Student *stu = new Stu(0, "Jack");// 使用new创建对象，在对象不再使用时必须使用delete释放对象
  
  Student stu = "Jack";//接受一个参数的构造函数可使用赋值初始化对象 不推荐
  ```

- 析构函数

  三种创建对象后调用析构函数的时间：

  - 静态存储类对象
  - 自动存储类对象
  - new创建对象

- 列表初始化语法

  ```c++
  Student stu = {0, "Jack"};
  Student stu{0, "Jack"};
  Student *stu = new Student{0, "Jack"};
  ```

- const成员函数

  ```c++
  //只要方法不修改对象，应将其声明为const
  void Student::show() const
  {
      cout << "Id   =" << m_Id << endl;
      cout << "Name =" << m_Name << endl;
  }
  ```

## 4.this指针

- `this`指针指向调用成员函数的对象

  ```c++
  const Student& Student::Compare(const Student& s) const
  {
      if(s.m_score > m_score)
      	return s;
      else
          return *this;//获取this指向的对象需要对其进行解引用操作
  }
  ```

## 5.对象数组

- 创建并初始化对象数组

  ```c++
  Student stuArray[3];// 使用默认构造函数
  Student stuArray[3] = {
      Student(0, "Jack"),
      Student(1, "Tom"),
      Student(2, "Jane")
  }
  Student* stuArray[3] = {
      new Student(0, "Jack"),
      new Student(1, "Tom"),
      new Student(2, "Jane")
  }
  ```

## 6.类作用域

- 类作用域常量

  ```c++
  class School
  {    
  private:
      static const int people = 1000;
  }
  ```

- 类作用域枚举

  ```c++
  enum class color {Red, Green, Blue};
  color mycolor = color::Red;// 使用枚举名来限定枚举量
  int value = color::Red; //error, 不能隐式转换类型
  ```

  ## 7.抽象数据类型（ADT）

  ```c++
  typedef int Item;
  class Student
  {
  private:
      Item m_Id;
  public:
      Student(I);
      void show();
  }
  ```
# Chapter14 C++中的代码重用

## 1.包含对象成员的类



## 2.私有继承



  
