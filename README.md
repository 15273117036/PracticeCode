# ARM实验：触控板 ——宋伟鹏

## 编译下载程序到实验板

​	工程我己经改好，解压`LT-ARM2.rar`打开工程，编译下载即可

## 编译主机驱动

​	`src.rar`以及`JInfo.rar`中的内容为主机驱动程序，由于开发板给的底层驱动是32位的，因此这部分代码应安装在一装有32位操作系统的电脑，推荐使用WMWare虚拟机，安装一个windows xp 32-bit。

​	安装好虚拟机之后，在虚拟机系统内安装JDK并配置环境变量，最新版本经测试仍可以在XP上完美运行。之后，解压`src.rar`，进入`.\src\src\song20170601`目录内，打开cmd并cd至当前目录，输入`javac Server.java CommunateListener.java CommunateTranser.java Config.java NInfo.java `编译生成class文件，然后cd至上层目录，即`.\src\src`目录，输入`javah -jni song20170601.NInfo`生成对应的JNI头文件(.h)。

​	解压`JInfo.rar`，把刚刚生成的头文件拷贝至解压后的目录，打开工程，添加那个头文件到工程，添加包含文件目录`$(Java_Home)\include`和`$(Java_Home)\include\win32`，其中`$(Java_Home)`为你安装JDK的目录。然后编译工程，生成`JInfo.dll`在`工程目录\Debug`下，拷贝此文件和工程根目录下的`EasyUsb214x.dll`到`$(Java_Home)\bin`中。

​	此时32位系统下的工作完成。

​	以下操作是在你的64位主机上。

​	在主机上（非你的32位虚拟机）解压`srcinnewerWindows.rar`，cd至`.\srcinnewerWindows\src\song20170602`目录，输入`javac Consle.java MouseInfo.java TouchGetter.java TouchOperator.java Config.java `生成对应的class文件。然后cd至上层目录，输入`javah -jni song20170602.MouseInfo`生成对应的JNI头文件(.h)。

​	解压`Mouse.rar`，打开用VS2015或者VS2017打开工程（不要使用更旧的版本，VC6.0更不行）,添加那个头文件到工程，编译配置改为x64，添加包含文件目录`$(Java_Home)\include`和`$(Java_Home)\include\win32`，其中`$(Java_Home)`为你安装JDK的目录。然后编译工程，生成`Mouse.dll`在`工程目录\x64\Debug`下，把它拷贝到`$(Java_Home)\bin`中。

​	至此，配置完成。

## 运行

​	把实验板的USB从接口插到电脑上，并接到虚拟机，cd至`song20170601`文件夹所在的目录，输入`java song20170601.Server`运行服务端。

​	打开一个新的cmd窗口，输入`ipconfig`查看此虚拟机的ip地址。

​	在主机上，cd至`song20170602`所在目录，输入`java song20170602.Consle`运行客户端，然后输入`connect 你虚拟机的ip`连接至服务端。

​	至此，便可使用触摸屏控制鼠标移动，按键控制鼠标按键。

​	其他详情阅读代码。

