# Task 2

* P301

  9.11：对6种创建和初始化`vector`对象的方法，每一种都给出一个实例。解释每个`vector`包含什么值 

  ```c++
  vector<int> v1; //默认初始化，空vector
  
  vector<int> v2 = {1, 2, 3}; //列表初始化，含有3个元素，值分别为1,2,3
  
  vector<int> v3(v2); //拷贝初始化，拷贝v2，含有3个元素，值分别为1,2,3
  
  vector<int> v4(10); //特定构造函数定义的初始化，含有10个元素，元素值初始化
  
  vector<int> v5(10, 5); //特定构造函数定义的初始化，含有10个元素，元素值初始化为5
  
  vector<int> v6(vector<int>::iterator b, vector<int>::iterator e); //特定构造函数定义的初始化，含有e-b个元素，元素值对应迭代器范围的元素值
  ```

  

* P309
  9.20：编写程序，从一个`list<int>`拷贝元素到两个`deque`中。值为偶数的所有元素都拷贝到一个`deque`中，而奇数值元素都拷贝到另一个`deque`中。 

  ```c++
  //Copyright 2019 蒋杨龙（18062019）
  
  #include<iostream>
  #include<list>
  #include<deque>
  
  using std::deque;
  using std::list;
  using std::endl;
  using std::cin;
  using std::cout;
   
  int main()
  {
      list<int> sde{1,2,3,4,5,6};
      deque<int> d1,d2;
      for(const auto &s:sde)
      {
          if(s%2==0)
              d1.push_back(s);
          else
              d2.push_back(s);
      }
  
      cout<<"sde: ";
      for(auto &i2:sde)
          cout<<i2<<" ";
      cout<<endl;
  
      cout<<"d1: ";
      for(auto &i1:d1)
          cout<<i1<<" ";
      cout<<endl;
  
      cout<<"d2: ";
      for(auto &i2:d2)
          cout<<i2<<" ";
      cout<<endl;
  
      return 0;
  }
  ```

  结果：

  > sde: 1 2 3 4 5 6
  > 
  > d1: 2 4 6
  > 
  > d2: 1 3 5

  

* P315

  9.29：假定`vec`包含25个元素，那么`vec.resize(100)`会做什么？如果接下来调用`vec.resize(10)`会做什么？

  ```c++
  vec.resize(100); //会将75个值为0的int添加到vec的末尾
  vec.resize(10);  //从vec末尾删除90个元素。
  ```

  

* P324

  9.43：编写一个函数，接受三个string参数，s，oldVal和newVal。使用迭代器及insert和erase函数将s中所有oldVal替换为newVal。测试你的程序，用他替换通用的简写形式，如，将“tho”替换为“though”，将“thru”替换为“through”。

  ```c++
  // Copyright 2019 蒋杨龙（18062019）
  
  #include <iostream>
  #include <string>
  
  using std::string;
  
  void func(string &s, const string &oldVal, const string &newVal){
      string::size_type pos = 0;
  
      while (pos<s.length()){
          pos = s.find(oldVal, pos);
          if (pos == string::npos) 
              break;
          s.erase(pos, oldVal.length()); //删除原来的字符
          s.insert(pos, newVal);         //添加新的字符
          pos = pos + newVal.length();
      }
  }
  
  int main(){
  
      string s = "a thsvdo tho thru";
      std::cout << "原：" << s << std::endl;
  
      func(s, "tho", "though");
      func(s, "thru", "through");
   
      std::cout << "改："  << s << std::endl;
      return 0;
  }
  
  ```

  结果：

  > 原：a thsvdo tho thru
  > 
  > 改：a thsvdo though through

  

* P331

  9.52：使用stack处理括号化的表达式。当你看到一个左括号，将其记录下来。当你在一个左括号之后看到一个右括号，从stack中pop对象，直至遇到左括号，将左括号也一起弹出栈。然后将一个值（括号内的运算结果）push到栈中，表示一个括号化的（子）表达式已经处理完毕，被其运算结果所替代。 

  ```C++
  // Copyright 蒋杨龙（18062019）
  
  #include <stack>
  #include <string>
  #include <iostream>
  
  using std::stack;
  using std::string;
  using std::cout;
  using std::endl;
  
  int main(){
      string output;
      auto &s = "Q (cd(e00) )h (xc) rt";
      auto seen = 0;
      stack<char> stk;
      
      cout << "原：" << s << endl;
  
      for(auto c : s) {
          stk.push(c);
          if (c == '(') ++seen;   
          if (seen && c == ')') { 
              while (stk.top() != '(') 
                  stk.pop();
              stk.pop();     
              stk.push('#'); 
              --seen; 
          }
      } ''
      for (; !stk.empty(); stk.pop()) 
          output.insert(output.begin(), stk.top());
      cout << "后：" << output << endl; 
  }
  ```

  结果：

  > 原：Q (cd(e00) )h (xc) rt
  > 
  > 后：Q #h # rt

 

