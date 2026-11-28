# 确认基础信息的操作<br>
whoami #查看当前登录用户<br>
hostname #主机名<br>
clear #清屏，crel L也可以清屏<br>
# Teminal：人机对话窗口
Shell：命令行解释器<br>
eho $SHELL #输出：/bin/bash 意思是正在使用bash
# 关于[root@localhost~]#
root用户名，root是超级管理员模式，普通的是student<br>
@分隔符<br>
localhost主机名<br>
~当前所在目录，~表示家目录<br>
#提示符。 #是超级用户，$是普通用户<br>
# 命令格式语法（约定俗成的东西，其实到后期命令格式是可以自己写的，不要死板）
命令 [选项] -[参数]<br>
如ls -l /home #注意空格，前面ls的l是list缩写，不是i的大写，后面-l是L小写表示long<br>
ls 命令本身<br>
-l 选项(怎么做，通过长格式long表示)参数是变化最大的<br>
/home(对象，也就是对谁做)<br>
# 一些基础命令
注意：操作前一定注意大小写和空格，否则可能无法运行或者错误运行<br>
echo:类似printf，就是输出内容，也就是复读<br>
比如echo Hello World然后entre，它就显示Hello World<br>
sleep:即等待，sleep 3就是等待3秒，这三秒内命令无法输入，也就是硬控你3秒<br>
ctrl c可以终值命令<br>
# 参数的几种种类
1.不带值的参数 #一般作为开头使用 -[参数名] 如-a<br>
2.带值参数 #传递具体值的 -[参数名] [参数值] 如 -n 10<br>
3.不带值的长参数 #一般作为开关使用，类似不带值的参数 --[参数名] 如 --all<br>
4.带值的长参数 #传递具体值 --[参数名]=[参数值] 如 --size=10MB<br>
5.位置参数 用于传递具体的操作对象 [操作对象]... 如 sample.txt<br>
原则上，程序可以设计任意的命令参数语法，但是前提是你是编脚本的那个，目前你是使用者，只能按照格式来.<br>
# 关于一些键盘上的操作
1.tab<br>
在你懒得去输入全指令名称的时候，tab可以帮你补全，如果没反应说明有多个候选项，可以连续按两次tab列出候选，继续输入几个关于命令的字母，消除隔阂再按tab补全<br>
2.home可以到命令最左边，end反之，ctrl←左移
3.复制 ctrl+insert
粘贴 shift+insert
# 获取命令文档
--help下提供文档学习，也可以使用manual获取，也就是man命令名
注意：命令本身提供了手册才能获取
# 区分
windows是\，但是Linux是/ 如ls /home/.../
目录树：Linux只有一个根节点/，但是windows是C:\ D:\
大小写，Linux注重，win反之
# 路径的写法
绝对路径：从根目录/开始，一级一级的写路径一直达到你想到的地方
相对路径以当前目录开始，倒退上一层，..代表上一层，.代表当前工作目录
例子
现在在 /home/nick/projects/app
pwd                      # -> /home/nick/projects/app，打印当前所在目录
绝对路径：从 / 一路写到底，在哪敲都一样
cat /etc/nginx/nginx.conf
相对路径：接着当前位置往下
cat src/main.py           # -> /home/nick/projects/app/src/main.py
.. 上一层
cd ..                     # 现在在 /home/nick/projects，切换目录
cat logs/app.log          # -> /home/nick/projects/logs/app.log查看/拼接文件内容

cd ../app                 # 回到 /home/nick/projects/app

. 当前目录
./run.sh                  # 等价于 run.sh（但要可执行权限）
cp ./a.txt /tmp/          # 明确「就是这个目录的 a.txt」复制文件或者目录
注意：家目录可以直接用~，root是可以的
# 指令
## cd:切换到特定目录
如cd tmp/
cd ..  #切换到上一层
cd  #回到家目录
cd - #上一次所在目录，两次cd -就会循环
## ls：打印目录list，也就是printf
核心参数：
·位置参数：想打印的目标目录，不传则打印当前工作目录
·-a：打印隐藏内容
extra：隐藏内容就是开头带.的目录，如.cache .config（类比图片隐藏）
-l：详细列表的形式打印
-F：文件名后显示类别的指示符
-h：更直观的形式显示文件大小
