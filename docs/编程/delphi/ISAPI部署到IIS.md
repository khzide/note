## ISAPI 部署到IIS

### 根节点设置允许未指定CGI， ISAPI模块。

![image-20220612094028734](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612094028734.png)

![image-20220612094123231](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612094123231.png)

### 网站右键添加虚拟目录或应用程序，指定ISAPI　DLL所在目录.



![image-20220612100325916](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612100325916.png)



### 应用程序或虚拟目录编辑功能权限为执行。

![image-20220612100637734](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612100637734.png)

### 设置DLL目录权限，具体应设置哪个用户未知，可以设置Everyone,一个用户搞定。

![image-20220612100843967](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612100843967.png)

![image-20220612100910241](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612100910241.png)



### 应用程序池，找到我们网站设置



![image-20220612100117503](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612100117503.png)

因为我们的DLL是32位的，所以设置启动32位应用程序。

![image-20220612094810529](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612094810529.png)

标识也建议改成Local Service或Network Service等。同时设置应用程序目录访问权限。具体设置哪个账号未知。

![image-20220612101143212](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612101143212.png)

双击应用程序池网站名字修改为无托管代码。

![image-20220612095830241](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612095830241.png)





## 扩展知识点：

**站点(site)**

一 个站点包含一个或者多个application和一个或者多个虚拟目录。我们可以通过对site进行不同的绑定以用不同的方式对site进行访问。这里的 “绑定”包含两个方面，一个是绑定的协议，另一个就是绑定信息。绑定协议用于指定通过什么协议去和该site进行通信。IIS7+中，对一个site可以 的协议包括http,https,net.tcp,net.pipe,net.msmq,net.formatname这几种。当然，对于一个网站，最常 用的就是http和https。而绑定信息则定义了通信的基本信息，比如IP地址，通信端口，站点的一些头部信息(header)。正如前面说到的，可以 为一个site添加多种绑定，只需要在IIS中对某个site进行“编辑绑定”操作即可。

**应用程序(application)**

application 是为一个site提供功能的基本单位，例如一个购物站点可以包含两个application：一个负责呈现商品，给消费者去选购，并放入购物车，而另一个 appliation则可以专注于用户的登录以及支付业务。当一个site只有一个application时候，这个application也就是 root application或者default application，代表着这个site本身，在applicationHost中的“<application path="/" >”里面，path="/"就表示该application是该site的根应用程序。　

　application运行在IIS中的 应用程序池中，以app domain隔离。application可以运行在IIS中任意一个应用程序池中，而不一定要运行在这个application所在的site的应用程 序池中，但对于使用托管代码开发的application（例如一个asp.net网站）必须运行在运行在.NET之上的应用程序池。可以在IIS中对应 用程序池进行设置，包括设置.NET版本(或者是非托管环境)，以及设置管道模式等操作。

**虚拟目录(virtual directory)**

一 个虚拟目录就是一个site（实际上是application）上的对一个本地计算机或者远程计算机上一个物理目录路径的一个映射名称。一个 application可以拥有至少一个虚拟目录。在applicationHost中的“<virtualDirectorypath="/" >”里面，path="/"就表示该virtual directory是该application(或者该site)的根虚拟目录。

当 设置一个虚拟路径映射到一个物理路径后，这个物理路径中的目录名称就会变成这个site（或者application）的url的一部分。一个 site(application)可以拥有多个虚拟目录，例如，一个site中的虚拟目录"www.site.com/script"映射到本地计算机 上该站点中script文件夹，而"www.site.com/image"则映射到远程图片服务器上的一个“image”文件夹。IIS7+利用虚拟目 录映射的目录路径目录下的web.config配置文件来管理该虚拟目录及其子目录（可以在applicationHost.config的 sites/virtualDirectoryDefaults节中使用allowSubDirConfig="false"属性来关闭 web.config对子目录的控制。）

