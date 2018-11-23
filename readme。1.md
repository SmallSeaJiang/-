pc端:  windows  osx

服务器端: 
    windows,
    linux: 由于linux本身是开源的,因此基于开源又开发很多版本的linux操作系统
        centos,
        redhat,
        debian,
        ubuntu: 移动端操作系统,pc端->苹果系统的操作

linux常用命令

ls   查看当前所在目录下所有的非隐藏文件或目录
参数说明
-a 查看当前目录下的所有文件,包括隐藏文件
-l 查看文件的详情
        -      rw-------. 1 root root    965    11月 21 10:33  anaconda-ks.cfg
        文件类型  文件权限     文件创建者 文件大小   文件创建时间    文件的名称
        文件权限: 读: read  r 4
                写: write w 2
                执行: execute x 1
        rw-     ---       ---
        拥有者  组权限   访客权限  
        -rw-r--r--. 1 root root   0 11月 21 15:22 index.html
        -rwxrwxrwx. 1 root root   0 11月 21 15:22 index.html
        修改文件的权限
        chmod 777 index.html
.:  当前目录
..: 上一级目录

cd 
作用: 进入指定目录
例如: 进入上一级目录 cd ..
    进入usr目录 cd usr
    进入根目录下的home目录  cd /home
    进入到根目录下的usr目录下的games目录 cd /usr/games
    回到初始目录 cd 回车即可

pwd
作用: 查看当前所在的目录的详细路径
    pwd

touch 
作用:创建文件
例子: touch index.js 在当前目录下创建一个index.js文件
    在指定目录下创建一个文件
    例子:在usr/games目录下创建index.html文件
    touch /usr/games/index.html
    列出games下的所有文件
    ls /usr/games

mkdir
作用: 创建目录(文件夹)
例子: mkdir download 创建下载目录
      mkdir /usr/games/腾讯

rm:
作用: 删除文件或目录
例子: rm index.html 删除index.html文件
      1.用这种方式删除文件,系统会弹出提示"否删除普通空文件",让选择是否真的删除,如果需要删除,则 填y或yes
      2.如果不想删除则输入其他非y或者yes的字符
     如果不想弹出提示,可以在rm后加上参数
        rm -f index.js会直接删除index.js文件,不会给提示

    rm无法直接删除目录,rm 目录名称的操作是失败的
    如果要删除目录则需要加上 -r    
    例子: rm -rf donwload 删除download目录,并且不需要系统确认提示.
    删除所有文件
        rm -rf *  
        删除所有以点开头的文件
        rm -rf .* 
       
命令:cp
作用:复制粘贴
例子: 
    将/root/download/下的index.html文件 复制粘贴到 /root/test目录,
    cp /root/download/index.html /root/test/index.html
    复制粘贴的同时给文件改名,常用于修改文件之前对文件进行备份
    cp index.html index.back.html
    复制目录,在当前目录下复制download目录,并给新目录起名为download2
    cp -r download download2

命令: mv
作用: 剪切或重命名文件
例子:  
    将当前目录下的index.html文件,重命名为index2.html
    mv index.html index2.html 

    将/root/test/index2.html移动到当前目录中
    mv /root/test/index.html ./

命令:cat
作用:预览文件内容
例子: cat index.html

命令:vi
作用:编辑文件
编辑过程: 
    1. vi 文件名.后缀 进入编辑模式
    2. 按i或s,进入编辑状态
    3. 按esc键->退出编辑状态
    4. 保存输入的内容->先输入冒号:然后输入w,保存完之后,退出编辑模式 按:q 退出
    5. 第四步可以同时完成 :wq 既可以保存退出

    注意: 如果写了一堆内容,发现写错文件,不保存直接强制退出 :q!

命令:tar
作用:压缩和解压文件
例子:
    tar -cf 压缩后的名称.tar 要压缩的文件或目录
    tar -cf download2.tar download2

    查看压缩包里目录结果
    tar -tvf download2.tar
    得到结果
    drwxr-xr-x root/root         0 2018-11-21 17:07 download2/
    -rw-r--r-- root/root         0 2018-11-21 16:42 download2/index.html
    -rw-r--r-- root/root         0 2018-11-21 16:42 download2/index.back.html
    drwxr-xr-x root/root         0 2018-11-21 17:08 download2/tencent/
    -rw-r--r-- root/root         0 2018-11-21 17:08 download2/tencent/qq.ext

    解压文件
    tar -xf download2.tar

命令: yum
作用:安装软件
例子: yum update(更新yum)
      yum install wget
命令:wget
作用: 下载网络上的软件包
例子: 下载nginx

命令: find
作用: 查找文件
例子: find / -name nginx

nginx的安装
1. 如果是新安装的centos系统,就需要安装一些编译工具,例如gcc等
    yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
2. 安装pcre工具
    wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
    解压pcre
    tar -zxvf pcre-8.35.tar.gz
    进入pcre-8.35目录
    1 ./configure
    2 make
    3 make install
3. 进入nginx解压的目录
    1 ./configure
    2 make
    3 make install
    nginx安装完成之后,nginx会存储在/usr/local/目录下
    nginx命令在 /usr/local/nginx/sbin/nginx

4. 启动nginx
    第一种启动方式
    进入 /usr/local/nginx/sbin目录
    执行nginx命令
        ./nginx
    第二种启动方式
        /usr/local/nginx/sbin/nginx
    第三种方式
        通过创建软连接(快捷方式)来快速启动nginx
        ln -s /usr/local/nginx/sbin/nginx /bin/nginx

5. 重启nginx
    根据进程号来停止nginx
        查看进程号
        ps -ef|grep nginx
        杀死进程
        kill -QUIT 2072

    强制停止nginx
     pkill -9 nginx

    重启nginx
    ./nginx -s reload

    使用secureCRT上传文件到linux服务器

    1. 右键虚拟机的选项卡,选择Connect SFTP Session

    2. 在sftp选项卡下的操作框中,切换linux的目标路径,也就是要将windows下的资源上传到linux的指定目录.
    
    3. 再通过 lcd 切换到windows要上传的文件所在的目录
        lcd F:\课堂\0914\第二阶段\day02\代码
    
    4. 通过put命令上传文件
        put -r 目录名称/文件名称
    
nginx项目配置
    配置文件路径 /usr/local/nginx/conf/nginx.conf

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80; //端口号
        server_name  localhost; //服务器地址
        location / {
            root   html; //项目在服务器中的位置
            index  index.html index.htm; //默认打开的页面
        }
    }
    server {
        listen 8080;
        server_name localhost;
        location / {
          root /home/spiritDemo;
          index index.html;
        }
    }
}