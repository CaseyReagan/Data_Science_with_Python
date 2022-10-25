# FTP的python实用方法
本文借鉴内容：1.远程FTP下载文件到本地目录. https://blog.csdn.net/Hudas/article/details/125148755

## 总结
+ 用浏览器和win的文件资源管理器直接访问。
+ 用shell和命令行访问。
+ python代码获取内容。

### （一）背景
有一个需要从某地址用ftp协议取文件的需求，并且需要取时间为最新的文件。
***
### （二）windows环境下直接访问ftp的两种方法
（1）直接使用浏览器访问，使用IE浏览器，在地址栏输入ftp://127.0.0.1（IP地址修改为FTP服务器的IP地址），会有弹出框提示进行账号和密码的输入，完成后可以直接访问ftp服务器内的文件目录和内容。
（2）使用windows的文件资源管理器访问，在文件资源管理器的地址栏一项，同样输入ftp://127.0.0.1（IP地址修改为FTP服务器的IP地址）地址后，会有弹出框提示账号密码的输入，完成后可以以win文件风格来访问服务器内文件目录和内容。
***
### （二）用shell和命令行访问ftp服务器
在有权限和同网络下，使用cmd或者powershell都可以，通过命令行进行ftp服务器的访问。直接输入ftp 127.0.0.1，会有提示输入访问的账户密码，完成后进入ftp的命令行，然后使用一些windows shell命令就可以对文件目录进行操作，下载文件通常使用get和mget这两条命令，mget可以下载文件夹，用put和mput命令上传文件。
***
### （三）python脚本来连接ftp服务器和下载文件
通过ftplib这个库来撰写ftp连接和操作脚本。

```python
from ftplib import FTP
import datetime
 
def get_current_monday():
    '''
    作用:获取当前周的周一
    参数:无
    返回值:年月日格式的字符串类型数值
    '''
    monday = datetime.date.today()
    one_day = datetime.timedelta(days=1)
    while monday.weekday() != 0:
        monday -= one_day
    return datetime.datetime.strftime(monday, "%Y%m%d")
 
def conn_ftp():
    '''
     作用：连接ftp服务器
     参数：无
     返回：ftp服务器连接的对象
    '''
    # ftp连接信息(可修改)
    ftp_ip = "xx.xxx.xx.xx"
    # 默认端口21
    ftp_port = 21
    # 连接ftp的用户名(可修改)
    ftp_user = "xxx"
    # 连接ftp的密码(可修改)
    ftp_password = "xxx"
    ftp = FTP()
    # 连接ftp
    ftp.connect(ftp_ip, ftp_port)
    # ftp登录
    ftp.login(ftp_user, ftp_password)
    # 查看欢迎信息
    print(ftp.getwelcome())
    return ftp
 
def download_file(ftp, key, path, local_path):
    '''
     作用: 根据关键词下载文件
     参数1：ftp连接对象
     参数2：下载的关键词
     参数3：要展示的目录
     参数4：本地存放路径
     返回：无
    '''
    # 进入指定目录
    ftp.cwd(path)
    for file_name in ftp.nlst():
        if(key in file_name):
            try:
                print(file_name)
                local_filename = local_path + "/" + file_name
                f = open(local_filename, "wb")
                # 下载ftp文件
                ftp.retrbinary('RETR ' + file_name, f.write)
                print('ftp文件成功下载到本地')
                f.close()
            except Exception as e:
                print(e)
 
Monday = get_current_monday()
ftp = conn_ftp()
# 设置编码，解决上传的文件包含中文的问题
ftp.encoding = 'GBK'
# key下载的关键词(可修改)
key = "LTPerformance_FOC_"+ Monday
path = "/Pure Data/"
local_path = "D:/Pure_data/LTPerformance"
download_file(ftp, key, path, local_path)
```
***
