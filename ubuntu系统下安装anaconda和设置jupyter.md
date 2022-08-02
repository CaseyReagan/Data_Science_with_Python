# ubuntu系统下安装anaconda和设置jupyter
本文借鉴内容：1.安装anaconda：https://blog.csdn.net/thy0000/article/details/122878599; http://t.zoukankan.com/stacso-p-13757453.html
2.jupyter notebook的部分：https://www.zhihu.com/question/278249210/answer/2460702301

### （一）背景
离网任务需要搭建一个linux环境下的anaconda的jupyter notebook环境来做一个测试，用来测试多线程脚本在该环境下能否正常运行。
搭建VirtualBox虚拟机系统见上一篇"搭建Vbox环境下ubuntu系统"。
### （二）anaconda的安装
1. 可以直接在ubuntu系统的浏览器中查找anaconda官网，会直接提供一个linux版本的下载链接，下载后会得到一个叫做"Anaconda3-2022.05-Linux-x86_64.sh"的文件。
2. 可以另建一个文件夹来存放这个.sh文件，用bash命令进入存放的文件夹，然后用bash命令运行这个脚本。
```bash
bash Anaconda3-2022.05-Linux-x86_64.sh
```
3. 之后不断的按enter和输入yes，就可以一路执行安装过程，安装完成后，会在默认的Home/reagan目录下创建一个/anaconda3/文件夹来存放安装的好的软件。
