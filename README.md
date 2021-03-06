apk-demo
-
Android 本身支持如下功能：
 * 存储—使用 SQLite(轻量级的关系数据库)进行数据存储
 * 连接性—支持 GSM/EDGE、IDEN、CDMA、EV-DO、UMTS、Bluetooth(包括A2DP 和 AVRCP)、WiFi、LTE 和 WiMAX
 * 消息传递—支持 SMS 和 MMS
 * Web 浏览器—基于开源的 WebKit，并集成 Chrome 的 V8 JavaScript 引擎。
 * 媒体支持
 * 硬件支持—加速度传感器、摄像头、数字式罗盘、接近传感器和全球定位系统(GPS)。
 * 多点触摸—支持多点触摸屏幕。
 
Android操作系统
-
Android 操作系统大致可以在 4 个主要层面上分为以下 5 个部分：
 * Linux 内核—这是 Android 所基于的核心。这一层包括了一个 Android 设备的各种硬件组件的所有低层设备`驱动程序`(显示驱动、摄像头驱动等)。
 * 系统运行库层-这一层通过一些 C/C++库来为 Android 系统提供了主要的特性支持。如 SQLite 库提供了数据库的支持，OpenGL|ES 库提供了 3D 绘图的支持，Webkit 库提供了浏览器内核 的支持等。同样在这一层还有 Android 运行时库，它主要提供了一些核心库，能够允许开发者 使用 Java 语言来编写 Android 应用。另外 Android 运行时库中还包含了 Dalvik 虚拟机， 它使得每一个 Android 应用都能运行在独立的进程当中
 * 应用程序框架—这一层主要提供了构建应用程序时可能用到的各种 API，Android 自带的一些核心 应用就是使用这些 API 完成的。
 * 应用程序—在这个最顶层中，可以找到 Android 设备自带的应用程序(例如电话、联系人、浏览器等)，以及可以从 Android Market 应用程序商店下载和安装的应用
程序。

市场上的 Android 设备
-
Android 操作系统可以支持如下类型的设备：
 * 智能手机
 * 平板电脑
 * 电子阅读器
 * 上网本
 * MP4 播放器
 * 互联网电视
 
四大组件
-
Android 系统四大组件分别是活动(Activity)、服务(Service)、广播接收器(Broadcast Receiver)和内容提供器(Content Provider)。其中活动是所有 Android 应用程序的门面， 凡是在应用中你看得到的东西，都是放在活动中的。而服务就比较低调了，你无法看到它，但它会一直在后台默默地运行，即使用户退出了应用，服务仍然是可以继续运行的。 广播接收器可以允许你的应用接收来自各处的广播消息，比如电话、短信等，当然你的 应用同样也可以向外发出广播消息。内容提供器则为应用程序之间共享数据提供了可能，比如你想要读取系统电话簿中的联系人，就需要通过内容提供器来实现。

第一个项目
-
使用android-studio初始化了第一个项目，我们看一下第一个项目中的文件：
 * src 目录是放置我们所有 Java 代码的地方，它在这里的含义和普通 Java项目下的 src 目录是完全一样的。
 * 如果你的项目中使用到了第三方 Jar 包，就需要把这些 Jar 包都放在 libs 目录下，放在这个目录下的 Jar 包都会被自动添加到构建路径里去。
 * bin个目录你也不需要过多关注，它主要包含了一些在编译时自动产生的文件。展开 bin 目录你会看到 HelloWorld.apk
 * AndroidManifest.xml这是你整个 Android 项目的配置文件，你在程序中定义的所有四大组件都需要在这个文件里注册。< activity>中表示HelloWorldActivity 是这个项目的主活动，在手机上点击应用图标，首先启动的就是这个活动。
 * 因为所有程序都包含在活动中，我们看一下HelloWorldActivity，HelloWorldActivity 是继承自 AppCompatActivity 的。`我们项目中所有的活动都必须要继承它才能拥有活动的特性。`onCreate()方法是一个活动被创建时必定要执行的方法，其中只有两行代码，并且没有Hello world!的字样。
 * 显示的Hello world!是在哪里定义的呢？其实 Android程序的设计讲究逻辑和视图分离，因此是不推荐在活动中直接编写界面的，更加通用的一种做法是，在布局文件中编写界面，然后在活动中引入进来。
 
res目录
-
其实归纳一下，res 目录就变得非常简单了。所有以 drawable 开头的文件夹都是用来放图片的，所有以 values 开头的文件夹都是用来放字符串的， layout 文件夹是用来放布局文件的，menu 文件夹是用来放菜单文件的。

比如刚刚在 strings.xml 中找到的 Hello world!字符串，我们有两种方式可以引用它:
 * 在代码中通过 R.string.hello_world 可以获得该字符串的引用
 * 在 XML 中通过@string/hello_world 可以获得该字符串的引用。
 
HelloWorld 项目的图标就是在 AndroidManifest.xml 中通过 android:icon="@drawable/ic_launcher"来指定的，ic_launcher 这张图片就在 drawable 文件夹下， 如果想要修改项目的图标应该知道怎么办了吧

使用 Android 的日志工具 Log
-
既然 LogCat 已经添加完成，我们来学习一下如何使用 Android 的日志工具吧。Android 中的日志工具类是 Log(android.util.Log)，这个类中提供了如下几个方法来供我们打印日志。

活动是什么
-
活动(Activity)是最容易吸引到用户的地方了，它是一种可以包含用户界面的组件， 主要用于和用户进行交互。一个应用程序中可以包含零个或多个活动。我们可以通过不再勾选 Create Activity 这个选项手动创建活动。


 

 
