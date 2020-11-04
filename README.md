# 个人博客

hexo——简单、快速、强大的Node.js静态博客框架，请访问https://belly0.github.io/

## 操作步骤(git bash下操作)
- hexo new post '文件名'(根目录下且不带后缀名)或hexo new '文件名'（\source\_posts文件夹下）
- hexo server(或者简写:hexo s）：打开本地服务器查看
- hexo generate(或者简写:hexo g) ：生成静态网页
- hexo deploy(或者简写:hexo d)：部署文章

参考文档：https://blog.csdn.net/sunhwee/article/details/100109805#28__765

## 初次备份源文件

github中添加MyBlog分支

- git branch -a
- git checkout MyBlog
- git add --all
- git commit -m ""
- git remote add origin github网址
- git push -u origin MyBlog

## 源文件分支更新

- git add . *#添加所有文件到暂存区*
- git commit -m "新增博客文章"  *#提交*
- git push origin hexo *#推送hexo分支到Github*

## 新电脑环境下的恢复安装hexo以及相关依赖，克隆hexo分支到本地

- git clone -b hexo github网址

写文章，hexo g, hexo d，发布到master分支
再更新备份到hexo分支，三步, `add`, `commit`, `pull`