而在IIS7或以上（但目前我能接触到的最高版本的IIS就是win7中的 IIS7.5），site,application和virtual directory的概念已经被规范起来，已经不像IIS6那样含糊。在IIS7+中，他们是独立的概念，并且在IIS组织架构上呈现出一种层次关系：一 个site中可以有一个或者多个application，一个application中可以有一个或者多个virtual directory，而一个virtual directory则对应着一个物理路径。一个site默认会至少有一个application，称为根应用程序(root application)或者默认应用程序（default application），而一个application至少有一个vitual director，称为根虚拟目录(root virtual directory)来看一下我的IIS7.5上一个site的结构和这个site在IIS的ApplicationHost.config文件是怎样对 应的。：

 

![img](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2013011215363253707.jpg)

 

　　**注：ApplicationHost.config文件在目录：\%windir%\system\inetsrv\config目录下**

我 的IIS中只有一个ID为13的site，site下有两个application分别为cd和dh。从右边的config中可以看到，其实除了cd和 dh两个application外，site本身也是一个application，也就是root application。同时也可以看到，每个application下有一个 virtual directory,也就是root virtual directory，充当着这个application的根目录，并映射到该application所在的物理路径。当然，每个application可 以有多个virtual directory，这些virtual directory可以对应其他的物理路径（譬如dh application下的image虚拟目录的物理路径可以使网络中另外一台计算机的某个共享目录）

在IIS7+中(**其实IIS6也是一样，但细节有不同，这里有点含糊，还待深入研究**)， 一个site运行在一个application pool中，而一个application pool默认有一个w3wp.exe（工作者进程），site中的application运行在这个w3wp.exe进程中的app domain（应用程序域）中(不同application运行在不同app domain中，以进行隔离),而同一个application的virtual directory运行在相同的app domain下。但site下的application不一定必须跟这个site运行在相同的application pool，application可以指定一个跟这个application的site不同的application pool。

假定两个网站用相同的应用程序，这里应该是可以选择应用程序池的吧？？？

![image-20220612155357175](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\image-20220612155357175.png)



## [IIS ApplicationPoolIdentity](https://www.cnblogs.com/jfzhu/p/4067297.html)

原创地址：http://www.cnblogs.com/jfzhu/p/4067297.html                        



 

