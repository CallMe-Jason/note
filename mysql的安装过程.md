1. 安装全局的环境变量

   ```
   控制面板\系统和安全\系统
   
   点击高级系统设置
   点击环境变量
   在用户自己变量里面  点击 path
   然后点击新建，将我们的 mysql的bin目录的地址粘贴过去
   
   然后打开终端，输入 mysql， 如果出现正常的mysql提示就安装成功了
   ```

2. 使用黑窗口进入mysql数据库

   ```
   mysql -u root -p  回车
   输入密码
   进入数据库了
   
   show databases;   分号不能掉，表示显示数据库的意思
   
   创建一个数据库，名称是hkzf
   create database hkzf;
   
   创建了以后，就要进入数据库  use hkzf;
   
   
   接下来就是导入数据库sql文件的操作
   source c:/hkzf_db.sql;    这一步就是导入sql文件的意思，文件很大，要等一会
   
   成功以后，使用 show tables； 检查是否成功
   ```

   