### 数据类型：
    常量：
    
    ​	 直接常量，也叫字面常量：语法：  `int age = 18;`
    ​	 字符常量：
            使用编译指令 `#define` 定义,语法： `#define 常量名 变量名`    注意结尾没有分号，可以放在源文件的任何位置；
            使用 `const` 来定义，语法：`const float PI = 3.1415926` 定义常量时，必须进行初始化。
    变量
        数据类型的变量：字符型cHar、整型iTimes、单精度型faverage，
        全局变量或者全程变量
        局部变量
        静态变量
        寄存器变量
        外部变量
    整型 范围 0~65535 

|类型|无符号数范围|有符号数范围|
|:-|:-:|-:|
|十进制整型|0~65535（0~2的16次方-1） |-32768 ~ +32767（-2的15次方~2的15次方-1）|
|十进制长整型| 0~4294967295<br />（0~2的32次方-1）|-2147483648 ~ +2147483647<br />（-2的31次方~2的31次方-1）|
|八进制整型|0~177777| |
|十六进制整型|0X0~0XFFFF| |


二叉树：
      ⑧
    ↙ ↘ 
  ①       ⑨

        圆圈为节点，每个数值为节点的值，箭头指向的节点为子节点，指向左边的为左孩子，右边的为右孩子，

        排序二叉树特点：左子节点的值小于当前节点的值，右子节点的值大于当前节点的值；
        