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
