# QT
一些QT笔记，简单案例
# QT / C++笔记

## 基本概念

**头文件与源文件的的区别**

​	头文件用于写类的声明，函数原型，#define等常数等，但一般不写具体实现。

​	源文件主要写头文件中已经声明的哪些函数的具体代码，开头必须 #include一下头文件

## C++中的 this , & , 与 *

​	指针：指针是一种特殊的变量，它存放的是变量的地址值，通过指针可以间接对这个变量操作。指针的类型与它所存地址的变量的类型是相同的。

​	地址：即变量的地址，内存中每个字节都有一个地址值，而变量的地址是它所占有的相应字节的首地址，如：int a；&a指的是int型变量a所占4个字节中的第一个字节的地址。

​	引用：引用也是一种比较特殊的数据类型，一个引用就是一个已存变量的别名，而且在定义引用时必须给它赋初值，如：int a；int & b=a；（定义引用就是在相应的变量名前加“&”）



## QT常用快捷键

 Ctrl + R  编译且运行

 Ctrl + B    编译

F4   .cpp   <------> .h   文件转换

F1     进入帮助实现



## QT核心 —— ==信号与槽==

​	connet(信号发出者地址，发什么信号，在哪个类触发（地址），槽函数)

​	例如

​	connet(ui->btn_open,&QPushbutton::clicked,this,&Serial::btn_open_port);

​	Qdebug = printf() = count <<



## QT使用时遇到的问题

1. 写打开串口触发时，没有设置端口名称
2. 

## QT写串口助手记录（）

1. 初始化

   先要扫描串口     foreach (const QSerialPortInfo &info, QSerialPortInfo::availablePorts())

   设置波特率、起始位、数据位、停止位等参数

2. 打开串口 

   设置串口号
   
   
      serial_port.setPortName(ui->select_serial->currentText());
   
   判断串口是否正常
   
   ​	erial_port.open(QIODevice::ReadWrite) == false
   
3.  按键处理数据

   ​	发送时，一般都是十六进制， 代码是十六进制字符串，要转换，QByteArray send_data_r1 = QByteArray::fromHex(send_data.toLocal8Bit());	

   ​	接收时，收到的是 字节数组，要转成 QString ,截取QString用  QString.mid(0,2) ，起始位置，和截取长高度 

   ​	接收时，需要使用槽函数 connect(&serial_port,&QSerialPort::readyRead,this,&read); 
