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
4. 安装完成后更新环境变量
```bash
source ~/.bashrc
```
5. 此时可以在bash中运行,升级conda和安装jupyter notebook命令来测试环境变量是否添加完成。
```bash
conda update conda

conda install jupyter notebook
```
### （三）jupyter notebook的设置
此时在bash命令行输入anaconda-navigator可以启动导航器，我们手动开启jupyter notebook，会默认打开firefox浏览器，但是很大概率会发生"页面载入出错"，这是兼容性的问题，可以通过修改默认浏览器到chrome来解决，也可以通过修改掉不使用"页面重定向"的config文件来解决。   
解决方法生成notebook配置文件，设置为不使用页面重定向。   
1. 生成notebook配置文件
```bash
jupyter notebook --generate-config
```
配置文件路径为：/home/username/.jupyter/jupyter_notebook_config.py 

2. 如果没有在ubuntu中设置显示隐藏文件夹，则可以通过cd命令进入该文件夹，直接使用bash命令打开。
```bash
open jupyter_notebook_config.py
```
在设置文件中加入下面语句
```python
c.NotebookApp.use_redirect_file = False
```
就可以成功。   
3. 完成后建议重启一次anaconda使生效。