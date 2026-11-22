关于实现编写规则的方法，目前26年11月22日，有三个可学习和执行的方法
# 临时编写法
核心：使用alias
例子：alias home='ls -l /home'
接下来，在系统里面输入home，他的效果就等效后面ls，直接查看家目录
# Shell脚本法
dnf install vim -y 先下载vim
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
以后输入。/hello.sh就可以直接显示了
<img width="1032" height="188" alt="屏幕截图 2026-11-22 173339" src="https://github.com/user-attachments/assets/ebc0e697-6683-4b89-9197-9b9918bd033d" />

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
# c语言法（编程语言法）
先下载gcc，也就是c语言编译器dnf install gcc -y
    新建文件夹并进入
    输入 mkdir my_c_program（新建一个专门放C程序的文件夹）
    输入 cd my_c_program（进入这个文件夹）
    输入 ls -l（这是个小习惯，查一下里面是不是空的）
    创建C语言文件
    输入 vim myprogram.c（创建一个叫这个的C语言文件，后缀是 .c。注意，和Shell脚本不一样，C语言是 .c）
    输入正文（注意头文件！）
    输入以下代码（我这是极简版）：
    c
    #include <stdio.h>
    #include <string.h>

    int main(int argc, char *argv[]) {
        if (argc > 1) {
            if (strcmp(argv[1], "-o") == 0) {
                printf("openEuler mode\n");
            } else {
                printf("Other mode\n");
            }
        } else {
            printf("No args\n");
        }
        return 0;
    }
    (这里有个大坑，最开始我在 #include <stdio.h> 和 <string.h>，前面有东西没删干净导致一编译满屏爆红字！C语言极其严格，用 printf 必须写 stdio，用 strcmp 必须写 string。)
    写好之后，按 Esc，输入 :wq 保存退出。
    编译（最关键的一步！）
    和 Shell 脚本（直接 chmod 给权限就能跑）不同，C 语言源码电脑看不懂，必须先翻译（编译）！
    输入 gcc myprogram.c -o myprogram
    (意思是：把 myprogram.c 翻译成机器能懂的可执行文件，并给它起名叫 myprogram。如果没有报错直接跳回提示符，就是成功了。)
    运行
    输入 ./myprogram -o（记住，自己做的程序，必须加 ./，后面的 -o 是传进去的参数）
    屏幕上就会打印出 openEuler mode！
# 关于C语言法我犯的错（踩坑记录）：
    没编译就想跑：只写了 .c 文件直接敲 ./myprogram，系统疯狂报错 No such file or directory。因为没经过 gcc 编译，系统里根本就不存在这个程序。
    把参数当命令：在终端直接敲了 -o 回车，报错 command not found。-o 只是传给程序的开关，不能直接运行，得跟着程序屁股后面跑。
    忘记加 ./：直接敲 myprogram，系统说找不到，因为系统只会去大超市（/bin等）找，你要想运行自己小卖部（当前目录）里的东西，必须用 ./ 指路。

