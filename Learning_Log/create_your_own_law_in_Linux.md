关于实现编写规则的方法，目前26年11月22日，有三个可学习和执行的方法
# 临时编写法
核心：使用alias
例子：alias home='ls -l /home'
接下来，在系统里面输入home，他的效果就等效后面ls，直接查看家目录
# Shell脚本法
1.新建文件夹
输入mkdir myscript(新建文件夹，关于myscript)
输入cd myscript（进入）
2.创建文件（这里以创建一个关于快捷输出hello world的脚本为例子）
输入vim hello.sh（创建一个叫hello的脚本文件，后缀sh）
3.输入正文
输入：
#!/bin/bash
echo "Hello world"

(#!/bin/bash是通行证，告诉系统用bash跑这个文件，这个必须在第一行)

按esc，输入:wq回车
终端输入chmod +x hello.sh(赋予执行权限)
运行：./hello.sh
# 关于可能会遇到的虚拟机未联网的问题
VMware的虚拟交换机在后台服务器挂了，导致虚拟机虽然是已连接状态但是并没有真正的虚拟网线接入
# 解决方案
windows宿主机上win+R搜索services.msc，找到VMware Nat Service和VMware DHCPService是"正在运行"状态
然后，在Linux上reboot虚拟机
现象：网络通了，但打不开网页（无法解析域名）
测试：输入 ping -c 4 114.114.114.114 是通的，说明网络没问题。但输入 ping -c 4 www.baidu.com 报错 Name or service not known。
根源：系统找不到“域名翻译器（DNS服务器）”。
手动指定DNS：输入vi /etc/resolv.conf，按i进入编辑模式，
把里面原来所有的内容全部删掉，清空页面。
输入以下两行（敲回车换行）
nameserver 114.114.114.114
nameserver 8.8.8.8
按 Esc，输入 :wq 保存退出。
再次 ping www.baidu.com，瞬间通畅，然后就可以 dnf install vim -y （安装vim）了。
安装完，回到上面，从头开始就好
