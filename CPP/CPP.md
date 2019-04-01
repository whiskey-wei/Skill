# 基础

## 1.const

* ### 定义常量  
    ```
    const int a = 5;
    int const b = 8;
    ```
    以上两种都可以

* ### 常量指针
    常量指针，无法通过指针去修改指向的地址的值指针本身可以指向其它地址
    ```
    int a1 = 7, b1 = 7;
    const int* m = &a1;
    int const* n = &b1;
    //*m = 5 错误
    m = &b1;
    n = &a1;
    ```

* ### 指针常量
    指针常量，指针可以修改指向的地址的值本身无法改变指向
    ```
    int a3 = 5, b3 = 7;
    int* const p = &a3;
    *p = 9;
    //p = &b3 错误
    ```

* ### 常量函数
    修饰成员函数，函数中不能修改类中的数据成员  
    修饰对象，此对象只能调用常量函数

* ### 顶层const与底层const
    const修饰指针的为顶层const，修饰所指对象的为底层const  
    ```
    1.执行对象拷贝时，底层const不能赋值给
    int num = 3;
    const int *p = &num; //p为底层const
    //int *q = p;//错误
    const int *q = p;
    
    2.const_cast只能改变底层const
    int num = 4;
    const int *p = &num;
    //*p = 5 //错误底层const无法改变所指对象的值
    int *q = const_cast<int*>(p); 
    //正确，const_cast可以改变运算对象的底层const。但是使用时一定要知道num不是const的类型。
    q = 5;
    ```
## 2.static
* 修饰函数与全局变量，使函数或变量只在当前文件可见。
* 修饰局部变量，使得局部变量生命周期变长，但是作用域不变。
~~~
int fun(){
    static int count = 10;   
    return count--; 
    /*在第一次进入这个函数的时候，变量a被初始化为10！并接着自减1，以后每  
    次进入该函数，a就不会被再次初始化了，仅进行自减1的操作；在static发明  
    前，要达到同样的功能，则只能使用全局变量*/   
}
 
int count = 1;
 
int main(void)
{
     printf("global\t\tlocal static\n");
     for(; count <= 10; ++count)
               printf("%d\t\t%d\n", count, fun());
     return 0;
}
~~~
* 默认初始化为0
* 修饰类的成员  
  * 类的静态成员函数是属于整个类而非类的对象，所以它没有this指针，这就导致 了它仅能访问类的静态数据和静态成员函数。  
  * 不能将静态成员函数定义为虚函数。 
  * 静态数据成员是静态存储的，所以必须对它进行初始化。

