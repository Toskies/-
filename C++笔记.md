# C++

## 细节知识点

参考：
		[C++教程](https://blog.csdn.net/qq_33670157/article/details/104455787)

### 1. typedef声明

```c++
//使用typedef为一个已有的类型取一个新的名字,语法如下：
typedef type newname
//eg：
typedef int feet
feet distance
```

### 2. 枚举类型enum	

```c++
//枚举类型的语法:
enum 枚举名{
	标识符[=整型常数], 
     标识符[=整型常数], 
... 
    标识符[=整型常数]
}枚举变量;
enum course {math,chinese,english,physics,chemistry}c;
c = english;
cout<<c<<endl;  //2
//english为1 physics为2 chemistry为3，chinese仍为1，math仍为0
enum course {math,chinese,english=1,physics,chemistry};
```

### 3. 变量

==变量的声明不分配内存，变量定义要给变量分配内存空间，；定义可以初始化，声明不能。==
分为 局部变量、全局变量；

#### 运算符优先级

 1）按单目、双目、三目、赋值依次降低
 2）按算术、移位、关系、逻辑位、逻辑依次降低

![运算符优先级](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210629205044551.png)

### 4. switch结构

```c++
char c = 'A';
	switch (c){
		case 'A':
		case 'B':
		case 'C':
			cout << "及格了" << endl;
			break;
		default:
			cout << "不及格" << endl;
	}
```

### 5. 三目运算符

```c++
//如果 Exp1 为真，则执行 Exp2。如果Exp1为假，则执行Exp3
Exp1 ? Exp2 : Exp3;
```

### 6. 预处理命令

预处理程序（删除程序注释，执行预处理命令等）–>编译器编译源程序；

1. 宏定义：`#define 标识符 字符串`

2. 文件包含：`\#include<filename> 或者#include“filename”`

3. 条件编译：

   ```c++
   //如果标识符被#define定义过，执行程序段1，否则执行程序段2
   #ifdef 标识符
   	程序段1
   #else
   	程序段2
   #endif
   //如果标识符没有被#define定义过，执行程序段1，否则执行程序段2
   #ifndef 标识符
   	程序段1
   #else
   	程序段2
   #endif
   //如果表达式为true，执行程序段1，否则执行程序段2
   #if 表达式
   	程序段1
   #else
   	程序段2
   #endif     
   ```

### 7. 数组与new（动态创建数组）


```c++
一维：
int* arr1 = new int[2];//delete []arr1;
int* arr2 = new int[3]{ 1,2 };//delete []arr2
二维：
int m=2, n=3;
int** arr3 = new int*[2];//delete []arr3
for (int i = 0; i < 10; ++i)
{ 
	arr3[i] = new int[3]; // delete []arr3[i]
}
int* arr4 = new int[m*n];//数据按行存储 delete []arr3
```

### 8. 数组与函数

==如果传递二维数组，形参必须制定第二维的长度。==
形式参数是一个指针：`void function(int *param)`
形式参数是一个已定义大小的数组：`void function(int param[10])`
形式参数是一个未定义大小的数组：`void function(int param[])`
二维数组：`void function(int a[][3],int size)`
==C++ 不支持在函数外返回局部变量的地址，除非定义局部变量为 static 变量==

- **获取数组的大小**

==动态创建(new)的基本数据类型数组无法取得数组大小==

```c++
int a[3];
//第一种方法
cout<<sizeof(a)/sizeof(a[0])<<endl;
//第二种方法
cout << end(a) - begin(a) << endl;
//二维数组
int arr[5][3];
int lines = sizeof(arr) / sizeof(arr[0][0]);
int row = sizeof(arr) / sizeof(arr[0]);//行
int col = lines / row;//列
cout << row << "::"<<col << endl;
cout << end(arr) - begin(arr) << endl;//5行
```

### 9. 函数

==函数声明中，参数名可以省略，参数类型和函数的类型不能省略==
**形参**：函数定义后面括号里的参数，函数调用前不占内存。
**实参**：函数调用括号里的参数，可以是常量，变量或表达式等。
**形参和实参必须个数相同、类型一致，顺序一致**

==**函数传递方式**：**传值**，**指针**，**引用**==

```c++
//传值-修改函数内的形式参数对实际参数没有影响
int add(int value)
{
	value++;
	return value;
}
int main()
{
	int v = 10;
	cout << "add() = " << add(v) << endl;//add() = 11
		cout << "v = " << v << endl;//v = 10
	return 0;
}
//指针-修改形式参数会影响实际参数
int add(int* pValue)
{
	(*pValue)++;
	return *pValue;
}
int main()
{
	int v = 10;
	cout << "add() = " << add(&v) << endl;//add() = 11
	cout << "v = " << v << endl;//v = 11
	return 0;
}
//引用-修改形式参数会影响实际参数
int add(int &value)
{
	value++;
	return value;
}
int main()
{
	int v = 10;
	cout << "add() = " << add(v) << endl;//add() = 11
	cout << "v = " << v << endl;//v = 11
	return 0;
}
```

#### ==**函数重载**==

同一个函数名对应不同的函数实现，每一类实现对应着一个函数体，名字相同，功能相同，只是参数的类型或参数的个数不同。
**多个同名函数只是函数类型（函数返回值类型）不同时，它们不是重载函数**

#### ==**函数覆盖**==

函数覆盖发生在子类与父类之间。函数在子类和父类中具有相同的函数原型（函数名、参数列表），在调用函数过程中，**根据对象的类型，调用相应类中的虚函数**。

#### 	==**“名字隐藏”**==

​		指的是**父类中有一组重载函数**，**子类**在继承父类的时候如果覆盖了**这组重载函数中的任意一个**，	则**其余没有被覆盖的同名函数在子类是不可见的**。

```C++
class Base
{
public:
	virtual void print(int a)
	{
		cout << "Base print int " << a << endl;
	}
 
	virtual void print(char a)
	{
		cout << "Base print char " << a << endl;
	}
 
	virtual void print(double a)
	{
		cout << "Base print double " << a << endl;
	}
};
 
class Derived :public Base
{
public:
	void print(int a)
	{
		cout << "Base print int " << a << endl;
	}
};
 
int main()
{
	Derived d;
	d.print(10);
	d.print(5.88);
	d.print('d');
	system("pause");
	return 0;
}
```

![输出结果](https://img-blog.csdnimg.cn/20190318094030590.png)

​		Derived类只覆盖了Base类中一组重载函数的一个，因此参数类型为double何char的两个重载函数对于Derived类是不可见的，但是程序没有报错，原因是double类型和char类型都可以自动转换成int类型。就是所谓的“名字隐藏”。
​		解决这种名字隐藏的办法有两个：（1）在子类中不适用函数覆盖，而是给子类的方法选择一个不同的函数名，区别于父类的方法。（2）子类覆盖父类中所有的重载方法，虽然这些重载方法中在子类中和父类中的实现完全一致，但是与第一种解决办法相比这样做的好处是不添加新的函数名。

**==函数重载与函数覆盖区别==**

1. 函数重载是同一类中的不同方法，函数覆盖是不同类中的同一方法；
2. 重载函数的参数列表不同，覆盖函数的参数列表相同；
3. 重载函数调用时根据参数类型选方法，覆盖函数调用时根据对象类型选择方法。

#### ==**内联（inline）函数**==

c++在==**编译**==时可以讲调用的函数代码嵌入到主调函数中，这种嵌入到主调函数中的函数称为内联函数，又称为内嵌函数或内置函数。

- 定义内联函数时，在函数定义和函数原型声明时都使用inline，也可以只在其中一处使用，其效果一样。
- 内联函数在编译时用内联函数函数的函数体替换,所以**不发生函数调用**，不需要保护现场，恢复现场，节省了开销。
- 内联函数增加了目标程序的代码量。因此，**一般只将函数规模很小且使用频繁的函数声明为内联函数**。
- 当内联函数中实现过于复杂时，编译器会将它作为一个普通函数处理,所以**内联函数内不能包含循环语句和switch语句**。



### 10. 字符串（string）

#### C风格字符串

```C
#include <stdio.h>
#include <string.h>
//初始化：
char a[5]
//字符个数不够，补0; 字符个数超过报错
char str[7] = {'h','e','i','r','e','n'};
char str[] = {'h','e','i','r','e','n'};
cin>>str;//输入 输入字符串长度一定小于已定义的字符数组长度
cout<<str;//输出

//字符串函数：
strcat(char s1[],const char s2[]);//将s2接到s1上
strcpy(char s1[],const char s2[]);//将s2复制到s1上
strcmp(const char s1[],const char s2[]);//比较s1,s2 s1>s2返回1 相等返回0，否则返回-1
strlen(char s[]);//计算字符串s的长度 字符串s的实际长度，不包括\0在内
```

#### C++字符串

C风格字符串(以空字符结尾的字符数组)太过复杂难于掌握，不适合大程序的开发，所以C++标准库定义了一种string类，定义在头文件<string>。
String和c风格字符串对比：

- Char*是一个指针，String是一个类
  string封装了char*，管理这个字符串，是一个char*型的容器。
- String封装了很多实用的成员方法
  查找find，拷贝copy，删除delete 替换replace，插入insert
- 不用考虑内存释放和越界
  string管理char*所分配的内存。每一次string的复制，取值都由string类负责维护，不用担心复制越界和取值越界等。

```c++
//定义
string 变量;
string str1;
//赋值
string str2 = "ShangHai";
string str3 = str2;
str3[3] = '2';//对某个字符赋值
//字符串数组
string 数组名[常量表达式]
string arr[3];

//处理函数
#include <iostream>
#include <algorithm>
#include <string>
//构造初始化
string str;//生成空字符串
string s(str);//生成字符串为str的复制品
string s(str, strbegin,strlen);//将字符串str中从下标strbegin开始、长度为strlen的部分作为字符串初值
string s(cstr, char_len);//以C_string类型cstr的前char_len个字符串作为字符串s的初值
string s(num ,c);//生成num个c字符的字符串
string s(str, stridx);//将字符串str中从下标stridx开始到字符串结束的位置作为字符串初值

size()和length();//返回string对象的字符个数
max_size();//返回string对象最多包含的字符数，超出会抛出length_error异常
capacity();//重新分配内存之前，string对象能包含的最大字符数
>,>=,<,<=,==,!=//支持string与C-string的比较(如 str<”hello”)。  使用>,>=,<,<=这些操作符的时候是根据“当前字符特性”将字符按字典顺序进行逐一得 比较，string (“aaaa”) <string(aaaaa)。    
compare();//支持多参数处理，支持用索引值和长度定位子串来进行比较。返回一个整数来表示比较结果，返回值意义如下：0：相等 1：大于 -1：
  
push_back() 
insert( size_type index, size_type count, CharT ch );//在index位置插入count个字符ch
insert( size_type index, const CharT* s );//index位置插入一个常量字符串
insert( size_type index, const CharT* s, size_type n);//index位置插入常量字符串中的count个字符
insert( size_type index, const basic_string& str );//index位置插入常量string
insert( size_type index, const basic_string& str, size_type index_str, size_type n);//index位置插入常量str的从index_str开始的n个字符
insert( size_type index, const basic_string& str,size_type index_str, size_type count = npos);//index位置插入常量str从index_str开始的count个字符，count可以表示的最大值为npos.这个函数不构成重载 npos表示一个常数，表示size_t的最大值，string的find函数如果未找到指定字符，返回的就是一个npos
iterator insert( iterator pos, CharT ch );//pos位置插入ch
iterator insert( const_iterator pos, CharT ch );//pos位置插入。const_iterator只能读取容器元素，不能修改容器元素
void insert( iterator pos, size_type n, CharT ch );//迭代器指向的pos位置插入n个字符ch
iterator insert( const_iterator pos, size_type count, CharT ch );//迭代器指向的pos位置插入count个字符ch
void insert( iterator pos, InputIt first, InputIt last );
iterator insert( const_iterator pos, InputIt first, InputIt last );
append() 和 + 操作符
//访问string每个字符串
string s1("yuanrui"); // 调用一次构造函数
// 方法一： 下标法
for( int i = 0; i < s1.size() ; i++ )
     cout<<s1[i];
// 方法二：正向迭代器
for( string::iterator iter = s1.begin();; iter < s1.end() ; iter++)
     cout<<*iter;
 // 方法三：反向迭代器
for(string::reverse_iterator riter = s1.rbegin(); ; riter < s1.rend() ; riter++)
     cout<<*riter;
iterator erase(iterator p);//删除字符串中p所指的字符
iterator erase(iterator first, iterator last);//删除字符串中迭代器区间[first,last)上所有字符
string& erase(size_t pos = 0, size_t len = npos);//删除字符串中从索引位置pos开始的len个字符
void clear();//删除字符串中所有字符
string& replace(size_t pos, size_t n, const char *s);//将当前字符串从pos索引开始的n个字符，替换成字符串s
string& replace(size_t pos, size_t n, size_t n1, char c); //将当前字符串从pos索引开始的n个字符，替换成n1个字符c
string& replace(iterator i1, iterator i2, const char* s);//将当前字符串[i1,i2)区间中的字符串替换为字符串s
//tolower()->转换成小写  toupper()函数->转换成大写 或者 STL中的transform算法（下文细讲）作用是 将一个容器中的值搬运到另一个容器中
string s = "ABCDEFG";
for( int i = 0; i < s.size(); i++ )
     s[i] = tolower(s[i]);
transform(s.begin(),s.end(),s.begin(),::tolower);
size_t find (constchar* s, size_t pos = 0) const;//在当前字符串的pos索引位置开始，查找子串s，返回找到的位置索引，-1表示查找不到子串
size_t find (charc, size_t pos = 0) const;//在当前字符串的pos索引位置开始，查找字符c，返回找到的位置索引，-1表示查找不到字符
size_t rfind (constchar* s, size_t pos = npos) const;//在当前字符串的pos索引位置开始，反向查找子串s，返回找到的位置索引，-1表示查找不到子串
size_t rfind (charc, size_t pos = npos) const;//在当前字符串的pos索引位置开始，反向查找字符c，返回找到的位置索引，-1表示查找不到字符
size_tfind_first_of (const char* s, size_t pos = 0) const;//在当前字符串的pos索引位置开始，查找第一个位于子串s的字符，返回找到的位置索引，-1表示查找不到字符
size_tfind_first_not_of (const char* s, size_t pos = 0) const;//在当前字符串的pos索引位置开始，查找第一个不位于子串s的字符，返回找到的位置索引，-1表示查找不到字符
size_t find_last_of(const char* s, size_t pos = npos) const;//在当前字符串的pos索引位置开始，查找最后一个位于子串s的字符，返回找到的位置索引，-1表示查找不到字符
size_tfind_last_not_of (const char* s, size_t pos = npos) const;//在当前字符串的pos索引位置开始，查找最后一个不位于子串s的字符，返回找到的位置索引，-1表示查找不到子串
sort(s.begin(),s.end());//排序
substr(pos,n);//返回字符串从下标pos开始n个字符
strtok(char *str, const char *delim);//分解字符串 str 为一组字符串，delim 为分隔符
char str[] = "I,am,a,student; hello world!";
const char *split = ",; !";
char *p2 = strtok(str,split);
while( p2 != NULL )
{
    cout<<p2<<endl;
    p2 = strtok(NULL,split);
}
```

### 11. 指针

​	两个相同数据类型的指针可以进行加减运算，一般用于数组的操作中。

```c++
int arr[10],len;
int *p1 = &arr[2],*p2 = &arr[5];
 len = p2-p1;//arr[2] 和arr[5]之间的元素个数 3
```

#### new和delete运算符

```C++
指针变量 = new 数据类型(初值);  //new-为变量分配内存空间；
delete 指针变量;
delete[] 指针变量;   //释放为多个变量分配的地址
int *ip;
ip= new int(1);
delete ip;
int *ip;
 ip= new int[10];
 for (int i = 0; i < 10;i++)
 {
	 ip[i] = i;
 }
 delete[] ip;
int a[3][4] = {0};
```

#### 指针与数组

```
int arr[10];
int *p1 = arr;// *p1 = &arr[0];
int a[3][5] = { 0 };
int(*ap)[5];	//指针访问二维数组：指向二维数组元素，指向一维数组
ap = a;
ap+1;//表示下一个一维数组
```

### 12. 引用

引用型变量声明：`数据类型 &引用名 = 变量名;`
==引用可以看做是数据的一个别名==，通过这个别名和原来的名字都能够找到这份数据，类似于window中的快捷方式。
==引用不占内存空间，**必须在定义的同时初始化**==，且不能再引用其他数据。
引用在定义时需要添加&，在使用时不能添加&，使用时添加&表示取地址。

==将引用作为函数返回值时不能返回局部数据的引用，因为当函数调用完成后局部数据就会被销毁。==函数在栈上运行，函数掉用完，后面的函数调用会覆盖之前函数的局部数据。

### 13. **结构体struct**

+ 对结构体变量的成员引用：`结构体变量名.成员名`
+ 指向结构体的指针变量引用格式：`指针变量名->成员名;`
+ 具有相同类型的结构体变量可以进行赋值运算，但是不能输入输出

### 14. 共用体union

  几个不同的变量共享同一个地址开始的内存空间。

  - 成员类型可以是基本数据类型，也可以是构造数据类型。
  - 公用体变量初始化时，只能对第一个成员赋值。
  - 公用体变量所占的内存长度等于最长的成员长度。
  - 公用体变量在一个时刻只能一个成员发挥作用，赋值时，成员之间会互相覆盖，最后一次被赋值的成员起作用。

### 15. 类

  ==类也是一种数据类型==

  ```c++
  class 类名
  {
  	public:
  		公有数据成员;
  		公有成员函数;
  	private:
  		私有数据成员;
  		私有成员函数;
  	protected:
  		保护数据成员;
  		保护成员函数;
  };
  //类外
  返回类型 类名:成员函数名(参数列表)
  {
  	函数体;
  }
  //内联函数：类外
  inline 返回类型 类名:成员函数名(参数列表)
  {
  	函数体;
  }
  ```

==成员访问权限==

![image-20210701165559634](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210701165559634.png)

#### ==对象==

**不可以在定义类的同时对其数据成员进行初始化，因为类不是一个实体，不合法但是能编译运行**
对象成员的引用：`对象名.数据成员名 或者 对象名.成员函数名(参数列表)`

```C++
//1.声明类同时定义对象
class 类名
{
	类体;
}对象名列表;
//2.先声明类，再定义对象
类名 对象名(参数列表);//参数列表为空时，()可以不写
//3. 不出现类名，直接定义对象
class 
{
	类体;
}对象名列表;
//4.在堆上创建对象
Person p(123, "yar");//在栈上创建对象
Person *pp = new Person(234,"yar");//在堆上创建对象
```

##### 构造函数

特殊的成员函数，主要功能是**为对象分配存储空间**，以及**为类成员变量赋初值**

1. **构造函数名必须与类名相同**
2. **没有任何返回值和返回类型**
3. **创建对象自动调用**，不需要用户来调用，且只调用一次
4. 类没有定义任何构造函数，编译系统会自动为这个类生成一个默认的无参构造函数

```c++
//1.类中定义 2.类中声明，类外定义
[类名::]构造函数名(参数列表)
{
	函数体
}
```

**带默认参数的构造函数**

```C++
class Person
{
public:
	Person(int = 0,string = "张三");
	void show();
private:
	int age;
	string name;
};
Person::Person(int a, string s)
{
	cout<<a<<" "<<s<<endl;
	age = a;
	name = s;
}
void Person::show()
{
	cout << "age="<<age << endl;
	cout << "name=" <<name << endl;
}
int main()
{
     Person p; //0 张三
	Person p2(12);//12 张三
	Person p3(123, "yar");//123 yar
	return 0;
}
```

**带参数初始化表的构造函数**

```C++
类名::构造函数名(参数列表):参数初始化表
{
	函数体;
}
参数初始化列表的一般形式：
参数名1(初值1),参数名2(初值2),...,参数名n(初值n)
class Person
{
public:
	Person(int = 0,string = "张三");
	void show();
private:
	int age;
	string name;
};
Person::Person(int a, string s):age(a),name(s)
{
	cout << a << " " << s << endl;
}
```

**构造函数重载：构造函数名字相同，参数个数和参数类型不一样。**

##### 拷贝构造函数

```C++
//如果类的设计者不写复制构造函数，编译器就会自动生成复制构造函数。大多数情况下，其作用是实现从源对象到目标对象逐个字节的复制，即使得目标对象的每个成员变量都变得和源对象相等。
类名::类名(类名&对象名)
{
	函数体;
}
```

##### 析构函数

特殊的成员函数，当对象的生命周期结束时，用来**释放分配给对象的内存空间**，并做一些清理的工作。

1. 析构函数名与类名必须相同。
2. 析构函数名前面必须加一个波浪号~。
3. 有参数，没有返回值，不能重载。
4. 一个类中只能有一个析构函数；
5. 没有定义析构函数，编译系统会自动为和这个类生成一个默认的析构函数。

```
//1.类中定义 2.类中声明，类外定义
[类名::]~析构函数名()
{
	函数体;
}
```

##### 对象指针

```C++
类名 *对象指针名;
对象指针 = &对象名;
//访问对象成员
对象指针->数据成员名
对象指针->成员函数名(参数列表)
Person p(123, "yar");
Person* pp = &p;
Person* pp2 = new Person(234,"yar")
pp->show();
```

#### ==this指针==

​	**每个成员函数都有一个特殊的指针this，它始终指向==当前被调用的成员函数操作的对象==**

```C++
class Person
{
public:
	Person(int = 0,string = "张三");
	void show();
private:
	int age;
	string name;
};
Person::Person(int a, string s):age(a),name(s)
{
	cout << a << " " << s << endl;
}
void Person::show()
{
	cout << "age="<<this->age << endl;
	cout << "name=" <<this->name << endl;
}
```

### 16. 静态变量

以关键字static开头的成员为静态成员，多个对象共享。
==static 成员变量属于类，不属于某个具体的对象
静态成员函数只能访问类中静态数据成员==

```c++
//类内声明，类外定义
class xxx
{
	static 数据类型 静态数据成员名;
	static 返回值类型 静态成员函数名(参数列表);
}

数据类型 类名::静态数据成员名=初值;

返回值类型 类名::静态成员函数名(参数列表)
{
	函数体;
}
//访问
类名::静态数据成员名;
对象名.静态数据成员名;
对象指针名->静态数据成员名;
类名::静态成员函数名(参数列表);
对象名.静态成员函数名(参数列表);
对象指针名->静态成员函数名(参数列表);
```

### 17. 友元friend

友元是一种**定义在类外部**的普通函数或类，但它需要**在类体内进行说明**，为了与该类的成员函数加以区别，在说明时前面加以关键字friend。**友元不是成员函数，但是它可以访问类中的私有成员**。
==**友元是赋予全局函数，类，类的成员函数访问其他类的私有成员的权限。**==

#### **全局函数做友元**

==友元函数是能够访问类中的私有成员的非成员函数。==友元函数从语法上看，它与普通函数一样，即在定义上和调用上与普通函数一样。

```c++
class Per
{
	//声明这个全局函数为Per类的友元函数
	friend void goodFriend(Per& p);
public:
	Per()
	{
		pen = "钢笔";
		money = "人民币";
	}
public:
	string pen;
private:
	string money;
};
//定义普通朋友函数
void friends(Per& p)
{
	cout << "朋友想借:" << p.pen << endl;//可以访问
	//cout << "朋友想借:" << p.money << endl;//不可以访问
}
//定义好朋友普通函数
void goodFriend(Per& p)
{
	cout << "好朋友想借" << p.pen << endl;
	cout << "好朋友想借" << p.money << endl;//友元函数可以访问类的私有权限
}
void test()
{
	Per p;
	friends(p);
	goodFriend(p);
}
```

#### **友元类**

当一个类作为另一个类的友元时，这就意味着这个类的所有成员函数都是另一个类的友元函数，都可以访问另一个类中的隐藏信息（包括私有成员和保护成员）。

- ==**友元关系不能被继承。**==
- **==友元关系是单向的==，不具有交换性。若类B是类A的友元，类A不一定是类B的友元，要看在类中是否有相应的声明。**
- **==友元关系不具有传递性。==若类B是类A的友元，类C是B的友元，类C不一定是类A的友元，同样要看类中是否有相应的申明。**

==**通过传入参数来访问类的私有成员：**==

```c++
class Per
{
	//声明Gf为Per类的友元类
	friend class Gf;
public:
	Per()
	{
		pen = "钢笔";
		money = "人民币";
	}
public:
	string pen;
private:
	string money;
};
class Gf
{
public:
	void test(Per& p)
	{
		cout << "好朋友想借" << p.pen << endl;
		cout << "好朋友想借" << p.money << endl;友元类可以访问私有成员
	}
};
//通过传入参数访问访问类的私有成员
void test()
{
	Per p;
	Gf f;
	f.test(p);
}
```

==**通过类内指针来访问类的私有成员**==

```C++
class Per
{
	//声明Gf为Per类的友元类
	friend class Gf;
public:
	Per()
	{
		pen = "钢笔";
		money = "人民币";
	}
public:
	string pen;
private:
	string money;
};
class Gf
{
public:
	Gf()
	{
		cout << "无参构造" << endl;
		//申请空间
		m_p = new Per;
	}
	void fun()
	{
		cout << "好朋友想借" << m_p->pen << endl;
		cout << "好朋友想借" << m_p->money << endl;//通过成员指针访问私有成员
	}
	Gf(const Gf& f)//防止浅拷贝
	{
		cout << "拷贝构造函数" << endl;
		//申请空间
		m_p = new Per;
	}
	~Gf()
	{
		cout << "析构函数" << endl;
		if(m_p != NULL)
		{
			delete m_p;
		}
	}
public:
	Per* m_p;
};
void test()
{
	Gf f1;
	f1.fun();
}
```

 	3. **类的成员函数做友元**

```c++
class Per;//声明类
class Gf
{
public:
	void fun(Per& p);
};
class Per
{
	//声明Gf类的成员函数为Per类的友元函数
	friend void Gf::fun(Per& p);
public:
	Per()
	{
		pen = "钢笔";
		money = "人民币";
	}
public:
	string pen;
private:
	string money;
};
void Gf::fun(Per& p)
{
	cout << "好朋友借" << p.pen << endl;
	cout << "好朋友借" << p.money << endl;
}
void test()
{
	Per p;
	Gf f;
	Gf.fun(p);
}
```

### 18. 类(class)与结构体(struct)的区别

- 引入C语言的结构体，是为了保证和c程序的兼容性。
- c语言中的结构体不允许定义函数成员，且没有访问控制权限的属性。
- c++为结构体引入了成员函数，访问控制权限，继承，多态等面向对象特性。
- c语言中，空结构体的大小为0，而C++中空结构体大小为1。
- **class中成员默认是private,struct中的成员默认是public。**
- **class继承默认是private继承，而struct继承默认是public继承。**
- **class可以使用模版，而struct不能。**

### 19. 继承和派生

#### 继承

​	继承就是再一个已有类的基础上建立一个新类，已有的类称基类或父类，新建立的类称为派生类和子类；派生和继承是一个概念，角度不同而已，继承是儿子继承父亲的产业，派生是父亲把产业传承给儿子。

- 一个基类可以派生出多个派生类，一个派生类可以继承多个基类

```C++
//继承方式为可选项，默认为private，还有public,protected
class 派生类名：[继承方式]基类名
{
	派生类新增加的成员声明;
};
```

- 继承方式

![image-20210702112233235](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210702112233235.png)

- 利用using关键字可以改变基类成员再派生类中的访问权限；using只能修改基类中public和protected成员的访问权限。

```C++
class Base
{
public:
	void show();
protected:
	int aa;
	double dd;
};
void Base::show(){
}
class Person:public Base
{
public:
	using Base::aa;//将基类的protected成员变成public
	using Base::dd;//将基类的protected成员变成public
private:
	using Base::show;//将基类的public成员变成private
	string name;
};
int main()
{
	Person *p = new Person();
	p->aa = 12;
	p->dd = 12.3;
	p->show();//出错,private函数
	delete p;
	return 0;
}
```

- 派生类的构造函数和析构函数

  ==执行顺序==：  1.  先执行基类的构造函数，随后执行派生类的构造函数；

  ​					  2.  先执行派生类的析构函数，再执行基类的析构函数。

- 派生类的构造函数：`派生类名(总参数列表)：基类名(基类参数列表),子对象名1(参数列表){构造函数体;}`

```C++
class Base
{
public:
	Base(int, double);
	~Base();
private:
	int aa;
	double dd;
};
Base::Base(int a, double d) :aa(a), dd(d)
{
	cout << "Base Class 构造函数!!!" << endl;
}
Base::~Base()
{
	cout << "Base Class 析构函数!!!" << endl;
}

class Person:public Base
{
public:
	Person(int,double,string);
	~Person();
private:
	string name;
};
Person::Person(int a,double d,string str):Base(a,d),name(str)//注意参数列表
{
	cout << "Person Class 构造函数!!!" << endl;
}
Person::~Person()
{
	cout << "Person Class 析构函数!!!" << endl;
}
int main()
{
	cout << "创建Person对象..." << endl;
	Person *p = new Person(1,2,"yar");
	cout << "删除Person对象...." << endl;
	delete p;
	system("pause");
	return 0;
}
```

![输出结果](https://img-blog.csdnimg.cn/20200228152406940.PNG)

#### **多继承**

一个派生类**同时继承多个基类**的行为。

```
class 派生类名:继承方式1 基类1,继承方式2 基类2
{
	派生类主体;
};
```

二义性问题：多个基类中有同名成员，出现访问不唯一的问题。

#### **虚基类**

c++引入虚基类使得派生类在继承间接共同基类时只保留一份同名成员。
虚基类的声明：`class 派生类名:virtual 继承方式 基类名`

- 虚继承的目的是让某个类做出声明，**承诺愿意共享它的基类**。其中，这个被共享的基类就称为虚基类（Virtual Base Class）。
- 派生类的 同名成员 比虚基类的 优先级更高

```c++
class  A//虚基类
{
protected:
	int a;
};
class B: virtual public A
{
protected:
	int b;
};
class C:virtual public A
{
protected:
	int c;
};
class D:public B,public C
{
protected:
	int d;
	void show()
	{
		b = 123;
		c = 23;
		a = 1;
	}
};
```

- 如果 B 或 C 其中的一个类定义了a，也不会有二义性，派生类的a 比虚基类的a 优先级更高。
- 如果 B 和 C 中都定义了 a，那么D直接访问a 将产生二义性问题。

### 20. 多态与虚函数

#### **向上转型**

- 只能将将派生类赋值给基类（C++中称为向上转型）： 派生类对象赋值给基类对象、将派生类指针赋值给基类指针、将派生类引用赋值给基类引用
- 派生类对象赋值给基类对象，舍弃派生类新增的成员；派生类指针赋值给基类指针，没有拷贝对象的成员，也没有修改对象本身的数据，仅仅是改变了指针的指向；派生类引用赋值给基类引用，和指针的一样。

​	**上转型后通过基类的对象、指针、引用只能访问从基类继承过去的成员（包括成员变量和成员函数），不能访问派生类新增的成员**

#### ==**多态**==

==**不同的对象**可以使用**同一个函数名**调用**不同内容的函数**。==

- 静态多态性-在程序**编译时**系统就决定调用哪个函数，比如**函数重载**；
- 动态多态性-在程序**运行过程中**动态确定调用那个函数，通过**虚函数**实现的。

#### ==**虚函数**==

使用基类对象指针访问派生类对象的同名函数。
- 将基类中的函数声明为虚函数，派生类中的同名函数自动为虚函数。
- 声明形式：`virtual 函数类型 函数名 (参数列表);`
- 构造函数不能声明为虚函数，析构函数可以声明为虚函数。

```C++
class  A
{
public:
	virtual void show()
	{
		cout << "A show" << endl;
	}
};
class B:  public A
{
public:
	void show()
	{
		cout << "B show" << endl;
	}
};
int main()
{
	
	B b;
	b.show();//B show
	A *pA = &b;
	pA->show();//B show 如果show方法前没用virtual声明为虚函数，这里会输出A show
	
	system("pause");
	return 0;
}
```

#### ==**纯虚函数**==

​	纯虚函数是在基类中声明的虚函数，它在基类中没有定义，但要求任**何派生类都要定义自己的实现方法**。在基类中实现纯虚函数的方法是在**函数原型后加“=0” 。**
​	包含纯虚函数的类叫做**抽象类**（也叫接口类），由于**纯虚函数不能被调用**，所以不能利用抽象类创建对象，又称抽象基类。纯虚函数在派生类中重新定义以后，派生类才能实例化出对象。

~~~c++
class  A
{
public:
	virtual void show() = 0;
};
class B:  public A
{
public:
	void show()
	{
		cout << "B show" << endl;
	}
};
~~~

### 21. 运算符重载


​	同一个运算符可以有不同的功能。运算符重载是通过函数实现的，它本质上是函数重载。

重载运算符遵循的规则：

		1. 不可以自己定义新的运算符，只能对已有的C++运算符重载。
		2. 不能改变运算符运算对象的个数。
		3. 不能改变运算符的优先级和结合性
		4. 应与标准类型运算功能相似，避免影响可读性。

**==可重载运算符：==**

![image-20210702202032989](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210702202032989.png)

**==不可重载运算符==**

![image-20210702202138033](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210702202138033.png)

#### **一般格式**

```C++
函数类型 operator运算符(参数列表)
{
	函数体
}
//举个栗子：定义一个向量类，通过运算符重载，可以用+进行运算。
class Vector3
{
public:
	Vector3();
	Vector3(double x,double y,double z);
public:
	Vector3 operator+(const Vector3 &A)const;
	void display()const;
private:
	double m_x;
	double m_y;
	double m_z;
};
Vector3::Vector3() :m_x(0.0), m_y(0.0), m_z(0.0) {}
Vector3::Vector3(double x, double y,double z) : m_x(x), m_y(y), m_z(z) {}
//运算符重载
Vector3 Vector3::operator+(const Vector3 &A) const
{
	Vector3 B;
	B.m_x = this->m_x + A.m_x;
	B.m_y = this->m_y + A.m_y;
	B.m_z = this->m_z + A.m_z;
	return B;
}
void  Vector3::display()const
{
	cout<<"(" << m_x << "," << m_y << "," << m_z << ")" << endl;
}
```

#### **形式**

运算符重载的形式有两种：重载函数作为**类的成员**；重载函数作为**类的友元函数**。

- **双目运算符**作为友元函数时需要制定两个参数。
- 运算符重载函数作为类成员函数可以显式调用。

```C++
class Vector3
{
public:
	Vector3();
	Vector3(double x,double y,double z);
public:
	Vector3 operator+(const Vector3 &A)const;
	Vector3 operator++();
	friend Vector3 operator-(const Vector3 &v1, const Vector3 &v2);
	friend Vector3 operator--(Vector3 &v);
	void display()const;
private:
	double m_x;
	double m_y;
	double m_z;
};
Vector3::Vector3() :m_x(0.0), m_y(0.0), m_z(0.0) {}
Vector3::Vector3(double x, double y,double z) : m_x(x), m_y(y), m_z(z) {}
//运算符重载
Vector3 Vector3::operator+(const Vector3 &A) const
{
	Vector3 B;
	B.m_x = this->m_x + A.m_x;
	B.m_y = this->m_y + A.m_y;
	B.m_z = this->m_z + A.m_z;
	return B;
}
Vector3 Vector3::operator++()
{
	this->m_x ++;
	this->m_y ++;
	this->m_z ++;
	return *this;
}
void  Vector3::display()const
{
	cout<<"(" << m_x << "," << m_y << "," << m_z << ")" << endl;
}
Vector3 operator-(const Vector3 &v1,const Vector3 &v2)
{
	Vector3 B(v1.m_x - v2.m_x, v1.m_y - v2.m_y, v1.m_z - v2.m_z);
	return B;
}
Vector3 operator--( Vector3 &v)
{
	v.m_x--;
	v.m_y--;
	v.m_z --;
	return v;
}
int main()
{
	Vector3 v1(1, 2, 3);
	Vector3 v2(2, 3, 2);
	
	++v1;//v1.operator++(); 作为类成员函数可以显式调用
	v1.display();
	--v2;
	v2.display();
	Vector3 v3 = v1 + v2;// v1.operator+(v2);作为类成员函数可以显式调用
	v3.display();
	Vector3 v4 = v1 - v2;
	v4.display();
	return 0;
}
```

#### **实现类型转换**

- 不指定函数类型和参数，**返回值的类型由类型名来确定**。
- 类型转换函数只能作为成员函数，**不能作为友元函数**。

```C++
operator 类型名()
{
	转换语句;
}
class Vector3
{
public:
	Vector3();
	Vector3(double x,double y,double z);
public:
	Vector3 operator+(const Vector3 &A)const;
	Vector3 operator++();
	friend Vector3 operator-(const Vector3 &v1, const Vector3 &v2);
	friend Vector3 operator--(Vector3 &v,int);
	operator double()
	{
		return m_x + m_y + m_z;
	}
	void display()const;
private:
	double m_x;
	double m_y;
	double m_z;
};
int main()
{
	Vector3 v1(1, 2, 3);
	double d = v1;
	cout << d << endl;//6
	return 0;
}
```

### 22. IO流

#### **流类**

​		流：一连串连续不断的数据集合。
​		输入输出流程：键盘输入=》键盘缓冲区=(回车触发)》程序的输入缓冲区=》‘>>’ 提取数据；
​									输出缓冲区=(缓冲满或endl)》‘<<’  送到 显示器显示。

![输入/输出流类](https://img-blog.csdnimg.cn/20200304113833126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNjcwMTU3,size_16,color_FFFFFF,t_70)

- 上图各类：	
  - istream 是用于输入的流类，cin 就是该类的对象。
  - ostream 是用于输出的流类，cout 就是该类的对象。
  - ifstream 是用于从文件读取数据的类。**从硬盘到内存**
  - ofstream 是用于向文件写入数据的类。**从内存到硬盘**
  - iostream 是既能用于输入，又能用于输出的类。
  - fstream 是既能从文件读取数据，又能向文件写入数据的类。
  - istrstream 输入字符串类
  - ostrstream 输出字符串类
  - strstream 输入输出字符串流类

#### ==**标准输入输出流**==

​	C++的输入/输出流库(iostream)中定义了4个标准流对象：**cin**(标准输入流-键盘)，**cout**(标准输出流-屏幕)，**cerr**(标准错误流-屏幕)，**clog**(标准错误流-屏幕)。

- **cerr 不使用缓冲区**，直接向显示器输出信息；而输出到 **clog 中的信息会先被存放到缓冲区，缓冲区满或者刷新时**才输出到屏幕。
- cout 是 ostream 类的对象，ostream 类的无参构造函数和复制构造函数都是私有的，所以无法定义 ostream 类的对象。
- 使用>>提取数据时，系统会跳过空格，制表符，换行符等空白字符。所以一组变量输入值时，可用这些隔开。
- **输入字符串，也是跳过空白字符**，会在串尾加上字符串结束标志\0。

```C++
int  x;
double y;
cin>>x>>y;//输入 22 66.0  两个数之间可以用空格、制表符和回车分隔数据
char str[10];
cin>>str;//hei ren  字符串中只有hei\0
```

##### **输入流中的成员函数**

- **get函数**：cin.get()，cin.get(ch)（成功返回非0值，否则返回0），cin.get(字符数组(或字符指针)，字符个数n,终止字符)

```C++
char c = cin.get();//获取一个字符
while ((c = cin.get()) != EOF)//循环读取，直到换行
{
	cout << c;
}

char ch;
cin.get(ch);
while (cin.get(ch))//读取成功循环
{
	cout << ch;
}

char arr[5];
cin.get(arr, 5, '\n');//输入 heiren  结果 heir\0
```

- **getline函数**：cin.getline(字符数组(或字符指针),字符个数n,终止标志字符)
  						读取字符直到终止字符或者读取n-1个字符，赋值给指定字符数组（或字符指针）


    					**此函数可读取整行，包括前导和嵌入的空格，并将其存储在字符串对象中。**

```C++
char arr0[30],arr1[30],arr2[40];
cin>>arr0;//遇到空格、制表符或回车结束  "Heiren"
cin.getline(arr1,30);//字符数最多为29个，遇到回车结束 " Hello World"
cin.getline(arr2,40,'*');//最多为39个，遇到*结束 "yar"
//输入 Heiren Hello World
//yar*123

getline(cin, inputLine);// cin 是正在读取的输入流，而 inputLine 是接收输入字符串的 string 变量的名称。
//例子：
#include <iostream>
#include <string> // Header file needed to use string objects
using namespace std;
int main()
{
    string name;
    string city;
    cout << "Please enter your name: ";
    getline(cin, name);
    cout << "Enter the city you live in: ";
    getline(cin, city);
    cout << "Hello, " << name << endl;
    cout << "You live in " << city << endl;
    return 0;
}
```

- **cin.peek()** 不会跳过输入流中的空格、回车符。在输入流已经结束的情况下，cin.peek() 返回 EOF
- **ignore(int n =1, int delim = EOF)**

```C++
int n;
 cin.ignore(5, 'Y');//跳过前5个字符或Y之前的字符，‘Y’优先
 cin >> n;
 //输入1234567  ->  67    1234567Y345->345

//输入2020.2.23
int year,month,day;
cin >> year ;
cin.ignore() >> month ; //用ignore跳过 '.'
 cin.ignore() >> day;
cin.ignore();   //跳过行末 '\n'

 cout<< setfill('0') << setw(2) << month ;//设置填充字符'\0'，输出宽度2
 cout << "-" << setw(2) << day << "-" << setw(4) << year << endl;
```

- **putback(char c)**，可以将一个字符插入输入流的最前面。

##### **输出流对象**

- 插入endl-输出所有数据，插入换行符，**清空缓冲区**
- \n-输出换行，**不清空缓冲区**
- cout.put(参数) 输出单个字符（可以时字符也可以是ASII码）

+ **ostream 类中的成员函数**

  ![image-20210702212804993](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210702212804993.png)

  ```C++
  cout.setf(ios::scientific);
  cout.precision(8);
  cout << 12.23 << endl;//1.22300000e+001
  ```

  ​	setf 和 unsetf 函数用到的flag，与 setiosflags 和 resetiosflags 用到的完全相同

### 23. 文件操作

​		文件-指存储在外部介质上的数据集合，文件按照数据的组织形式不一样，分为两种：ASCII文件(文	本/字符)，二进制文件(内部格式/字节)
​		ASCII文件输出还是二进制文件，数据形式一样，对于数值数据，输出不同

#### **文件类与对象**

C++ 标准类库中有三个类可以用于文件操作，它们统称为文件流类。这三个类是：

- ifstream：输入流类，用于从文件中读取数据。**从硬盘到内存**
- ofstream：输出流类，用于向文件中写入数据。**从内存到硬盘**
- fstream：输入/输出流类，既可用于从文件中读取数据，又可用于 向文件中写入数据。

```C++
#include <fstream>
ifstream in;
ofstream out;
fstream inout;
```

#### **打开文件**

- 打开文件的目的：建立对象与文件的关联，指明文件使用方式
- 打开文件的两种方式：**open函数**和**构造函数**

==**open函数**==：`void open(const char* szFileName, int mode);`

​					第一个参数是**指向文件名的指针**，第二个参数是**文件的打开模式标记**。

![image-20210703133617305](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210703133617305.png)

ios::binary 可以和其他模式标记组合使用，例如：
- ios::in | ios::binary表示用二进制模式，以读取的方式打开文件。
- ios::out | ios::binary表示用二进制模式，以写入的方式打开文件。

==**使用流类的构造函数打开文件**==

​	定义流对象时，在构造函数中给出文件名和打开模式也可以打开文件。

​	以 ifstream 类为例，它有如下构造函数：`ifstream::ifstream (const char* szFileName, int mode = ios::in, int);`

​	第一个参数是指向文件名的指针；第二个参数是打开文件的模式标记，默认值为`ios::in`; 第三个参数是整型的，也有默认值，一般极少使用。

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    ifstream inFile("c:\\tmp\\test.txt", ios::in);
    if (inFile)
        inFile.close();
    else
        cout << "test.txt doesn't exist" << endl;
    ofstream oFile("test1.txt", ios::out);
    if (!oFile)
        cout << "error 1";
    else
        oFile.close();
    fstream oFile2("tmp\\test2.txt", ios::out | ios::in);
    if (!oFile2)
        cout << "error 2";
    else
        oFile.close();
    return 0;
}
```

#### **文本文件的读写**

对于文本文件，可以使用 cin、cout 读写。
eg：编写一个程序，将文件 i.txt 中的整数倒序输出到 o.txt。（12 34 56 78 90 -> 90 78 56 34 12）

```C++
#include <iostream>
#include <fstream>
using namespace std;
int arr[100];
int main()
{

	int num = 0;
	ifstream inFile("i.txt", ios::in);//文本模式打开
	if (!inFile)
		return 0;//打开失败
	ofstream outFile("o.txt",ios::out);
	if (!outFile)
	{
		outFile.close();
		return 0;
	}
	int x;
	while (inFile >> x)
		arr[num++] = x;
	for (int i = num - 1; i >= 0; i--)
		outFile << arr[i] << " ";
	inFile.close();
	outFile.close();
	return 0;
}
```

#### 二进制文件的读写

- 用文本方式存储信息不但浪费空间，而且不便于检索。
- 二进制文件中，信息都占用 sizeof(对象名) 个字节；文本文件中类的成员数据所占用的字节数不同，占用空间一般比二进制的大。

**ostream::write 成员函数**：`ostream & write(char* buffer, int count);`

~~~C++
class Person
{
public:
	char m_name[20];
	int m_age;
};
int main()
{

	Person p;
	ofstream outFile("o.bin", ios::out | ios::binary);
	while (cin >> p.m_name >> p.m_age)
		outFile.write((char*)&p, sizeof(p));//强制类型转换
	outFile.close(); 
	return 0;
}
~~~

**istream::read 成员函数**：`istream & read(char* buffer, int count);`

~~~C++
Person p;
ifstream inFile("o.bin", ios::in | ios::binary); //二进制读方式打开
if (!inFile)
	return 0;//打开文件失败
while (inFile.read((char *)&p, sizeof(p)))
	cout << p.m_name << " " << p.m_age << endl;
inFile.close();
~~~

**文件流类的 put 和 get 成员函数**

~~~C++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
    
    ifstream inFile("a.txt", ios::binary | ios::in); 
    if (!inFile)
        return 0;
    ofstream outFile("b.txt", ios::binary | ios::out);
    if (!outFile) 
    {
        inFile.close();
        return 0;
    }
    char c;
    while (inFile.get(c))  //每读一个字符
        outFile.put(c);  //写一个字符
    outFile.close();
    inFile.close();
    return 0;
}
~~~

​	**一个字节一个字节地读写，不如一次读写一片内存区域快。每次读写的字节数最好是 512 的整	数倍**

#### 移动和获取文件读写指针

- ifstream 类和 fstream 类有 seekg 成员函数，可以设置文件读指针的位置；

- ofstream 类和 fstream 类有 seekp 成员函数，可以设置文件写指针的位置。

- ifstream 类和 fstream 类还有 tellg 成员函数，能够返回文件读指针的位置；

- ofstream 类和 fstream 类还有 tellp 成员函数，能够返回文件写指针的位置。

  ~~~C++
  ostream & seekp (int offset, int mode);
  istream & seekg (int offset, int mode);
  //mode有三种：ios::beg-开头往后offset(>=0)字节 ios::cur-当前往前(<=0)/后(>=0)offset字节 ios::end-末尾往前(<=0)offect字节
  int tellg();
  int tellp();
  //seekg 函数将文件读指针定位到文件尾部，再用 tellg 函数获取文件读指针的位置，此位置即为文件长度
  ~~~

  举个栗子：折半查找文件，name等于“Heiren”

  ~~~C++
  #include <iostream>
  #include <fstream>
  //#include <vector>
  //#include<cstring>
  using namespace std;
  
  class Person
  {
  public:
  	char m_name[20];
  	int m_age;
  };
  int main()
  {
  	Person p;
  	ifstream ioFile("p.bin", ios::in | ios::out);//用既读又写的方式打开
  	if (!ioFile) 
  		return 0;
  	ioFile.seekg(0, ios::end); //定位读指针到文件尾部，以便用以后tellg 获取文件长度
  	int L = 0, R; // L是折半查找范围内第一个记录的序号
  				  // R是折半查找范围内最后一个记录的序号
  	R = ioFile.tellg() / sizeof(Person) - 1;
  	do {
  		int mid = (L + R) / 2; 
  		ioFile.seekg(mid *sizeof(Person), ios::beg); 
  		ioFile.read((char *)&p, sizeof(p));
  		int tmp = strcmp(p.m_name, "Heiren");
  		if (tmp == 0)
  		{ 
  			cout << p.m_name << " " << p.m_age;
  			break;
  		}
  		else if (tmp > 0) 
  			R = mid - 1;
  		else  
  			L = mid + 1;
  	} while (L <= R);
  	ioFile.close();
  
  	system("pause");
  	return 0;
  }
  ~~~

#### 文本文件与二进制文件打开方式的区别

- UNIX/Linux 平台中，用文本方式或二进制方式打开文件没有任何区别。
- 在 UNIX/Linux 平台中，文本文件以\n（ASCII 码为 0x0a）作为换行符号；而在 Windows 平台中，文本文件以连在一起的\r\n（\r的 ASCII 码是 0x0d）作为换行符号。
- 在 Windows 平台中，如果以文本方式打开文件，当读取文件时，系统会将文件中所有的\r\n转换成一个字符\n，如果文件中有连续的两个字节是 0x0d0a，则系统会丢弃前面的 0x0d 这个字节，只读入 0x0a。当写入文件时，系统会将\n转换成\r\n写入。
- **用二进制方式打开文件总是最保险的。**

### 24. 泛型和模版

- 泛型程序设计在**实现时不指定具体要操作的数据的类型**的程序设计方法的一种算法，指的是算法只要实现一遍，就能适用于多种数据类型，优势在于代码复用，减少重复代码的编写。
- 模板是泛型的基础，是创建泛型类或函数的蓝图或公式。
- 泛型是概念, 模板是泛型的实现

#### 函数模版

~~~c++
template<class T>或template<typename T>
函数类型 函数名(参数列表)
{
	函数体;
}
template<class T1,class T2,...>//class可以换成typename
函数类型 函数名(参数列表)
{
	函数体;
}
//举个栗子
template<class T> T max(T a, T b)
{
	return a > b ? a : b;
}
int main()
{
	cout <<"max value is "<< max(12,34) << endl;//34
	cout << "max value is " << max(12.4, 13.6) << endl;//13.6
	cout << "max value is " << max(12.4, 13) << endl;//error 没有与参数列表匹配的 函数模板 "max" 实例参数类型为:(double, int)
	return 0;
}
~~~

#### 类模版

​	声明了类模板，就可以将类型参数用于类的成员函数和成员变量了。换句话说，原来使用 int、float、char 等内置类型的地方，都可以用类型参数来代替。

~~~c++
template<class T>//class可以换成typename 模板头
class 类名
{
	函数定义;
};
//多个类型参数和函数模板类似，逗号隔开
~~~

**当类中的成员函数在类的声明之外定义时，它必须定义为函数模板，带上模板头**，定义形式如下：

~~~c++
template<class T>//class可以换成typename
函数类型 类名<T>::函数名(形参列表)
{
	函数体;
}
~~~

**举例：**

~~~C++
template<typename T1, typename T2>  // 模板头  没有分号
class Point {
public:
	Point(T1 x, T2 y) : x(x), y(y) { }
public:
	T1 getX() const;  //成员函数后加const，声明该函数内部不会改变成员变量的值
	void setX(T1 x);  
	T2 getY() const;  
	void setY(T2 y);  
private:
	T1 x;  
	T2 y;  
};
template<typename T1, typename T2>  //模板头
T1 Point<T1, T2>::getX() const  {
	return x;
}
template<typename T1, typename T2>
void Point<T1, T2>::setX(T1 x) {
	x = x;
}
template<typename T1, typename T2>
T2 Point<T1, T2>::getY() const {
	return y;
}
template<typename T1, typename T2>
void Point<T1, T2>::setY(T2 y) {
	y = y;
}
int main()
{
	Point<int, double> p1(66, 20.5);
	Point<int, char*> p2(10, "东经33度");
	Point<char*, char*> *p3 = new Point<char*, char*>("西经12度", "北纬66度");
	cout << "x=" << p1.getX() << ", y=" << p1.getY() << endl;
	cout << "x=" << p2.getX() << ", y=" << p2.getY() << endl;
	cout << "x=" << p3->getX() << ", y=" << p3->getY() << endl;
	return 0;
}
~~~

#### typename和class的区别

- 模板定义语法中**关键字 class 与 typename 的作用完全一样**。
- 不同的是typename 还有另外一个作用为：使用嵌套依赖类型(nested depended name)

~~~c++
class MyClass
{
public:
		typedef int LengthType;
		LengthType getLength() const
		{
			return this->length;
		}
		void setLength(LengthType length)
		{
			this->length = length;
		}
		
private:
	LengthType length;
};
template<class T>
void MyMethod(T myclass)
{
	//告诉 c++ 编译器，typename 后面的字符串为一个类型名称，而不是成员函数或者成员变量
	typedef typename T::LengthType LengthType; //
	LengthType length = myclass.getLength();
	cout << "length = " <<length<< endl;
	
}
int main()
{
	MyClass my;
	my.setLength(666);
	MyMethod(my);//length = 666
	return 0;
}
~~~

#### 强弱类型语言和C++模版

计算机编程语言可以根据在 **"定义变量时是否要显式地指明数据类型**"可以分为强类型语言和弱类型语言。

- **强类型语言-在定义变量时需要显式地指明数据类型**，为变量指明某种数据类型后就不能赋予其他类型的数据了，除非经过强制类型转换或隐式类型转换。典型的强类型语言有 C/C++、Java、C# 等。

  ~~~c++
  int a = 123;  //不转换
  a = 12.89;  //隐式转换 12（舍去小数部分）
  a = (int)"heiren,HelloWorld";  //强制转换（得到字符串的地址） 不同类型之间转换需要强制
  
  //Java 对类型转换的要求比 C/C++ 更为严格，隐式转换只允许由低向高转，由高向低转必须强制转换。
  int a = 100;  //不转换
  a = (int)12.34;  //强制转换（直接舍去小数部分，得到12）
  ~~~

- **弱类型语言-在定义变量时不需要显式地指明数据类型**，编译器（解释器）会根据赋给变量的数据自动推导出类型，并且可以赋给变量不同类型的数据。典型的弱类型语言有 JavaScript、Python、PHP、Ruby、Shell、Perl 等。

  ~~~C++
  var a = 100;  //赋给整数
  a = 12.34;  //赋给小数
  a = "heiren,HelloWorld";  //赋给字符串
  a = new Array("JavaScript","React","JSON");  //赋给数组
  ~~~

​       **强类型语言在编译期间就能检测某个变量的操作是否正确**，因为变量的类型始终都是确定的，加快了程序的运行；对于弱类型的语言，变量的类型可以随时改变，编译器在编译期间能确定变量的类型，只有等到程序运行后、赋值后才能确定变量当前是什么类型，所以传统的编译对弱类型语言意义不大。

- 解释型语言-弱类型**往往**是解释型语言，边执行边编译
- 编译型语言-先编译后执行。



​	**STL(Standard Template Library，标准模板库)就是c++对数据结构封装后的称呼。**

### 25. STL

​	C++标准模板库（Standard Template Library,STL）是泛型程序设计最成功的实例。STL是一些**常用数据结构和算法的模板的集合**

- ==**C++ 标准模板库的核心包括三大组件：容器Containers，算法Algorithms，迭代器iterators**==

#### 容器

​		STL容器是同质的。
​		顺序容器：可变长动态数组Vector、双端队列deque、双向链表list
​		关联容器：set、multliset、map、multimap

##### ==**vector矢量**==

- vector是向量类型，可以容纳许多类型的数据，因此也被称为容器

- (可以理解为动态数组，是封装好了的类）随着元素的加入，它的内部机制会自动扩充空间以容纳新元素。
          为了降低空间配置时的速度成本，vector实际配置的大小可能比客户端需求大一些，以备将来可能的扩充，这边是容量的概念。换句话说，一个vector的容量永远大于或等于其大小，一旦容量等于大小，便是满载，下次再有新增元素，整个vector容器就得另觅居所。

- 进行`vector`操作前应添加头文件`#include <vector>`


- **初始化**

  ~~~C++
  //定义具有10个整型元素的向量（尖括号为元素类型名，它可以是任何合法的数据类型），不具有初值，其值不确定
  vector<int>a(10);
  
  //定义具有10个整型元素的向量，且给出的每个元素初值为1
  vector<int>a(10,1);
  
  //用向量b给向量a赋值，a的值完全等价于b的值
  vector<int>a(b);
  
  //将向量b中从0-2（共三个）的元素赋值给a，a的类型为int型
  vector<int>a(b.begin(),b.begin+3);
  
   //从数组中获得初值
  int b[7]={1,2,3,4,5,6,7};
  vector<int> a(b,b+7）;
  ~~~

- **vector对象常用内置函数**

  ~~~C++
  #include<vector>
  vector<int> a,b;
  
  a.begin();//返回一个指向容器中第一个元素的迭代器
  
  a.end();//返回一个表示超过容器末尾的迭代器，指向容器最后一个元素后面的那个元素
  
  a.assign(b.begin(),b.begin()+3);//b为向量，将b的0-2个元素赋值给向量a
  
  a.assign(4,2);//a含有4个值为2的元素
  
  a.back();//返回a的最后一个元素
  
  a.front();//返回a的第一个元素
  
  a[i];//返回a的第i元素,当且仅当a存在
  
  a.clear();//清空a中的元素
  
  a.empty();//判断a是否为空，空则返回true，非空则返回false
  
  a.pop_back();//删除a向量的最后一个元素
  
  a.erase(a.begin()+1,a.begin()+3);//删除a中第一个（从第0个算起）到第二个元素，也就是说删除的元素从a.begin()+1算起（包括它）一直a.begin()+3（不包括它）结束[a.begin()+1,a.begin()+3)
  
  a.push_back(5);//在a的最后一个向量后插入一个元素，其值为5
  a.emplace_back(5);//C++11；和push_back功能一样。emplace_back() 和 push_back() 的区别，就在于底层实现的机制不同。push_back() 向容器尾部添加元素时，首先会创建这个元素，然后再将这个元素拷贝或者移动到容器中（如果是拷贝的话，事后会自行销毁先前创建的这个元素）；而 emplace_back() 在实现时，则是直接在容器尾部创建这个元素，省去了拷贝或移动元素的过程。
  
  a.insert(a.begin()+1,5);//在a的第一个元素（从第0个算起）位置插入数值5,
  
  a.insert(a.begin()+1,3,5);//在a的第一个元素（从第0个算起）位置插入3个数，其值都为5
  
  a.insert(a.begin()+1,b+3,b+6);//b为数组，在a的第一个元素（从第0个元素算起）的位置插入b的第三个元素到第5个元素（不包括b+6）
  
  a.size();//返回a中元素的个数
  
  a.capacity();//返回a在内存中总共可以容纳的元素个数
  
  a.resize(10);//将a的现有元素个数调整至10个，多则删，少则补，其值随机
  
  a.resize(10,2);//将a的现有元素个数调整至10个，多则删，少则补，其值为2
  
  a.reserve(100);//将a的容量扩充至100，
  
  a.swap(b);//b为向量，将a中的元素和b中的元素整体交换
  
  a==b;//b为向量，向量的比较操作还有 != >= > <= <
  ~~~


##### **deque双端队列**

​		Vector容器是单向开口的连续内存空间，deque则是一种双向开口的连续线性空间。所谓的双向开口，意思是可以在头尾两端分别做元素的插入和删除操作，当然，vector容器也可以在头尾两端插入元素，但是在其头部操作效率奇差，无法被接受。

![deque原理](https://img-blog.csdnimg.cn/20190817080710196.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMzIyMTAz,size_16,color_FFFFFF,t_70)

​		Deque容器和vector容器最大的差异，一在于deque允许使用常数项时间对头端进行元素的插入和删除操作。二在于deque没有容量的概念，因为它是动态的以**分段连续空间组合而成**，随时可以增加一段新的空间并链接起来，换句话说，像vector那样，”旧空间不足而重新配置一块更大空间，然后复制元素，再释放旧空间”这样的事情在deque身上是不会发生的。也因此，deque没有必须要提供所谓的空间保留(reserve)功能。

​		既然deque是分段连续内存空间，那么就必须有中央控制，维持整体连续的假象，数据结构的设计及迭代器的前进后退操作颇为繁琐。Deque代码的实现远比vector或list都多得多。**Deque采取一块所谓的map(注意，不是STL的map容器)作为主控，这里所谓的map是一小块连续的内存空间，其中每一个元素(此处成为一个结点)都是一个指针，指向另一段连续性内存空间，称作缓冲区。缓冲区才是deque的存储空间的主体。**

![](https://img-blog.csdnimg.cn/20190817080837663.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMzIyMTAz,size_16,color_FFFFFF,t_70)

​		**虽然deque容器也提供了Random Access Iterator,但是它的迭代器并不是普通的指针，其复杂度和vector不是一个量级，这当然影响各个运算的层面。因此，除非有必要，我们应该尽可能的使用vector，而不是deque。**
​		对deque进行的排序操作，为了最高效率，可将deque先完整的复制到一个vector中，对vector容器进行排序，再复制回deque.

~~~C++
//构造函数
deque<T> deqT;//默认构造形式
deque(beg, end);//构造函数将[beg, end)区间中的元素拷贝给本身。
deque(n, elem);//构造函数将n个elem拷贝给本身。
deque(const deque &deq);//拷贝构造函数。

//赋值
assign(beg, end);//将[beg, end)区间中的数据拷贝赋值给本身。
assign(n, elem);//将n个elem拷贝赋值给本身。
deque& operator=(const deque &deq); //重载等号操作符 
swap(deq);// 将deq与本身的元素互换

//大小
deque.size();//返回容器中元素的个数
deque.empty();//判断容器是否为空
deque.resize(num);//重新指定容器的长度为num,若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
deque.resize(num, elem); //重新指定容器的长度为num,若容器变长，则以elem值填充新位置,如果容器变短，则末尾超出容器长度的元素被删除。

//两端插入删除
push_back(elem);//在容器尾部添加一个数据
push_front(elem);//在容器头部插入一个数据
pop_back();//删除容器最后一个数据
pop_front();//删除容器第一个数据

//数据存取
at(idx);//返回索引idx所指的数据，如果idx越界，抛出out_of_range。
operator[];//返回索引idx所指的数据，如果idx越界，不抛出异常，直接出错。
front();//返回第一个数据。
back();//返回最后一个数据

//任意位置、区间  插入和删除
insert(pos,elem);//在pos位置插入一个elem元素的拷贝，返回新数据的位置。
insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。
insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。

clear();//移除容器的所有数据
erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
erase(pos);//删除pos位置的数据，返回下一个数据的位置。
~~~

##### **stack栈**

​	stack是一种先进后出(First In Last Out,FILO)的数据结构，它只有一个出口，只有stack顶端的元素，才有机会被外界取用。**Stack不提供遍历功能，也不提供迭代器。 **     **常用API：**

~~~C++
stack<T> stkT;//stack采用模板类实现， stack对象的默认构造形式： 
stack(const stack &stk);//拷贝构造函数

stack& operator=(const stack &stk);//重载等号操作符

push(elem);//向栈顶添加元素
pop();//从栈顶移除第一个元素
top();//返回栈顶元素

empty();//判断堆栈是否为空
size();//返回堆栈的大小
~~~

##### **queue队列**

​	queue是一种先进先出(First In First Out,FIFO)的数据结构，它有两个出口，queue容器允许从一端新增元素，从另一端移除元素。只有queue的顶端元素，才有机会被外界取用。**Queue不提供遍历功能，也不提供迭代器。**  		 **常用API：**

~~~C++
queue<T> queT;//queue采用模板类实现，queue对象的默认构造形式：
queue(const queue &que);//拷贝构造函数

push(elem);//往队尾添加元素
pop();//从队头移除第一个元素
back();//返回最后一个元素
front();//返回第一个元素

queue& operator=(const queue &que);//重载等号操作符

empty();//判断队列是否为空
size();//返回队列的大小
~~~

##### ==**list双向链表**==

​	链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。
​	list容器不仅是一个双向链表，而且还是一个**循环的双向链表**。
​	每次插入或者删除一个元素，就是配置或者释放一个元素的空间。

~~~C++
list<T> lstT;//list采用采用模板类实现,对象的默认构造形式：
list(beg,end);//构造函数将[beg, end)区间中的元素拷贝给本身。
list(n,elem);//构造函数将n个elem拷贝给本身。
list(const list &lst);//拷贝构造函数。

push_back(elem);//在容器尾部加入一个元素
pop_back();//删除容器中最后一个元素
push_front(elem);//在容器开头插入一个元素
pop_front();//从容器开头移除第一个元素
insert(pos,elem);//在pos位置插elem元素的拷贝，返回新数据的位置。
insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。
insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。
clear();//移除容器的所有数据
erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
erase(pos);//删除pos位置的数据，返回下一个数据的位置。
remove(elem);//删除容器中所有与elem值匹配的元素。

size();//返回容器中元素的个数
empty();//判断容器是否为空
resize(num);//重新指定容器的长度为num，若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。
resize(num, elem);//重新指定容器的长度为num，若容器变长，则以elem值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。

assign(beg, end);//将[beg, end)区间中的数据拷贝赋值给本身。
assign(n, elem);//将n个elem拷贝赋值给本身。
list& operator=(const list &lst);//重载等号操作符
swap(lst);//将lst与本身的元素互换。

front();//返回第一个元素。
back();//返回最后一个元素。

reverse();//反转链表，比如lst包含1,3,5元素，运行此方法后，lst就包含5,3,1元素。
sort(); //list排序
~~~

##### set/multiset

​	所有元素都会根据元素的键值自动被排序。Set不允许两个元素有相同的键值。**不可以通过set的迭代器改变set元素的值**，因为set元素值就是其键值，关系到set元素的排序规则，即set的iterator是一种const_iterator

​	multiset特性及用法和set完全相同，唯一的差别在于它允许键值重复。set和multiset的底层实现是红黑树。

~~~c++
set<T> st;//set默认构造函数：
multiset<T> mst; //multiset默认构造函数: 
set(const set &st);//拷贝构造函数

set& operator=(const set &st);//重载等号操作符
swap(st);//交换两个集合容器

size();//返回容器中元素的数目
empty();//判断容器是否为空

insert(elem);//在容器中插入元素。
clear();//清除所有元素
erase(pos);//删除pos迭代器所指的元素，返回下一个元素的迭代器。
erase(beg, end);//删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
erase(elem);//删除容器中值为elem的元素。

find(key);//查找键key是否存在,若存在，返回该键的元素的迭代器；若不存在，返回set.end();
count(key);//查找键key的元素个数
lower_bound(keyElem);//返回第一个key>=keyElem元素的迭代器。
upper_bound(keyElem);//返回第一个key>keyElem元素的迭代器。
equal_range(keyElem);//返回容器中key与keyElem相等的上下限的两个迭代器。


struct MyCompare02{
	bool operator()(int v1,int v2){
		return v1 > v2;
	}
};

//set从大到小
void test02(){

	srand((unsigned int)time(NULL));
	//我们发现set容器的第二个模板参数可以设置排序规则，默认规则是less<_Kty>
	set<int, MyCompare02> s;
	for (int i = 0; i < 10;i++){
		s.insert(rand() % 100);
	}
	
	for (set<int, MyCompare02>::iterator it = s.begin(); it != s.end(); it ++){
		cout << *it << " ";
	}
	cout << endl;
}
~~~

##### map/multimap

​	Map的特性是，所有元素都会根据元素的键值**自动排序**。
​	Map**所有的元素都是pair**,同时拥有实值和键值，pair的第一元素被视为键值，第二元素被视为实值，**map不允许两个元素有相同的键值**。

​	**不可以通过map的迭代器改变map的键值**

​	Multimap和map的操作类似，**唯一区别multimap键值可重复**。	

~~~C++
map<T1, T2> mapTT;//map默认构造函数: 
map(const map &mp);//拷贝构造函数

map& operator=(const map &mp);//重载等号操作符
swap(mp);//交换两个集合容器

size();//返回容器中元素的数目
empty();//判断容器是否为空

map.insert(...); //往容器插入元素，返回pair<iterator,bool>
map<int, string> mapStu;
// 第一种 通过pair的方式插入对象
mapStu.insert(pair<int, string>(3, "小张"));
// 第二种 通过pair的方式插入对象
mapStu.inset(make_pair(-1, "校长"));
// 第三种 通过value_type的方式插入对象
mapStu.insert(map<int, string>::value_type(1, "小李"));
// 第四种 通过数组的方式插入值
mapStu[3] = "小刘";
mapStu[5] = "小王";

clear();//删除所有元素
erase(pos);//删除pos迭代器所指的元素，返回下一个元素的迭代器。
erase(beg,end);//删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
erase(keyElem);//删除容器中key为keyElem的对组。

find(key);//查找键key是否存在,若存在，返回该键的元素的迭代器；/若不存在，返回map.end();
count(keyElem);//返回容器中key为keyElem的对组个数。对map来说，要么是0，要么是1。对multimap来说，值可能大于1。
lower_bound(keyElem);//返回第一个key>=keyElem元素的迭代器。
upper_bound(keyElem);//返回第一个key>keyElem元素的迭代器。
equal_range(keyElem);//返回容器中key与keyElem相等的上下限的两个迭代器。
~~~

##### STL容器使用时机

![image-20210708162230755](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210708162230755.png)

#### 迭代器

​		**迭代器是一个广义指针。**迭代器使算法独立于使用的容器类型。**模版**提供了存储在容器中的**数据类型**的通用表示（容器中存储的数据结构），**迭代器**提供了遍历容器中的值的通用表示（容器本身的**数据结构**）。
​		**迭代器是一种检查容器内元素并遍历元素的数据类型。**C++更趋向于使用迭代器而不是下标操作，因为标准库为每一种标准容器（如vector）定义了一种迭代器类型，而只用少数容器（如vector）支持下标操作访问容器元素。按照定义方式分为以下四种。
​		1.正向迭代器：`容器类名::iterator 迭代器名;`
​		2.常量正向迭代器：`容器类名::const_iterator 迭代器名;`
​		3.反向迭代器：`容器类名::reverse_iterator 迭代器名;`
​		4.常量反向迭代器：`容器类名::const_reverse_iterator 迭代器名`

~~~C++
vector<double> :: iterator pd;//pd是一个迭代器
vector<double> scores;
pd = scores.begin();
*pd = 22.3;
++pd;
~~~

![image-20210706103435852](C:\Users\93593\AppData\Roaming\Typora\typora-user-images\image-20210706103435852.png)

#### 算法

   STL 提供能**在各种容器中通用的算法**（大约有70种），如插入、删除、查找、排序等。**算法就是函数模板**。算法**通过迭代器来操纵容器中的元素**。
   STL 中的大部分常用算法都在**头文件 algorithm** 中定义。此外，**头文件 numeric** 中也有一些算法。
   许多算法操作的是容器上的一个区间（也可以是整个容器），因此需要两个参数，**一个是区间起点元素的迭代器，另一个是区间终点元素的后面一个元素的迭代器。**

~~~c++
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;
int main()  {
   vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	v.push_back(4); //1,2,3,4
	vector<int>::iterator p;
	p = find(v.begin(), v.end(), 3); //在v中查找3 若找不到,find返回 v.end()
	if (p != v.end())
		cout << "1) " << *p << endl; //找到了
	p = find(v.begin(), v.end(), 9);
	if (p == v.end())
		cout << "not found " << endl; //没找到

	p = find(v.begin() + 1, v.end() - 1, 4); //在2,3 这两个元素中查找4
	cout << "2) " << *p << endl; //没找到，指向下一个元素4

	int arr[10] = { 10,20,30,40 };
	int * pp = find(arr, arr + 4, 20);
	if (pp == arr + 4)
		cout << "not found" << endl;
	else
		cout << "3) " << *pp << endl;
	return 0;

}
~~~

- **STL函数**

  **函数对象适配器**

  ​	函数适配器bind1st 、bind2nd；这两个适配器函数和标准库函数对象类都是定义在functional头文件中的，其中，bind是捆绑的意思，1st和2nd分别是first和second的意思。

  ~~~C++
  bind1st(const Operation& op, const T& x);
  bind2nd(const Operation& op, const T& x);
  ~~~

  **bind1st函数代表这么一个操作:  x op value;    bind2nd函数代表：value op x**   ;value 是被应用bind函数的对象。这两个适配器函数都用于将一个二元算子转换成一个一元算子。

  

  **常用遍历函数**

  ~~~c++
  //遍历算法 遍历容器元素
  for_each(iterator beg, iterator end, _callback);//beg 开始迭代器；end 结束迭代器；_callback函数回调或者函数对象;return 函数对象
  
  //for_each源码：
  template<class _InIt,class _Fn1> inline
  void for_each(_InIt _First, _InIt _Last, _Fn1 _Func)
  {
  	for (; _First != _Last; ++_First)
  		_Func(*_First);
  }
  
  for_each(books.begin(),books.end(),ShowReview);//前两个参数是定义容器中区间的迭代器，最后一个参数是指向函数的指针;   不可修改容器内容
  
  //等价于
  vector<Review> :: iterator pr;
  for(pr = books.begin();pr != books.end();pr++){
      ShowReview(*pr);
  }
  //基于范围的for循环 （C++ 11）；  可修改容器的内容
  for(auto x : books)
      ShowReview(x);
  
  //transform算法 将指定容器区间元素搬运到另一容器中;transform 不会给目标容器分配内存，所以需要我们提前分配好内存
  transform(iterator beg1, iterator end1, iterator beg2, _callbakc);//beg1 源容器开始迭代器;end1 源容器结束迭代器;beg2 目标容器开始迭代器;_cakkback 回调函数或者函数对象;return 返回目标容器迭代器
  //transform源码：
  	template<class _InIt, class _OutIt, class _Fn1> inline 
  	_OutIt _Transform(_InIt _First, _InIt _Last,_OutIt _Dest, _Fn1 _Func)
  	{	
  
  		for (; _First != _Last; ++_First, ++_Dest)
  			*_Dest = _Func(*_First);
  		return (_Dest);
  	}
  
  	template<class _InIt1,class _InIt2,class _OutIt,class _Fn2> inline
  	_OutIt _Transform(_InIt1 _First1, _InIt1 _Last1,_InIt2 _First2, _OutIt _Dest, _Fn2 _Func)
  	{	
  		for (; _First1 != _Last1; ++_First1, ++_First2, ++_Dest)
  			*_Dest = _Func(*_First1, *_First2);
  		return (_Dest);
  	}
  
  ~~~

  **random_shuffle函数**

  ~~~c++
  random_shuffle(books.begin(),books.end());
  ~~~

  **sort函数**

  ~~~C++
  sort(books.begin(),books.end());
  
  sort(books.begin(),books.end(),WorseThan);//最后一个参数指向要是用的函数指针
  ~~~

  

### 26. 命名空间和异常处理

#### 命名空间

 		命名空间实际上是由用户自己命名的一块内存区域，用户可以根据需要指定一个有名字的空间区域，每个命名空间都有一个作用域，将一些全局实体放在该命名空间中，就与其他全局实体分割开来。

~~~c++
namespace [命名空间名]//名省略时，表示无名的命名空间
{
	命名空间成员;
}
~~~

​	命名空间成员的引用：`命名空间名::命名空间成员名`
​	使用命名空间别名：`namespace 别名 = 命名空间名`
​	使用using声明**命名空间成员**的格式：`using 命名空间名::命名空间成员名;`
​	使用using声明**命名空间的全部成员**：`using namespace 命名空间名;`

- using声明后，在using语句所在的作用域中使用该命名空间成员时，不必再用命名空间名加以限定。
- **标准C++库的所有标识符**（包括函数、类、对象和类模板）都是在一个**名为std的命名空间中**定义的。
- 无名的命名空间，只在本文件的作用域内有效。

#### 异常处理

 	**异常**就是程序在执行过程中，由于使用环境变化和用户操作等原因产生的错误，从而影响程序的运行。

- 程序中常见的错误：语法错误，运行错误
- 异常处理机制的组成：检查异常（try）、抛出异常（throw）、捕获并处理异常（catch）

==**异常处理语句：**==

- 被检查的语句必须放在try后面的{}中，否则不起作用，{}不能省略。
- 进行异常处理的语句必须放在catch后面的{}中，catch后()中的异常信息类型不能省略，变量名可以省略。
- catch语句块不能单独使用，必须和try语句块作为整体出现。
- 在try-catch结构中，只能有一个try，但可以有多个catch.
- catch(…)通常放在最后，可以捕获任何类型的异常信息。

~~~C++
try
{
	被检查的语句（可以有多个throw语句）;
}
catch(异常信息类型 [变量名])
{
 
}
~~~

**throw语句：**`thow 变量或表达式;`

​	throw放在try中，也可以单独使用，向上一层函数寻找try-catch，没有找到系统就会调用系统函数terminate，使程序终止运行。

~~~C++
try
{
	throw 123;
}
catch (int a)
{
	cout << a << endl;//123
}
~~~

==**类的异常处理，当在try中定义了类对象，在try中抛出异常前创建的对象将被自动释放。**==

**异常规范**-描述了一个函数允许抛出那些异常类型。

- 异常规范应同时出现在函数声明和函数定义中。

- 如果没有异常规范，可以抛出任何类型的异常。

- 异常规范的一般形式：`函数类型 函数名(参数类型)throw ([异常类型1，异常类型2，...])`

  ~~~C++
  float fun(float float)throw(int,float,double);
  ~~~



### 27. ==杂记==

#### **pair**

​	pair类型定义在    `#include <utility>`   头文件中
​	pair是将2个数据组合成一组数据，如stl中的map就是将key和value放在一起来保存。**当一个函数需要返回2个数据的时候，可以选择pair。**

​	类模板：`template <class T1, class T2> struct pair.`

​	利用**make_pair**创建新的pair对象。

~~~C++
pair<string, int> pair2 = make_pair("name", 30);
cout << pair2.first << endl;
cout << pair2.second << endl;
~~~

~~~C++
pair<T1, T2> p1;            //创建一个空的pair对象（使用默认构造），它的两个元素分别是T1和T2类型，采用值初始化。
pair<T1, T2> p1(v1, v2);    //创建一个pair对象，它的两个元素分别是T1和T2类型，其中first成员初始化为v1，second成员初始化为v2。
make_pair(v1, v2);          // 以v1和v2的值创建一个新的pair对象，其元素类型分别是v1和v2的类型。
p1 < p2;                    // 两个pair对象间的小于运算，其定义遵循字典次序：如 p1.first < p2.first 或者 !(p2.first < p1.first) && (p1.second < p2.second) 则返回true。
p1 == p2；                  // 如果两个对象的first和second依次相等，则这两个对象相等；该运算使用元素的==操作符。
p1.first;                   // 返回对象p1中名为first的公有数据成员
p1.second;                 // 返回对象p1中名为second的公有数据成员

//初始化
pair<string, string> anon;        // 创建一个空对象anon，两个元素类型都是string
pair<string, int> word_count;     // 创建一个空对象 word_count, 两个元素类型分别是string和int类型
pair<string, vector<int> > line;  // 创建一个空对象line，两个元素类型分别是string和vector类型

pair<string, string> author("James","Joy");    // 创建一个author对象，两个元素类型分别为string类型，并默认初始值为James和Joy。
pair<string, int> name_age("Tom", 18);
pair<string, int> name_age2(name_age);    // 拷贝构造初始化
~~~

#### lower_bound()和upper_bound()

[C++ lower_bound 与 upper_bound 函数 - 唐的糖 - 博客园 (cnblogs.com)](https://www.cnblogs.com/Tang-tangt/p/9291018.html)

二分查找的函数有 3 个：**(注意：使用二分查找的前提是数组有序。)**

lower_bound(起始地址，结束地址，要查找的数值) 返回的是数值 **第一个** 出现的位置。		如果所有元素都小于val，则返回last的位置.last的位置是**越界**的

upper_bound(起始地址，结束地址，要查找的数值) 返回的是 **第一个大于待查找数值** 出现的位置。		如果val大于数组中全部元素，返回的是last。(注意：数组下标越界)

binary_search(起始地址，结束地址，要查找的数值)  返回的是是否存在这么一个数，是一个**bool值**。

 lower_bound(val):返回容器中第一个值【大于或等于】val的元素的iterator位置。upper_bound(val): 返回容器中第一个值【大于】val的元素的iterator位置。

 

## Effective C++

### 让自己习惯C++



# STL



