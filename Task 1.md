# Task 1


**P 51**

- 2.23：给定指针p，你能知道它是否指向了一个合法的对象吗？如果能，叙述判断的思路；如果不能，也请说明原因。

   > 不能知道它是否指向了一个合法的对象。因为给定一个指针之后，你无法判断这个指针是否已经被初始化，也无法判断这个指针是否指向正确的地址。

- 2.24：在下面这段代码中为什么p合法而lp非法？
  `int i = 42; void *p = &i; long *lp =&i;` 

   > void\*可以于存放任意对象的地址，long\*只可以存放long类型的地址。

**P 53**

- 2.25：说明下列变量的类型和值。

  **(a)** `int* ip, i, &r = i;`

  > ip：int型指针，无效指针；
  > 
  > i：int类型，未赋值；
  > 
  > r：对i的引用。

  **(b)** `int i, *ip = 0;`

  > i：int类型，未赋值；
  > 
  > ip：int型指针，空指针。

  **(c)** `int* ip, ip2;`

  > ip：int型指针，无效指针；
  > 
  > ip2：int类型，未赋值。

**P 62**

- 2.35：判断下列定义推断出的类型是什么，然后编写程序进行验证。

  ```c++
  const int i = 42;
  auto j = i; const auto &k = i; auto *p = &i;
  const auto j2 = i, &k2 = i;
  ```

  >  i:      int
  >  j:      int
  >  k:     int
  >  p:     int const *
  >  j2:    int
  >  k2:   int
  >
  >  **程序：**
  >
  >  ```c++
  >  // Copyright 2019 蒋杨龙 (18062019)
  >  
  >  # include <iostream>
  >  
  >  int main() {
  >      const int i = 42;
  >      auto j = i;
  >      const auto &k = i;
  >      auto *p = &i;
  >      const auto j2 = i, &k2 = i;
  >      std::cout << "i:\t"<< typeid(i).name() << "\n"
  >          << "j:\t" << typeid(j).name() << "\n"
  >          << "k:\t" << typeid(k).name() << "\n"
  >          << "p:\t" << typeid(p).name() << "\n"
  >          << "j2:\t" << typeid(j2).name() << "\n"
  >          << "k2:\t" << typeid(k2).name() << "\n"
  >          << std::endl;
  >      system("pause");
  >      return 0;
  >  }
  >  ```
  >
  >  **结果：**
  >
  >  ![2.35](.\2.35.png)

**P 81**

- 3.4：编写一段程序读入两个字符串，比较其是否相等并输出结果。如果不相等，输出较大的那个字符串和长度较大的那个字符串。改写上述程序，比较输入的两个字符串是否等长，如果不等长，输出长度较大的那个字符串。

  > 第一问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <string>
  > 
  > int main() {
  >     std::string s1, s2;
  >     std::cout << "请输入两个字符串：" << std::endl;
  >     std::cin >> s1 >> s2;
  >     if (s1 == s2)
  >         std::cout << "两个字符串相等。" << std::endl;
  >     else if (s1 > s2)
  >         std::cout << "较大的字符串：" << s1 << std::endl;
  >     else
  >         std::cout << "较大的字符串：" << s2 << std::endl;
  >     return 0;
  > }
  > ```
  >
  > 第二问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <string>
  > 
  > int main() {
  >     std::string s1, s2;
  >     std::cout << "请输入两个字符串：" << std::endl;
  >     std::cin >> s1 >> s2;
  >     if (s1.size() == s2.size())
  >         std::cout << "两个字符串等长。" << std::endl;
  >     else if (s1.size() > s2.size())
  >         std::cout << "较长的字符串：" << s1 << std::endl;
  >     else
  >         std::cout << "较长的字符串：" << s2 << std::endl;
  >     return 0;
  > }
  > ```

- 3.5：编写一段程序从标准输入中读入多个字符串并将它们连接在一起，输出连接成的大字符串。然后修改上述程序，用空格把输入的多个字符串分隔开来。

  > 第一问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <string>
  > 
  > int main() {
  >     std::string s1, s2 {"", ""};
  >     int num;
  >     std::cout << "请输入将输入的字符串个数：" << std::endl;
  >     std::cin >> num;
  >     while (num--) {
  >         std::cin >> s1;
  >         s2 += s1;
  >     }
  >     std::cout << "连接后的字符串：" << s2 << std::endl;
  >     return 0;
  > }
  > ```
  >
  > 第二问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <string>
  > 
  > int main() {
  >     std::string s1, s2 {"", ""};
  >     int num;
  >     std::cout << "请输入将输入的字符串个数：" << std::endl;
  >     std::cin >> num;
  >     while (num--) {
  >         std::cin >> s1;
  >         s2 += s1 + " ";
  >     }
  >     std::cout << "连接后的字符串：" << s2 << std::endl;
  >     return 0;
  > }
  > ```