* P339

  10.3：用accumulate求一个vecto<int>中的元素之和。

  ```c++
  //copyright 2019 蒋杨龙（18062019）
  
  #include <iostream>
  #include <string>
  #include <vector>
  #include <algorithm>
  #include <numeric>
  
  int main(){
      std::vector<int> v = {1, 2, 3, 4};
      std::cout << std::accumulate(v.cbegin(), v.cend(), 0)
                << std::endl;
      return 0;
  }
  ```

  结果：

  > 10



* P349

  10.15：编写一个lambda，捕获它所在函数的int，并接受一个int参数。lambda应该返回捕获的int和int参数的和。

  ```c++
  //copyright 2019 蒋杨龙（18062019）
  
  #include <iostream>
  
  int main(){   
      int i = 2;
      auto add = [i](int num){return i + num;};
      
      std::cout << "2与1的和：" << add(1) << std::endl;
      return 0;
  }
  ```

  结果：

  > 2与1的和：3

  

* P365

  10.34：使用reverse_iterator逆序打印一个vector。

  ```c++
  // copyright 蒋杨龙（18062019）
  
  #include <iostream>
  #include <vector>
  
  int main()
  {
      std::vector<int> v = {0, 1, 2, 3};
  
      for (auto iter = v.crbegin(); iter != v.crend(); ++iter)
          std::cout << *iter << " ";
      std::cout << std::endl;
  
      return 0;
  }
  ```

  结果：

  > 3 2 1 0

  

* P370

  10.42：使用list代替vector从新实现10.2.3节中去除重复单词的程序。

  ```c++
  // copyright 蒋杨龙（18062019）
  
  #include <iostream>
  #include <string>
  #include <list>
  
  using std::string;
  using std::list;
  
  int main(){
      list<string> words = {"More", "than", "18,000", "people", "on", "the", "Chinese", "mainland", "donated", "organs", "after", "death", "between", "2015", "and", "last", "year", ",", "with", "the", "number", "of", "donors", "more", "than", "doubled", "every", "year", "during", "the", "period", ",", "according", "to", "a", "report", "released", "Saturday", "."};
      words.sort();
      words.unique();
  
      for (const auto& e : words) std::cout << e << " ";
      std::cout << std::endl;
      return 0;
  }
  ```

  结果：

  > , . 18,000 2015 Chinese More Saturday a according after and between death donated donors doubled during every last mainland more number of on organs people period released report than the to with year 

 

- P381      

  11.12：编写程序，读入string和int的序列，将每个string和int存入一个pair中，pair保存在一个vector中。

  ```c++
  // copyright 2019 蒋杨龙（18062019）
  
  #include <iostream>
  #include <vector>
  #include <utility>
  #include <string>
  
  int main()
  {
      std::vector<std::pair<std::string, int>> vec;
      std::vector<int> vint = {1, 2, 3};
      std::vector<std::string> vstr = {"one", "two", "three"};
      for (int i = 0; i < 3; ++i)
          vec.push_back(std::pair<std::string, int>(vstr[i], vint[i]));
  
      for (const auto& p : vec)
          std::cout << p.first << ": " << p.second << std::endl;
  }
  ```

  结果：

  > one: 1
  > two: 2
  > three: 3

  

- P383      

  11.17：假定c是一个string的multiset，v是一个string的vector，解释下面的调用。指出每个调用是否合法：

  ```c++
  copy(v.begin(),v.end(),inserter(c,c.end()));//正确 
  
  copy(v.begin(),v.end(),back_inserter(c)); 
  //错误 back_inserter()需要使用push_back()，multiset没有push_back这个操作，尾插法不适合 
  
  copy(c.begin(),c.end(),inserter(v,v.end()));//正确 
  
  copy(c.begin(),c.end(),back_inserter(v));//正确
  ```

  

- P396      

  11.38：用unordered_map重写单词计数程序和单词转换程序。

  > 使用无序容器不影响操作，只需将map改成unordered_map即可。

   

