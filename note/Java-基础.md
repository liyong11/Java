# **数据**
## 基本数据类型
内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。
数据类型|初始值
---|:---:|---:
* short 16位|0
* int 32位 4字节|0
* long 64位|0L
* float 32位|0.0f
* double 64位|0.0d
* char 16位|'u0000'
* byte 8位|0
* boolean 1位|false

String不是Java的基本数据类型,初始值为'null'.

## 变量
在声明一个变量后,如果使用变量前需要变量初始化,否正Java编译器会报错</br>
`int firstnumber;`</br>
`firstnumber = 0;`
## 数组
概念: 
> 数组是一种数据结构,是用来储存同一类型值得集合.通过整形的数下标可以访问数组中的某一个值.在声明数组时,需要申明类型和变量名字.

定义:`int[] a;` or `int[] a = new int[100];`

For-Each 循环:</br>
该语句能在不使用下标的情况下遍历数组
> `for(int element: array)`</br>
&nbsp;&nbsp;&nbsp;&nbsp;`{
    System.out.println(element);
}`

