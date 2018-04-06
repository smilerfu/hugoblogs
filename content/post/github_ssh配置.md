---
title: "GitHub的SSH配置"
date: 2018-04-05T01:39:00+08:00
lastmod: 2018-04-05T01:39:00+08:00
keywords: []
description: ""
tags: []
categories: ["Git"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
---

<!--more-->

### 克隆仓库
我们在github上克隆仓库的时候，一般使用ssh或者https这2种方式。
![](/images/git/git_clone_ssh_https.png)

https在git push的时候每次都要输入账号和密码。因此比较繁琐。

所以我们一般采用ssh方式来克隆远程仓库。

不过采用ssh方式时，我们需要先配置下密钥。

### 生成ssh秘钥
生成ssh秘钥一般有两种方式，一种使用git生成，另一种则使用TortoiseGit自带的PuTTYgen生成。

##### 方式一、 使用git生成
1. 右键选择 ```Git Bash Here``` 可打开git的控制台窗口
2. 输入以下命令生成秘钥

    ```ssh-keygen -t rsa -C "example@email.com"```

    其中:

    * ```example@email.com``` - 你你自己的github邮箱地址

    按回车后，会有一些输入项让你配置，默然直接回车即可。

    最后控制台的输出如下:

    ```
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/UserName/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/UserName/.ssh/id_rsa.
Your public key has been saved in /c/Users/UserName/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:xxxxxxxxxxxxxxxxxxx example@email.com
The key's randomart image is:
+---[RSA 2048]----+
|xxxxxxxxxxxxxxxxxxx|
+----[SHA256]-----+
    ```

    其中:

    * ```UserName``` - 你的计算机用户名
    * ```example@email.com``` - 你输入的github邮箱地址
    * ```xxxxxxxxxxxxxxxxxxx``` - 每个人都不同
        
    从而我们就得到了一对公钥和私钥。

    公钥存放在```c/Users/UserName/.ssh/id_rsa.pub```中

    私钥存放在```c/Users/UserName/.ssh/id_rsa```中

##### 方式二、使用TortoiseGit自带的PuTTYgen生成


### github配置ssh
1. 打开github配置界面

    ![](/images/git/github_settings_menu.png)

2. 选择SSH and GPG keys

    ![](/images/git/github_settings_ssh.png)

3. 选择New SSH key

    ![](/images/git/github_settings_ssh_new.png)

4. 输入新的SSH Keys
    ![](/images/git/github_settings_ssh_new_add.png)
    其中:

    * ```Title``` - 用于区分不同秘钥，可自行定义
    * ```Key``` - 即上面生成的公钥文件```id_rsa.pub```里面的文本内容

        可通过以下命令获取:

        ```
            cd ~/.ssh
            cat id_rsa.pub
        ```
        把控制台输出的文本拷贝到输入框中。

5. 点击 Add SSH key 按钮就配置成功了

### 配置TortoiseGit
方式1使用git生成的秘钥是无法直接在TortoiseGit使用的。我们还要为TortoiseGit进行一些设置。
设置有2种方式。
##### 方式一、将TortoiseGit的SSH client设置为git的ssh.exe
1. 打开TortoiseGit的设置界面，选择```Network```选项
2. 将SSH client设置为git安装目录下```usr\bin\ssh.exe```选项

![](/images/git/git_settings_network.png)

##### 方式二. 将上面git产生的私钥转换成TortoiseGit使用的ppk秘钥
1. 运行```puttygen.exe```(位于TortoiseGit安装目录下的bin目录)
![](/images/git/git_settings_puttygen_main.png)
2. 选择```Load```，加载方式一使用git生成的id_rsa私钥
![](/images/git/git_settings_puttygen_load.png)
3. 选择```Save private key```,保存为ppk格式文件。
4. 运行```pageant.exe```位于TortoiseGit安装目录下的bin目录)
5. 选择```Add Key```，选择刚才保存的 ppk 文件即可

### 修改仓库的访问方式(ssh或者https)
##### 查看当前的remote方式
```git remote -v```
##### 将ssh方式修改为https方式
```git remote set-url origin https://github.com/yourname/example.git```
##### 将https方式修改为ssh方式
```git remote set-url origin git@github.com:yourname/example.git```

### 问题汇总
##### 1. TortoiseGit disconnected no supported authentication报错
![](/images/git/git_error_disconnect_no_suported_authentication.png)
该问题即没有配置好TortoiseGit，按照上面配置TortoiseGit进行配置即可


git remote set-url origin git@github.com:smilerfu/smilerfu.github.io.git