从IIS 7.5开始，Application Pool Identity的Built-in Account除了LocalService，LocalSystem，NetWorkService又多了一个ApplicationPoolIdentity。关于Built-in Account参见[《Windows服务使用的登陆帐号》](http://www.cnblogs.com/jfzhu/p/4007472.html)。

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614002844916.png)](https://images0.cnblogs.com/blog/442200/201411/011613547693335.png)

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614128621208.png)](https://images0.cnblogs.com/blog/442200/201411/011614061126870.png)

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614193153103.png)](https://images0.cnblogs.com/blog/442200/201411/011614153155791.png)

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614222848127.png)](https://images0.cnblogs.com/blog/442200/201411/011614205509158.png)

 

ApplicationPoolIdentity是IIS默认选择的Application Pool Identity。在启动应用池时会动态创建和应用池同名的虚拟帐号。说它是“虚拟”的，是因为在用户管理中看不到该用户或用户组，但该帐号又是确实存在的，比如上图中的应用池名字是WCFDemo，在任务管理器中可以看到w3wp.exe进程（即IIS进程）运行在WCFDemo帐号下。

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614296285351.png)](https://images0.cnblogs.com/blog/442200/201411/011614249255655.png)

 

一个ASP.NET web application可能需要对certificates store中的一个certificate的private key有读权限，下面演示如何对application pool identity赋予读权限。

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614363001947.png)](https://images0.cnblogs.com/blog/442200/201411/011614329725264.png)

 

点击Add

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614393157659.png)](https://images0.cnblogs.com/blog/442200/201411/011614370034332.png)

 

添加 `IIS AppPool\AppPoolName帐号，替换AppPoolName为应用池的名称，这里为WCFDemo。`

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614415974529.png)](https://images0.cnblogs.com/blog/442200/201411/011614397843115.png)

[![image](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\011614446591526.png)](https://images0.cnblogs.com/blog/442200/201411/011614422065942.png)

 

**总结：**ApplicationPoolIdentity是从IIS 7.5之后新添加的Built-in account，是IIS创建新application pool时默认选择的运行帐号。该帐号在启动Application Pool是启动一个虚拟帐号，虚拟帐号名与Application Pool同名，在用户管理中找不到虚拟帐号，但在Task Manager中可以看到w3wp.exe运行在该虚拟帐号下。最后如果想给该虚拟帐号赋予权限，需要赋给`IIS AppPool\AppPoolName，取代AppPoolName为Application Pool名称。`



## 为 ISAPI DLL 配置 Windows 7 IIS7

Windows 7 IIS7 需要一些配置才能使 ISAPI DLL 正常工作。与 IIS 5 相比，它并不是那么简单。

### 安装 IIS 7

1. 转到控制面板 | 程序和功能 | 打开或关闭 Windows 功能（需要特权模式）。
2. 检查“Internet 信息服务”并确保“ISAPI 扩展”和“ISAPI 过滤器”也被选中。
3. 单击确定按钮开始安装。

[![1](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\1_thumb[1].png)](http://lh3.ggpht.com/_2bPtCVVRtI0/SsVjXB-ZU7I/AAAAAAAAAH4/mPg9pjB0OPE/s1600-h/1[3].png)

完成 IIS 7 安装后，打开您喜欢的 Web 浏览器并输入 URL http://localhost/以确保 IIS 正常运行。您可能需要检查防火墙设置并在必要时为端口 80 TCP 流量添加例外。

### 为 ISAPI DLL 配置



### 添加虚拟目录

首先，您可能需要添加一个虚拟目录来托管您的 ISAPI DLL：

1. 打开 Internet 信息服务管理器（需要特权模式）
2. 右键单击“默认网站”节点，然后单击弹出菜单的“添加虚拟目录”：

[![2](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2_thumb[1].png)](http://lh3.ggpht.com/_2bPtCVVRtI0/SsVjZY3sQYI/AAAAAAAAAIA/S19Ksk6yhNM/s1600-h/2[3].png)

输入虚拟目录的“别名”和“物理路径”：

[![3](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\3_thumb[3].png)](http://lh6.ggpht.com/_2bPtCVVRtI0/SsVjb4eBLJI/AAAAAAAAAII/LMYXSNMpz0g/s1600-h/3[7].png)

### 为虚拟目录启用 ISAPI

为虚拟目录启用 ISAPI：

1. 选择虚拟目录节点（例如：本例中的“ISAPI”）。 
2. 双击“处理程序映射”图标。 
3. 单击“操作”面板中的“编辑功能权限...”
4. 弹出“编辑功能权限”对话框
5. 勾选“执行”。
6. 单击确定按钮以提交更改。

[![4](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\4_thumb[1].png)](http://lh3.ggpht.com/_2bPtCVVRtI0/SsVje6eqz5I/AAAAAAAAAIQ/OZu4Cb1RP2M/s1600-h/4[3].png)

### 为虚拟目录启用目录浏览

这是可选的，但很方便。要为虚拟目录启用目录浏览：

1. 选择虚拟目录节点（例如：本例中的“ISAPI”）。 
2. 双击“目录浏览”图标。
3. 在“操作”面板中单击“启用”。

[![5](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\5_thumb[1].png)](http://lh4.ggpht.com/_2bPtCVVRtI0/SsVjhvQoGSI/AAAAAAAAAIY/TDCey9z_ZtY/s1600-h/5[3].png)

### 编辑匿名身份验证凭据

1. 选择虚拟目录节点。
2. 双击“身份验证”图标。
3. 点击选择“匿名认证”项。
4. 单击“操作”面板中的“编辑...”。
5. 将弹出一个对话框。
6. 选中“应用程序池标识”并按 OK 按钮提交更改。

[![1](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\1_thumb[1].png)](http://lh6.ggpht.com/_2bPtCVVRtI0/SvDndGhVJRI/AAAAAAAAAMM/EDsrUJ_372I/s1600-h/1[4].png)

### 启用 ISAPI 模块

1. 单击根节点。
2. 双击“ISAPI 和 CGI 限制”图标。
3. 单击“操作”面板中的“编辑功能设置...”。
4. 选中“允许未指定的 ISAPI 模块”选项。此选项允许在 IIS 下执行任何 ISAPI dll。如果不使用此选项，则需要明确指定 ISAPI DLL 列表。

[![6](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\6_thumb[1].png)](http://lh5.ggpht.com/_2bPtCVVRtI0/SsVjj01s08I/AAAAAAAAAIg/0rcu_9ELIiU/s1600-h/6[3].png)

### 虚拟目录的编辑权限

1. 选择虚拟目录节点（例如：本例中的“ISAPI”）。 
2. 右键单击该节点，然后单击弹出菜单的“编辑权限”。
3. 弹出一个属性对话框。
4. 切换到“安全”页面
5. 单击编辑按钮以显示权限对话框。
6. 将“IIS_IUSRS”添加到权限列表中。

[![7](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\7_thumb[1].png)](http://lh3.ggpht.com/_2bPtCVVRtI0/SsVjmuMDn3I/AAAAAAAAAIo/BI9q9Bmqcsw/s1600-h/7[3].png)

### 在 IIS 7 x64 上启用 32 位 ISAPI DLL

仅当您使用 IIS7 x64 并希望在 IIS 上运行 32 位 ISAPI DLL 时才需要这样做。如果您的 ISAPI DLL 和 IIS7 都是 x86 或都是 x64，您可以跳过此步骤。

1. 单击“应用程序池”节点。
2. 单击“DefaultAppPool”项
3. 从“操作”面板中单击“高级设置...”。
4. 弹出“高级设置”对话框
5. 将“启用 32 位应用程序”设置为 True
6. 单击确定按钮以提交更改

[![8](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\8_thumb[1].png)](http://lh4.ggpht.com/_2bPtCVVRtI0/SsVjr54r3vI/AAAAAAAAAIw/bGRyAw4IAgo/s1600-h/8[3].png)

如果您没有为 32 位应用程序启用此选项，则在从 Web 浏览器执行 ISAPI 时可能会遇到以下错误：

> #### HTTP 错误 500.0 - 内部服务器错误
>
> ##### 由于发生内部服务器错误，无法显示该页面。
>
> HTTP 错误 500.0 - 内部服务器错误
> 模块 IsapiModule
> 通知 ExecuteRequestHandler
> 处理程序 ISAPI-dll
> 错误代码 0x800700c1
> 请求的 URL  http://localhost:80/isapi/isapi.dll
> 物理路径 C:\isapi\isapi.dll
> 登录方法匿名
> 登录用户匿名 

您现在可以将您的 ISAPI DLL 部署到虚拟目录中并开始从 Web 浏览器执行该库。

### DataSnap 和 ISAPI DLL

您可以创建 Delphi DataSnap ISAPP DLL 库并部署在 IIS 上。如果您使用了 ISAPI DLL，有时可能会在开发或部署期间遇到编译错误。这是因为调用的 ISAPI DLL 将缓存在应用程序池中。您不允许在缓存 ISAPI DLL 时覆盖它。

为了克服这个问题，您需要执行 Recycle 操作：

1. 单击“应用程序池”节点。
2. 右键单击“DefaultAppPool”项，然后单击“Recycle…”项。

[![捕获](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\Capture_thumb[1].png)](http://lh4.ggpht.com/_2bPtCVVRtI0/Su_NtBKIoRI/AAAAAAAAAL0/_KNEUdMyzKk/s1600-h/Capture[3].png)

在部署阶段鼓励部署为 ISAPI DLL，因为 IIS 将缓存 ISAPI DLL 以考虑性能。

但是，在开发阶段缓存可能不可行，因为需要在通过频繁编译或覆盖覆盖 ISAPI DLL 时执行回收。您可以考虑在开发时将服务器模块编译为 CGI 应用程序。CGI 的每次调用都是一个单独的操作系统进程，不会被 IIS 应用程序池缓存。

### 在 IIS 上安装 CGI

1. 转到控制面板 | 程序和功能 | 打开或关闭 Windows 功能（需要特权模式）。
2. 检查“Internet 信息服务”并确保选中“CGI”。
3. 单击确定按钮开始安装。

[![2](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2_thumb[1].png)](http://lh5.ggpht.com/_2bPtCVVRtI0/Su_NvU6gqlI/AAAAAAAAAL8/PJbS1sELxas/s1600-h/2[4].png)

### 启用 CGI 模块

1. 单击根节点。
2. 双击“ISAPI 和 CGI 限制”图标。
3. 单击“操作”面板中的“编辑功能设置...”。
4. 选中“允许未指定的 CGI 模块”选项。

### [![3](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\3_thumb[1].png)](http://lh6.ggpht.com/_2bPtCVVRtI0/Su_Nxlow9rI/AAAAAAAAAME/QT32v7p5d6I/s1600-h/3[3].png)



### 通过 URL 使用 DataSnap 服务器方法

DataSnap 服务器方法通过 REST 协议使用 JSON 作为数据流。例如，一个简单的 EchoString 服务器方法定义为：

> type
>  {$MethodInfo On}
>  TMyServerMethod = class(TPersistent)
>  public
>   function EchoString(Value: string): string;
>  结尾;
>  {$MethodInfo 关闭}
>
> 执行
>
> 函数 TMyServerMethod.EchoString(Value: string): string;
> 开始
>  结果：=值；
> 结尾;

要通过 URL 访问在 ISAPI DLL 中编译的此方法，URL 类似于

http://localhost/datasnap/MyISAPI.DLL/datasnap/rest/TMyServerMethod/EchoString/Hello

响应文本将是：

> {“结果”：[“你好”]}

同样，CGI URL 是

http://localhost/datasnap/MyCGI.exe/datasnap/rest/TMyServerMethod/EchoString/Hello

 

## 压力测试

压力测试
ab -n 100 -c 10 http://15fp.cn/ws/wsd.dll/datasnap/rest/tsm/echostring/abc
ab -n 100 -c 10 http://15fp.cn/wsd.dll/datasnap/rest/tsm2/time

ab -n 100 -c 10 http://dev.yt2008.cn/wsd.dll/datasnap/rest/tsm2/time
ab -n 50 -c 50 -v 4 http://dev.yt2008.cn/ws/wsd.dll/datasnap/rest/tsm2/tablelist

ab -n 1000 -c 50 -v 4 -A kpl:15fp.cn http://dev.yt2008.cn:9983/datasnap/rest/tsm2/tablelist

经测试在50个连接的情况下，EXE跟DLL性能差不多。



# IIS8中安装和使用URL重写工具(URL Rewrite)的方法

 更新时间：2017年03月16日 23:19:03  作者：十有三  

本文记录了在IIS8下安装和使用URL Rewrite插件的步骤，详细举例说明如何使用URL重写工具实现301重定向的功能



本文记录了在IIS8下安装和使用URL Rewrite插件的步骤，详细举例说明如何使用URL重写工具实现301重定向的功能。

**下载和安装URL Rewrite**

IIS8默认是没有安装URL重写工具的，必须要自己下载安装。

如果IIS上默认有安装Web平台安装程序，我们可以使用平台自动安装URL Rewrite重写工具，打开IIS(Internet 信息服务管理器)，在管理器主页中找到管理项，打开Web平台安装程序，如下图：

![打开Web平台安装程序自动安装URL Rewrite](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153680.jpg)

在Web平台安装程序中选择产品》服务器，在列表中找到URL重写工具，点击添加后点击安装，即可自动安装好！如下图：

![安装URL重写工具插件](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153681.jpg)

我们也可以手动下载URL Rewrite插件，这是官方地址：[URL Rewrite下载](http://www.iis.net/downloads/microsoft/url-rewrite)

这里有两种方式，一种是下载Web平台安装程序的插件包进行在线安装，点击下载页面中的Install this extension按钮下载urlrewrite2.exe安装程序，双击后会自动运行Web平台安装程序安装URL重写工具2.0。

![安装插件](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153682.jpg)

![使用Web平台安装程序安装URL重写工具](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153683.jpg)

另外一种方式是下载离线安装包，下载地址在页面靠近底部的Download URL Rewrite Module 2.0区块。不过要选择对应自己网站服务器的版本，比如笔者的服务器是64位，中文简体，就要选择如图所示的版本：

![选择URL重写工具版本](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153684.jpg)

**这两种方式都没有什么复杂的步骤，基本一直点击下一步直到完成就可以了。**

------

**2015/10/21更新，现在下载链接只有版本的区别，没有语言区别了，语言会根据服务器自动判断：**

![选择URL重写工具插件的系统版本](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153685.jpg)

------

在IIS上使用URL重写工具的具体步骤

URL Rewrite重写工具主要是使用正则或者通配符进行匹配，对于正则和通配符要有一定的了解，可以网上查下相关的资料，这里建议看官方的帮助文档：[URL Rewrite Module Configuration](http://www.iis.net/learn/extensions/url-rewrite-module/url-rewrite-module-configuration-reference) 和 [IIS URL 重写模块](https://technet.microsoft.com/zh-cn/library/ee215194(v=ws.10).aspx)

首先打开IIS下网站的URL重写功能：

![url重写图标](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153786.jpg)

------

我们右键或者右边的操作菜单栏中选择添加规则，我们可以看到默认有提供很多规则模板，这里我们选择一个空白规则作为添加301重定向的重写演示：

![重写的选择规则模板](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153787.jpg)

------

打开编辑入站规则的界面后，**我们输入自己定义的名称，选择匹配URL的方式和使用的规则，规则可以选择正则表达式、通配符和完全匹配，这里使用的是正则作为示例。最后在匹配URL模式输入.\*（正则表达式，表示匹配所有的路径，这里就是文档中的rule patterns）。**

![设置rule patterns](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153788.jpg)

关于这里的规则模式，这里建议看这篇文章：[详解IIS中URL重写工具的匹配URL-规则模式(rule patterns)](https://www.jb51.net/article/108684.htm)

------

接下来添加URL过滤条件，逻辑分组那根据自己的需求选择，比如笔者是打算做全站301跳转，所以这里用任意匹配。点击添加按钮，设置输入为{HTTP_HOST} ，类型为与模式匹配，模式为^www.shiyousan.com$， 由于之前选择了使用正则作为匹配规则，所以这里要注意使用正确匹配规则。这里主要是设置匹配所有带www的二级域名路径，无论是否有带参数或者目录全部都会匹配到，等于二级域名全站匹配进行重定向跳转。

PS:

服务器变量如果没有就放空不设置。{HTTP_HOST}服务器变量类型，表示所请求的主机，是规则条件输入的值。如果选择的类型为与模式匹配，一般常用有QUERY_STRING、HTTP_HOST、SERVER_PORT、SERVER_PORT_SECURE、REQUEST_URI等服务变量，建议看这篇文章：[详解IIS中URL重写工具的规则条件(Rule conditions)](https://www.jb51.net/article/108682.htm)，里面有更加详细的说明。

![设置condition patterns](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153789.jpg)

------

最后一步就是设置操作，操作类型有五个选项：重写、无、重定向、自定义响应、中止请求。笔者选择的是重定向，然后设置重定向URL，这里的URL是：http://shiyousan.com/{R:0} 。表示所有www.shiyousan.com的URL地址(包括有带参数的地址以及多级目录的地址)都要跳转到shiyousan.com这个顶级域名的URL中。最后重定向类型选择永久301就大功告成了！！！

![img](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153790.jpg)

PS:{R:0}是反向引用，表示与匹配url模式.*的正则全部匹配，也就是rule patterns的匹配规则，具体可以看这篇文章：[详解IIS中的URL重写工具下关于操作重定向URL中的{R:N}与{C:N}](https://www.jb51.net/article/108683.htm)，也可以看官方的文档：[Using back-references in rewrite rules](http://www.iis.net/learn/extensions/url-rewrite-module/url-rewrite-module-configuration-reference#Using_back-references_in_rewrite_rules)

![R:0与rule patterns](E:\风暴文档\笔记\康\软件\delphi\ISAPI部署到IIS.assets\2017031623153791.jpg)

# URL 重写模块配置参考Miscrosoft 官方文档

https://docs.microsoft.com/en-us/iis/extensions/url-rewrite-module/url-rewrite-module-configuration-reference