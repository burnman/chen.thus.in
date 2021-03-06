在Windows上使用Wget
===================

**首先让我们了解下什么是Wget？**

GNU Wget是一个在网络上进行下载的简单而强大的自由软件，其本身也是GNU计划的一部分。它的名字是“World Wide Web”和“Get”的结合，同时也隐含了软件的主要功能。目前它支持通过HTTP、HTTPS，以及FTP这三个最常见的TCP/IP协议协议下载。

**特点**

-   支持递归下载
-   支持断点下载功能
-   恰当的转换页面中的链接
-   生成可在本地浏览的页面镜像
-   支持代理服务器
-   支持多种操作系统，包括类unix操作系统和Windows系统

由于它的这些特点，所以它天生就是用来down网站的神器。下面我们就来说说怎么在Windows上使用它。点击[这里][]下载wget
for windows的最新版，下载完成后，解压出wget.exe文件，把它放到c:\\windows\\sytem32目录下。然后运行(CTRL+R)输入cmd就可以使用wget了。

**Wget的命令格式如下：**

`wget[参数列表][URL]`

**下面就结合具体例子来说明下Wget的用法**

1.  下载整个http或者ftp站点。

`wget http://www.baidu.com`

这个命令可以将百度首页下载下来。使用-x会强制建立服务器上一模一样的目录，如果使用-nd参数，那么服务器上下载的所有内容都会加到本地当前目录。

`wget -r http://www.baidu.com`

这个命令会按照递归的方法，下载服务器上所有的目录和文件，实质就是下载整个网站。这个命令一定要小心使用，因为在下载的时候，被下载网站指向的所有地址同样会被下载，因此，如果这个网站引用了其他网站，那么被引用的网站也会被下载下来！基于这个原因，这个参数不常用。可以用-l number参数来指定下载的层次。例如只下载两层，那么使用-l 2。要是您想制作镜像站点，那么可以使用－m参数，例如：

`wget -m http://www.baidu.com`

这时wget会自动判断合适的参数来制作镜像站点。此时，wget会登录到服务器上，读入robots.txt并按robots.txt的规定来执行。

  [这里]: http://users.ugent.be/~bpuype/wget/