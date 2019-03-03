## 一、 准备工作
&emsp;首先你需要有一个github账户，同时电脑里安装git，
这些工作准备好了之后，可以开始我们的Pycharm体验了。  
> 说明: 博主的Pycharm是2018.1版本。

## 二、 配置Pycharm的Git环境
&emsp;1.打开Pycharm，选择菜单栏的`File -> Settings ->
Version Control -> Github` :  
![1_File_Settings](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/1_File_Settings.png)  
&emsp;2.输入自己的github账号:  
![2_配置Github](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/2_%E9%85%8D%E7%BD%AEGithub.png)  
&emsp;3.在同个目录下选择Git，填上自己安装的Git路径:  
![3_配置Git](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/3_%E9%85%8D%E7%BD%AEGit.png)  

## 三、 从Github导入项目到本地
假如你打算克隆别人的项目，或者是参与别人的项目，亦或者是下载自己Github
仓库里的项目，需要复制下图1的URL  
>说明: 如果是参加别人的项目，并贡献你自己的代码，需要fork(下图2的位置)
一下别人的项目，然后在你自己的Github仓库就能看到一个属于你自己的项目副本

![11_克隆](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/11_%E5%85%8B%E9%9A%86.png)  
&emsp;1.选择菜单栏的`VCS -> Checkout from Version Control`，
选择 `Git`  
![4_从Git检出项目](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/3_%E9%85%8D%E7%BD%AEGit.png)  
&emsp;2.在弹出的窗口的URL填上你要导入的Github上的项目地址，Directory
填上保存到本地的路径，然后点击Clone，克隆好了就选择打开  
![5_克隆远程仓库](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/5_%E5%85%8B%E9%9A%86%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93.png)  

## 四、 将本地创建的项目上传到Github上
&emsp;选择菜单栏`VCS -> Import into Version Control -> Share Project on Github`就可以了  
![10_本地项目上传到Github](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/10_%E6%9C%AC%E5%9C%B0%E9%A1%B9%E7%9B%AE%E4%B8%8A%E4%BC%A0%E5%88%B0Github.png)

## 五、 如何提交本地修改，更新到Github
&emsp;1. 在Pycharm中修改过的文件会显示蓝色，新建的文件会显示红色(没有Add操作之前)或绿色(Add操作之后)  
![6_文件颜色显示](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/6_%E6%96%87%E4%BB%B6%E9%A2%9C%E8%89%B2%E6%98%BE%E7%A4%BA.png)  
&emsp;2. 鼠标右键项目目录，先选择 `Git -> Add`，再选择 `Git -> Commit Directory...`  
> 说明: 如果读者是参与别人的项目，在Commit之前要先Pull，作用是先更新本地的代码，防止你克隆项目
后到提交项目前的这段时间，原项目已经更新，导致合并冲突，Pull操作下面会说明  

![7_Comit](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/7_Comit.png)
![8_提交更改](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/8_%E6%8F%90%E4%BA%A4%E6%9B%B4%E6%94%B9.png)  
&emsp;3. 仅仅是进行Commit操作是不会更新到Github的，还需要Push操作  
鼠标右键项目目录，选择 `Git -> Repository -> Push`  
![9_Push操作](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/9_Push%E6%93%8D%E4%BD%9C.png)
> 说明: Pull操作也在这里  
如果遇到`OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443`的错误，  
一般是你开启了代理，关掉了就好

## 六、 Pull Request
这部分操作的作用是，在你贡献了自己的代码后，发送给原项目的管理者，让其审核是否合并你贡献的代码  
![12_Pull_Request](https://github.com/olewaLdeisi/olewaLdeisi.github.io/blob/master/img/Pycharm%E4%B9%8BGit%E7%B3%BB%E5%88%97/imgs/12_Pull_Request.png)
<br/>
本文完，敬请期待下一篇 [Pycharm之Git分支管理]()




