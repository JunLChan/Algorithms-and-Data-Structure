```c++
#include <iostream>
#include <cstring>

using namespace std;

class MyString {
public:
    //构造函数
    MyString(const char *str = nullptr);

    //拷贝构造函数
    MyString(const MyString &myString);

    //拷贝赋值函数
    MyString& operator=(const MyString &myString);

private:
    char *m_data;
    int m_size;

};

//构造函数
MyString::MyString(const char *str) {
    if(str == nullptr)	//如果str为空，则分配一个字节存放'\0';
    {
        m_data = new char[1];	//分配一个字节；
        m_data[0] = '\0';	//存放'\0'；
        strcpy(m_data, str);
    }
    else
    {
        m_size = strlen(str);	
        m_data = new char[m_size + 1]; //strlen()所得字符串长度不包括尾部'\0'，所以分配新空间时应加1；	
        strcpy(m_data, str);
    }
}

//拷贝构造函数
MyString::MyString(const MyString &myString) {
    m_size = myString.m_size;
    m_data = new char[m_size + 1];	//strlen()所得字符串长度不包括尾部'\0'，所以分配新空间时应加1；	
    strcpy(m_data, myString.m_data);
}

//拷贝赋值函数
MyString& MyString::operator=(const MyString &myString) {
    if(this == &myString)       //判断是否进行自我赋值；
    {
        return *this;
    }

    delete[] m_data;        //释放原有的内存资源；
    m_size = strlen(myString.m_data);
    m_data = new char[m_size + 1];	//strlen()所得字符串长度不包括尾部'\0'，所以分配新空间时应加1；	
    strcpy(m_data, myString.m_data);
    return *this;
}

//析构函数
MyString::~MyString() {
    if(m_data != nullptr)	//如果m_data不为nullptr，释放堆内存；
    {
        delete[] m_data;
        m_data = nullptr;
    }
}
```

