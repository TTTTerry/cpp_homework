# Task 3

* 8.4

  ```c++
  #include<iostream>
  #include<string>
  #include<fstream>
  #include<vector>
  using namespace std;
  
  int fileToVector(string fileName,vector<string> &svec){
      ifstream inFile(fileName);
      if (!inFile) {
          return 1;
      }
      string s;
      while (getline(inFile, s)) {
          svec.push_back(s);
      }
      inFile.close();
      if (inFile.eof()) {
          return 4;
      }
      if (inFile.bad()) {
          return 2;
      }
      if (inFile.fail()) {
          return 3;
      }
  }
  int main() {
      vector<string> svec;
      string fileName, s;
      cout << "Enter fileName:" << endl;
      cin >> fileName;
      switch (fileToVector(fileName, svec))
      {
      case 1:
          cout << "error: can not open file: " << fileName << endl;
          return -1;
      case 2:
          cout << "error: system failure." << endl;
          return -1;
      case 3:
          cout << "error: read failure." << endl;
          return -1;
      }
      cout << "向量里面的内容：" << endl;
      for (vector<string>::iterator iter = svec.begin();iter != svec.end();++iter)
          cout << *iter << endl;
      return 0;
  }
  ```

  

* 8.7

  ```c++
  #include <iostream>
  #include <string>
  #include <fstream>
  
  using namespace std;
  
  class Sales_data {
  public:
      Sales_data() {}
      Sales_data(std::string bN, unsigned sold, double reven) :bookNo(bN), units_sold(sold), revenue(reven) {}
      std::string isbn() const { return this->bookNo; }
      Sales_data& combine(const Sales_data &rhs) {
          units_sold += rhs.units_sold;
          revenue += rhs.revenue;
          return *this;
      }
      double avg_price() const {
          if (units_sold) {
              return revenue / units_sold;
          }
          else return 0;
      }
      Sales_data add(const Sales_data &lhs, const Sales_data &rhs) {
          Sales_data sum = lhs;
          sum.combine(rhs);
          return sum;
      }
  public:
      std::string bookNo; //书号
      unsigned units_sold;
      double revenue;
  };
  
  istream &read(istream &is, Sales_data &item) {
      double price = 0;
      is >> item.bookNo >> item.units_sold >> price;
      item.revenue = item.units_sold * price;
      return is;
  }
  
  ostream &print(ostream &os, const Sales_data &item) {
      os << item.isbn() << " " << item.units_sold << " " << item.revenue << " " << item.avg_price()<<"\n";
      return os;
  }
  
  
  int main(int argc, char **argv)
  {
      ifstream input(argv[1]);
      ofstream output(argv[2]);
  
      Sales_data total;
  
      if (read(input, total))
      {
          Sales_data trans;
  
          while (read(input, trans))
          {
              if (total.isbn() == trans.isbn())
              {
                  total.combine(trans);
              }
              else
              {
                  print(output, total);
                  cout << endl;
                  total = trans;
              }
          }
          print(output, total);
          cout << endl;
          return 0;
      }
      else
      {
          cerr << "No data?!" << std::endl;
          return -1;  // indicate failure
      }
  }
  ```

  

* 8.9

  ```c++
  #include<iostream>
  #include<string>
  #include<fstream>
  #include<sstream>
  #include<vector>
  using namespace std;
  
  istream &iofunc(istream &is) {
      string s;
      while (is >> s) {
          cout << s << endl;
      }
      is.clear();
      return is;
  }
  
  int main() {
      string sss;
      cin >> sss;
      istringstream iss(sss);
      iofunc(iss);
      system("pause");
      return 0;
  }
  ```

  

* 12.1

  > b1包含4个元素，b2被销毁

  

* 12.7

  ```c++
  #include<vector>
  #include<iostream>
  #include<string>
  #include<memory>
  
  using namespace std;
  
  shared_ptr<vector<int>> create_vi() {
      return make_shared<vector<int>>();
  }
  
  void push_vi(shared_ptr<vector<int>> p) {
      int i;
      while (cin >> i) {
          p->push_back(i);
      }
  }
  
  void print_vi(shared_ptr<vector<int>> p) {
      for (const auto i : (*p)) {
          cout << i << " ";
      }
      cout << endl;
  }
  
  int main() {
      auto p = create_vi();
      push_vi(p);
      print_vi(p);
      system("pause");
      return 0;
  }
  ```

  

