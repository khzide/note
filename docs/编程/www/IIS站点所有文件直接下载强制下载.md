# IIS站点所有文件直接下载强制下载.

ISS下载不同后缀名文件会有限制，网上找了一些资料，都很旧了，自己重新整理了下。

配置完成后，访问站点内的所有文件都会被强制下载，提示下载窗口，包含asp，php，txt等所有的文件。

解决思路主要通过修改MIME信息来实现，MIME参考手册：http://www.w3school.com.cn/media/media_mimeref.asp

1.点击你的站点，在右侧找到MIME类型（网上说在网站右键点属性，可能IIS版本更新，并没有属性选项）

![img](设置网站所有文件强制可下载.assets\231914140492088.png)

2.打开MIME类型，并点击右上角添加：以.ini类型为例填写

文件扩展名：.ini    MIME类型：application/octet-stream

确定保存，其他扩展名例如.txt .rar这样就行

![img](设置网站所有文件强制可下载.assets\231919085331154.jpg)

3.配置可下载所有文件类型，添加方式相同，点击添加，因为要下载所有类型，所以扩展名是.*，MIME类型也有所区别application/force-download

文件扩展名：.*    MIME类型：application/force-download 

这样配置IIS就可以允许你下载指定类型的文件或者全部类型了。

![image-20220705205243266](设置网站所有文件强制可下载.assets\image-20220705205243266.png)