- P446      

  13.12：在下面的代码片段中会发生几次析构器函数调用？

  ```c++
  bool fcn( const Sales_data *trans, Sales_data accum )
  {
      Sales_data item1( *trans ), item2( accum );
      return item1.isbn() != item2.isbn();
  }
  ```

  > 三次。
  >
  > 函数结束时：
  >
  > 局部变量item1,item2的生命期结束，被销毁，Sales_data的析构函数被调用。
  >
  > 参数accum的生命期结束，被销毁，调用Sales_data的析构函数。



- P452      

  13.18：定义一个Employee类，它包含雇员的姓名和唯一的雇员证号。为这个类定义默认构造函数，以及接受一个表示雇员姓名的string 的构造函数。每个构造函数应该通过递增一个static 数据成员来生成一个唯一的证号。

  ```c++
  #include <iostream>
  #include <string> 
  
  using namespace std;
  
  class Employee{
   public:
      Employee();
   	Employee(string s);
      ~Employee() = default;
      string name;
      int id;
  
   private:
      static int sid;
  };
  
  int Employee::sid = 0;
  
  Employee::Employee() {
  	id = sid++;
  }
  
  Employee::Employee(string s) {
  	name = s;
  	id = sid++;
  }
  ```

  

- P472      

  13.49：为你的StrVec、String和Message类添加一个移动构造函数和一个移动赋值运算符。

  ```C++
  String& String::operator=(String&& rhs) NOEXCEPT
  {
  	if (this != &rhs) {
  		free();
  		elements = rhs.elements;
  		end = rhs.end;
  		rhs.elements = rhs.end = nullptr;
  	}
  	return *this;
  }
  
  String::String(String&& s) NOEXCEPT : elements(s.elements), end(s.end)
  {
  	s.elements = s.end = nullptr;
  }
  ```

  

- P485     

  13.58：编写新版本Foo类，其sorted函数中有打印语句，测试这个类，来验证你对前两题的答案是否正确。

  ```c++
  #include <vector>
  #include <iostream>
  #include <algorithm>
  
  using std::vector;
  using std::sort;
  
  class Foo {
   public:
      Foo sorted()&&;
      Foo sorted() const&;
  
   private:
      vector<int> data;
  };
  
  Foo Foo::sorted() &&
  {
      sort(data.begin(), data.end());
      std::cout << "&&" << std::endl; 
      return *this;
  }
  
  Foo Foo::sorted() const &
  {
      std::cout << "const &" << std::endl; 
      return Foo(*this).sorted(); 
  }
  
  int main()
  {
      Foo().sorted(); 
      Foo f;
      f.sorted(); 
  }
  ```

   

- P493      

  14.3：string和vector都定义了重载的==以比较各自的对象， 假设svec1和svec2是存放string的vector，确定在下面的表达式中分别使用了哪个版本的==？

  ```c++
  (a)"cobble" == "stone"    //应用了C++语言内置版本的==，比较两个指针。
  (b)svec1[0] == svec2[0]   //应用了string版本的重载==。
  (c)svec1 = svec2          //应用了vector版本的重载==。
  (d)svec1[0] == "stone"    //应用了string版本的重载==，字符串字面常量被转换成string。
  ```

  

- P500      

  14.20：为你的Sales_data 类定义加法和复合赋值运算符。

  ```c++
  class Sales_data{
  	friend Sales_data operator+(const Sales_data &lhs, const Sales_data &rhs);
   public:
  	Sales_data& operator+=(const Sales_data &rhs);
  };
  
  Sales_data operator+(const Sales_data &lhs, const Sales_data &rhs) {
  	Sales_data sum = lhs;
  	sum += rhs;
  	return sum;
  }
  
  Sales_data& Sales_data::operator+=(const Sales_data &rhs) {
  	units_sold += rhs.units_sold;
  	revenue += rhs.revenue;
  	return *this;
  }
  
  ```

  

  