**P 94**

- 3.20：读入一组整数并把它们存入一个vector对象，将每对相邻整数的和输出出来。改写你的程序，这次要求先输出第1个和最后1个元素的和，接着输出第2个和倒数第2个元素的和，以此类推。

  > 第一问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <vector>
  > 
  > int main() {
  >     std::vector<int> vint;
  >     int i;
  >     std::cout << "输入一组数字，以空格隔开，以非数字字符结束："
  >         << std::endl;
  >     while (std::cin >> i)
  >         vint.push_back(i);
  >     std::cout << "结果：" << std::endl;
  >     for (int i = 0; i < vint.size() - 1; i += 2)
  >         std::cout << vint[i] + vint[i + 1] << ' ';
  >     if (vint.size() % 2 == 1)
  >         std::cout << vint[vint.size() - 1] <<std::endl;
  >     else
  >         std::cout << std::endl;
  >     return 0;
  > }
  > ```
  >
  > 第二问：
  >
  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <vector>
  > 
  > int main() {
  >     std::vector<int> vint;
  >     int i;
  >     std::cout << "输入一组数字，以空格隔开，以非数字字符结束："
  >         << std::endl;
  >     while (std::cin >> i)
  >         vint.push_back(i);
  >     std::cout << "结果：" << std::endl;
  >     for (int i = 0; i < vint.size() / 2; ++i)
  >         std::cout << vint[i] + vint[vint.size() - i - 1] << ' ';
  >     if (vint.size() % 2 == 1)
  >         std::cout << vint[vint.size() / 2] <<std::endl;
  >     else
  >         std::cout << std::endl;
  >     return 0;
  > }
  > ```

**P 99**                

