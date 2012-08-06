##搭建Android开发环境

JDK的配置
可以到sun官方http://java.sun.com下载，JDK的具体配置过程

JDK下载地址为：http://www.oracle.com/technetwork/java/javase/downloads/jdk-7u2-download-1377129.html 选择相应版本 X86

一、Android SDK的下载及配置 

进入Android 主页http://developer.android.com/index.html，选择SDK页签，找到对应的版本如图： 



变量步骤如下：
我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量：
JAVA_HOME值为： D:\Program Files\Java\jdk1.6.0_18（你安装JDK的目录）
CLASSPATH值为：.;%JAVA_HOME%\lib\tools.jar;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\bin;
Path:  在开始追加 %JAVA_HOME%\bin;
NOTE：前面四步设置环境变量对搭建Android开发环境不是必须的，可以跳过。
安装完成之后，可以在检查JDK是否安装成功。打开cmd窗口，输入java –version 查看JDK的版本信息。出现类似下面的画面表示安装成功了：
Eclipse安装
可以选择Eclipse IDE for Java Developers 或者 Eclipse IDE for Java EE Developers. 后者应该包含前者，同时还包含了一些Web开发的东西。而一般的做Android开发使用前者即可。我选择后者，因为想系统的了解下java.
Android SDK的下载：
http://developer.android.com/sdk/index.html
选择希望安装的SDK及其文档或者其它包，点击Installation Selected、Accept All、Install Accepted，开始下载安装所选包
在用户变量中新建PATH值为：Android SDK中的tools绝对路径（本机为D:\AndroidDevelop\android-sdk-windows\tools）。
我选择下载所有的包，貌似下载很慢。
在用户变量中新建PATH值为：Android SDK中的tools绝对路径（本机为D:\AndroidDevelop\android-sdk-windows\tools）。
“确定”后，重新启动计算机。重启计算机以后，进入cmd命令窗口，检查SDK是不是安装成功。 
运行 android –h 如果有类似以下的输出，表明安装成功：