* 12.10

  > 正确

  

* 12.15

  ```c++
  #include<iostream>
  #include<memory>
  #include<string>
  
  using namespace std;
  
  struct destination {
      string des;
      destination(string des_) :des(des_) {}
  };
  
  struct connection{
      string conn;
      connection(string conn_) :conn(conn_) {}
  };
  
  connection connect(destination *des_) {
      cout << "connect to: " << des_->des << endl;
      return connection(des_->des);
  }
  
  void disconnect(connection conn_) {
      cout << "disconnect " << conn_.conn << endl;
  }
  
  void end_connection(connection *p) { disconnect(*p); }
  
  void f(destination &d) {
      connection c = connect(&d);
      shared_ptr<connection> p(&c, [](connection *p) {disconnect(*p);});  //p接管了内置指针&c所指向的对象的所有权
      cout << "connecting now(" << p.use_count() << ")" << endl;
  }
  
  int main() {
      destination des("aa");
      f(des);
  
      system("pause");
      return 0;
  }
  ```

  

* 12.17

  > (a)不合法，ix不是new返回的指针
  >
  > (b)不合法，pi不是new返回的指针
  >
  > (c)合法
  >
  > (d)不合法，&ix不是new返回的指针
  >
  > (e)合法
  >
  > (f)不合法，必须使用new返回的指针进行初始化，赋值和拷贝的操作也不包含get()方法

  

* 12.18

  > release()函数的作用就是放弃对指针指向对象的控制权，但shared_ptr是多对一的关系，其他的智能指针仍然可以删除这个对象，所以这个函数的话对shared_ptr 没意义 。

  

* 12.19

  ```c++
  class StrBlob
  {
  public:
      friend class StrBlobPtr;//声明friend
      StrBlobPtr begin();
      StrBlobPtr end();
      StrBlob();//默认构造函数
      StrBlob(initializer_list<string> il):data(make_shared<vector<string>>(il)){}
      StrBlob(string il):data(make_shared<vector<string>> (il)){}
      typedef vector<string>::size_type size_type;//定义类型别名，方便使用
   
      //定义函数，返回大小
      size_type size() const
      {
          return data->size();
      }
      //判断vector<string>是否为空
      bool empty()
      {
          return data->empty();
      }
      //向vector<string>中加入元素
      void pushback(const string &s)
      {
          data->push_back(s);
      }
      //访问函数，应首先调用check()
      string& front()
      {
          check(0,"front on empty StrBlob");
          return data->front();
      }
      string& back()
      {
          check(0,"back on empty StrBlob");
          return data->back();
      }
      void popback()
      {
          check(0,"pop_back on empty StrBlob");
          data->pop_back();
      }
   
  private:
      shared_ptr<vector<string>> data;//指向vector<string>的智能指针
      void check(size_type i,const string &msg) const//若访问元素的大小大于data的size,输出错误信息
      {
          if (i > data->size())
          {
              throw out_of_range(msg);//抛出该out_of_range异常，表示不在范围之内
          }
      }
  };
   
  class StrBlobPtr
  {
  public:
      StrBlobPtr():curr(0){}//构造函数，将curr设定为0
      StrBlobPtr(StrBlob &a, size_t sz = 0):wptr(a.data),curr(sz){}//构造函数，将StrBlob的智能指针与此类中的weak_ptr绑定
      string& deref() const
      {
          auto p =check(curr,"deference past end");
          return (*p)[curr];
      }
      StrBlobPtr& incr()
      {
          auto p =check(curr,"deference past end");
          ++curr;
          return *this;
      }
  private:
      shared_ptr<vector<string>> check(size_t i,const string& msg) const//检查函数，返回一个vector<string>的智能指针
      {
          auto ret = wptr.lock();//检查对象是否还存在
          if(!ret)
          {
              throw runtime_error("未绑定");
          }
          if (i >= ret->size())
          {
              throw out_of_range(msg);
          }
          return ret;
      }
      weak_ptr<vector<string>> wptr;//定义弱智能指针
      size_t curr;//设立游标，表示下标
   
  };
   
  StrBlobPtr StrBlob::begin()
  {
      return StrBlobPtr(*this);
  }
  StrBlobPtr StrBlob::end()
  {
      return StrBlobPtr(*this, data->size());
  }
  ```

  