- 3.23：编写一段程序，创建一个含有10个整数的vector对象，然后使用迭代器将所有元素的值都变成原来的两倍。输出vector对象的内容，检验程序是否正确。

  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > # include <vector>
  > 
  > int main() {
  >     std::vector<int> vint(10, 0);
  >     std::cout << "请输入10个整数:" << std::endl;
  >     for (auto it = vint.begin(); it != vint.end(); ++it) {
  >         std::cin >> *it;
  >     }
  >     std::cout << "翻倍后的10个整数:" << std::endl;
  >     for (auto it = vint.begin(); it != vint.end(); ++it) {
  >         *it *= 2;
  >         std::cout << *it << ' ';
  >     }
  >     std::cout << std::endl;
  >     return 0;
  > }
  > ```

**P 188**

- 6.10：编写一个函数，使用指针形参交换两个整数的值。在代码中调用该函数并输出交换后的结果，以此验证函数的正确性。

  > ```c++
  > // Copyright 2019 蒋杨龙 (18062019)
  > 
  > # include <iostream>
  > 
  > void swap(int *q, int *p) {
  >     int t = *q;
  >     *q = *p;
  >     *p = t;
  > }
  > 
  > int main() {
  >     int a, b;
  >     std::cout << "分别输入两个整数a，b:" << std::endl;
  >     std::cin >> a >> b;
  >     swap(&a, &b);
  >     std::cout << "交换后:\n" << "a: " << a
  >         << "\nb: " << b << std::endl;
  >     return 0;
  > }
  > ```

**P 193**

- 6.19：假定有如下声明，判断哪个调用合法、哪个调用不合法。对于不合法的函数调用，说明原因。 

  ```c++
  double calc(double);
  int count (const string &, char);
  int sum(vector<int>::iterator, vector<int>::iterator, int);
  vector<int> vec(10);
  ```

  **(a)** `calc(23.4 , 55.1); `

  > 非法调用：函数声明的形参个数只有一个，但是函数调用中却有2个实参，形参和实参应该要一一对应。

  **(b)** ` count("abcda"，‘a’ );` 

  > 合法调用。

  **(c)** `calc(66); `

  > 合法调用。

  **(d)** `sum(vec.begin() ,vec.end(), 3.8); `

  > 合法调用。

**P 210**

- 6.39：说明在下面的每组声明中第二条声明语句的何含义。如果有非法声明，请指出来。

  **(a)** 

  ```c++
  int calc(int, int);
  int calc(const int, const int);
  ```

  > 声明一个 `int calc(int, int)` 的重载函数，其两个形参类型改变为 `const int` 型。
  >
  > - 非法：一个拥有顶层`const`的形参无法和另一个没有顶层`const`的形参区分开来，即重复声明了`int calc(int, int)`。

  **(b)** 

  ```c++
  int get();
  double get();
  ```

  > 声明一个 `int get()` 的重载函数，仅将其返回类型改变为 `double` 型。
  >
  > - 非法：不允许两个函数除了返回类型以外的其他所有要素相同。

  **(c)** 
  ```c++
  int *reset(int *);
  double *reset(double *);
  ```

  > 声明一个 `int *reset(int *)` 的重载函数，其形参类型改变为 `double *` 型，返回类型改变为 `double *` 型。
  >
  > - 合法。

**P 241**

- 7.16 ：在类的定义中对于访问说明符出现的位置和次数有限定吗？如果有，是什么？什么样的成员应该定义在 `public` 说明符之后？什么样的成员应该定义在 `private` 说明符之后?

  > - 一个类可以包含0个或多个访问说明符，而且对于每个访问说明符能出现在哪里以及能出现多少次都没有限定。
  > - 作为接口的一部分，构造函数和一部分成员函数应该定义在 `public` 说明符之后。
  > - 数据成员和作为实现部分的函数则应该跟在 `private` 说明符之后。

**P 249**

- 7.27：给你自己的Screen 类添加move 、set 和display 函数， 通过执行下面的代码检验你的类是否正确。

  ```c++
  Screen myScreen(5, 5, 'X');
  myScreen.move(4,0).set('#').display(cout);
  cout << "\n";
  myScreen.display(cout);
  cout << "\n";
  ```

  > ```c++
  > // 练习 7.27
  > #include <iostream>
  > #include <string>
  >  
  > using namespace std;
  >  
  > class Screen
  > {
  >  
  > private:
  > 	unsigned height = 0, width = 0;
  > 	unsigned cursor = 0;
  > 	string contents;
  >  
  > public:
  > 	Screen() = default;   //默认构造函数
  > 	//构造函数初始值列表
  > 	Screen(unsigned ht, unsigned wd ) : height(ht), width(wd),
  > 		contents(ht * wd, ' ') { }
  > 	Screen(unsigned ht, unsigned wd, char c) 
  > 		: height(ht), width(wd), contents(ht * wd, c) { }
  >  
  > public:
  > 	Screen & move(unsigned r, unsigned c)
  > 	{
  > 		cursor = r * width + c;
  > 		return *this;
  > 	}
  > 	Screen & set(char ch)
  > 	{
  > 		contents[cursor] = ch;
  > 		return *this;
  > 	}
  > 	Screen & set(unsigned r, unsigned c, char ch)
  > 	{
  > 		contents[r * width + c] = ch;
  > 		return *this;
  > 	}
  > 	Screen & display(ostream & os)
  > 	{
  > 		os << contents;
  > 		return *this;
  > 	}
  >  
  > };
  >  
  > int main()
  > {
  > 	Screen myScreen(5, 5, 'X');
  > 	myScreen.move(4, 0).set('#').display(cout);
  > 	cout << "\n";
  > 	myScreen.display(cout);
  > 	cout << "\n";
  >  
  > 	system("pause");
  > 	return 0;
  > }
  > ```

**P 266**

- 7.49：对于combine 函数的三种不同声明，当我们调用i.combine(s)时分别发生什么情况？其中i 是一个Sales_data，而s 是一个string 对象。

  ```c++
  (a)Sales_data & combine(Sales_data);
  
  (b)Sales_data & combine(Sales_data &);
  
  (c)Sales_data & combine(const Sales_data &) const;
  ```

  > 如果我们试图在一行代码中使用两种转换规则，编译器将报错。
  > (a)是正确的，编译器隐式地调用Sales_data的构造函数，生成一个临时的Sales_data对象，然后传递给combine的形参。
  > (b)是错误的，编译无法通过。因为combine成员函数的形参是非常量引用，但是s自动创建的Sales_data临时对象无法传递给combine所需的非常量引用。（PS：隐式转换生成的无名的临时对象是const的）
  > 修改为：Sales_data &combine( const Sales_data& ) 就可以了。
  > (c)是错误的，编译无法通过。因为我们把combine成员函数声明成了常量成员函数，所以该函数无法修改数据成员的值。

**P 272**

- 7.58：下面的静态数据成员的声明和定义有错误吗？请解释原因。

  ```c++
  
  //example.h
  class Example
  {
  public:
  	static double rate = 6.5;
      //不是字面值常量类型的常量表达式的静态数据成员不允许在类内初始化
  	static const int vetSize = 20;
      //正确，但是在类外应该在定义一下，比如：
      //const int Example::vetSize;
  	static vector<double> vec(vetSize);
      //错误，必须要是常量字面值类型，vector不是字面值类型，不允许类内初始化
  };
  
  //example.C
  #include "example.h"
  //因为上面两个初始化都是错误的，因此下面两个static数据成员必须给出初始值。
  double Example::rate;
  vector<double> Example::vec;
  ```

  
