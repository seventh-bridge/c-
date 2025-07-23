# 类
## 构造函数
    * 默认构造函数：没有参数的构造函数。
    * 参数化构造函数：接收参数以初始化对象。
    * 拷贝构造函数：用一个对象初始化另一个对象。
    * 移动构造函数（C++11）：从临时对象“移动”资源
## 析构函数
    * 析构函数：在对象生命周期结束时调用，用于释放资源。
```cpp
    #include <iostream>

    class Example {
    public:
        // 默认构造函数
        Example() : data_(0) {
            std::cout << "Default constructor called.\n";
        }

        // 参数化构造函数
        Example(int data) : data_(data) {
            std::cout << "Parameterized constructor called with data = " << data_ << ".\n";
        }

        // 拷贝构造函数
        Example(const Example& other) : data_(other.data_) {
            std::cout << "Copy constructor called.\n";
        }

        // 移动构造函数
        Example(Example&& other) noexcept : data_(other.data_) {
            other.data_ = 0;
            std::cout << "Move constructor called.\n";
        }

        // 析构函数
        ~Example() {
            std::cout << "Destructor called for data = " << data_ << ".\n";
        }

    private:
        int data_;
    };

    int main() {
    Example ex1;               // 调用默认构造函数
    Example ex2(42);           // 调用参数化构造函数
    Example ex3 = ex2;         // 调用拷贝构造函数
    Example ex4 = std::move(ex2); // 调用移动构造函数
    return 0;
    }
```
## 拷贝控制
### 拷贝构造函数
    * 定义：用于创建一个新对象，并复制现有对象的成员。
    * 语法：ClassName(const ClassName& other);
### 拷贝赋值运算符
    * 定义：用于将一个已存在对象的值赋给另一个存在的对象。
    * 语法：ClassName& operator=(const ClassName& other);
```cpp
    int main() {
        MyString s1("Hello");
        MyString s2 = s1;        // 调用拷贝构造函数
        MyString s3;
        s3 = s1;                  // 调用拷贝赋值运算符

        s1.print();
        s2.print();
        s3.print();
        return 0;
    }
```
## 禁止在栈中实例化的类
若想阻止在栈上实例化类，而只允许在自由存储区中创建其实例，关键的在于将析构函数声明为私有的。
```cpp
    class solution{
        private:
        ~solution();
    };

    int main(){
        solution mysolution;//compile error
        solution* mysolution=new solution();//no error
        return 0;
    }
```
但这并不能阻止其在堆上实例化，因为在`main`中无法调用析构函数，无法释放内存，所以会导致内存泄漏。对于该问题需要在类中提供销毁实例的静态公有函数。
```cpp
    class solution{
        private:
        ~solution();
        public:
        static void DestroyInstance(solution* pInstance){
            delete pInstance;
        }
    };

    int main(){
        solution* mysolution=new solution();//no error
        solution::DestroyInstance(mysolution);
        return 0;
    }
```
## this指针
在类中，关键字`this`包含当前对象的地址，当在类成员方法中调用其他成员方法时，编译器将隐式地传递`this`指针。注意调用静态方法时，不会隐式地传递`this`指针，因为静态函数不与类实例相关联，而由所有实例共享。
```cpp
    class Human{
        private:
        void Talk(string s){
            this->name=s;
        }
        public:
        void IntroduceSelf(){
            Talk("Boy");//same as Talk(this,"Boy")
        }
    }
```
## 声明友元
可以使用关键字`friend`声明友元类或友元函数，使其可以从外部访问其他类的私有数据成员和方法。
## 共用体
共用体的成员默认时公有的，不能继承，当将`sizeof()`用于共用体时，结果时为共用体最大成员的长度。声明形式如下：
```cpp
    union UnionName{
        Type1 member1;
        ...
        TypeN memberN;
    };
```
## 对类和结构使用聚合初始化
如下的初始化语法被称为聚合初始化语法：`Type objectName = {argument1,...,argumentN};`。
聚合初始化可以用于聚合类型，对于类或结构的聚合类型指：只包含公有和非静态数据成员，不包含私有或受保护的数据成员，不包含虚成员函数，只涉及公有继承，不包含用户定义的构造函数。
```cpp
    class Agg{
        public:
        int num;
        double pi;
    };

    struct agg{
        char hellp[6];
        int imp[3];
        string world;
    };

    int main(){
        int myNums[]={9,5,-1};
        Agg a1{2017,3,14};
        agg a2{{'h','e','l','l','o'},{2011,2014,2017},"world"};
        return 0;
    }
```
注：聚合初始化只能初始化共用体的第一个非静态成员。