- P509      

  14.38：编写一个类令其检查某个给定的string 对象的长度是否与一个阈值相等。使用该对象编写程序， 统计并报告在输入的文件中长度为1的单词有多少个、长度为2的单词有多少个、……、长度为10 的单词又有多少个。

  ```C++
  #include <iostream>
  #include <vector>
  #include <string>
  #include <algorithm>
   
  using namespace std;
   
  class StrLenIs{
   public:
  	StrLenIs(int len) : len(len) { }
  	bool operator()(const string &str) { return str.length() == len; }
   
   private:
  	int len;
  };
   
  void readStr(istream &is, vector<string> &vec) {
  	string word;
  	while (is >> word) {
  		vec.push_back(word);
  	}
  }
  
  int main() {
  	vector<string> vec;
  	readStr(cin, vec);
  	const int minLen = 1;
  	const int maxLen = 10;
  	for (int i = minLen; i <= maxLen; ++i)
  	{
  		StrLenIs slenIs(i);
  		cout << "len: " << i << ", cnt: " << count_if(vec.begin(), vec.end(), slenIs) << endl;
  	}
   	system("pause");
  	return 0;
  }
  ```

  

- P522      

  14.52：在下面的加法表达式中分别选用了哪个operator＋？列出候选函数、可行函数及为每个可行函数的实参执行的类型转换：

  ```c++
  struct LongDouble
  {
  	//用于演示的成员operator+;在通常情况下+是个非成员
  	LongDouble operator+(const SmallInt&);
  	//其他成员与14.9.2节一致
  };
  longDouble operator+(longDouble&, double);
  SmallInt si;
  longDouble ld;
  ld = si + ld;
  ld = ld + si;
  ```

  > 对于ld=si+ld，由于LongDouble不能转换为SmallInt，因此Smallint的成员operator+和friend operator都不可行。
  > 
  > 由于Smallint不能转换为LongDouble，LongDouble的成员operator+和非成员operator+也都不可行。
  >
  > 由于SmallInt可以转换为int， LongDouble了可以转换为float和double，所以内置的operator+(int, float)和operator+(int, double)都可行，会产生二义性。
  >
  > 对于ld=ld+si，类似上一个加法表达式，由于Smallint不能转换为double，LongDouble也不能转换为SmallInt，因此SmallInt的成员operator+和两个非成员operator+都不匹配。
  >
  > LongDouble的成员operator+可行，且为精确匹配。
  > 
  > SmallInt可以转换为int，longDouble可以转换为float和double，因此内置的operator+(float, int)和operator(double, int)都可行。但它们都需要类型转换，因此LongDouble的成员operator+优先匹配。

- P539      

  15.12：有必要将一个成员函数同时声明成override 和final 吗？ 为什么？

  > override：在C+=11新标准中我们可以使用override关键字来说明派生类中的虚函数。这么做的好处是在使得我们的意图更加清晰明确地告诉编译器我们想要覆盖掉已存在的虚函数。如果定义了一个虚函数与基类中的名字相同但是形参列表不同，在不使用override关键字的时候这种函数定义是合法的，在使用了override关键字之后这种行为是非法的，编译器会提示出错。
  >
  > final：如果我们将某个函数定义成final，则不允许后续的派生类来覆盖这个函数，否则会报错。
  >
  > 因此同时将一个成员函数声明成override和final能够使我们的意图更加清晰。

  

- P542      

  15.16：改写你在15. 2.2 节（第533 页）练习中编写的数量受限的折扣策略，令其继承Disc_quote 。

  ```c++
  class Limited_quote : public Disc_quote{
   public:
  	Limited_quote() = default;
  	Limited_quote(const string &book, double price, size_t qty, double disc) : 
  		Disc_quote(book, price, qty, disc) { }
  	double net_price(size_t cnt) const override	{
  		if (cnt <= quantity) {
  			return cnt * (1 - discount) * price;
  		} else {
  			return quantity * (1 - discount) * price + (cnt - quantity) * price;
  		}
  	}
  };
  
  ```

  

- P562      

  15.30：编写你自己的Basket 类，用它计算上一个练习中交易记录的总价格。

  ```c++
  class Basket{
   public:
  	void add_item(const shared_ptr<Quote> &sales) {
  		items.insert(sales);
  	}
  	double total_receipt(std::ostream&) const;
   private:
  	static bool compare(const std::shared_ptr<Quote> &lhs, 
                          const std::shared_ptr<Quote> &rhs) {
  		return lhs->isbn() < rhs->isbn();
  	}
  	std::multiset<std::shared_ptr<Quote>, decltype(compare)*> items{ compare };
  };
  
  double Basket::total_receipt(std::ostream &os) const {
  	double sum = 0.0;
   	for (auto iter = items.cbegin(); iter != items.cend();
           iter = items.upper_bound(*iter)) {
  		sum += print_total(os, **iter, items.count(*iter));
  	}
  	os << "Total Sale: " << sum << endl;
  	return  sum;
  }
  ```
