---
title: 从GitHub仓库备份到Termux克隆还原
subtitle: ---Hexo 源文件Chromebook迁移之路
date: 2019-07-27 21:46:46
tags:   [Hexo, NexT, GitHub, Termux]
---
新置办了台chromebook，想着必须要让新的生产工具提供点儿生产力啊，哪怕是伪装生产力也好啊。那就把hexo迁移过来，拿markdown写点东西吧，问题也就随之来了。Hexo是用GitHub作为远端仓库，但是吧这仓库里面有的只是静态网页，而没有你电脑里生成网页的那一大堆源文件。所以你要是想拿新电脑写，就不能指望仓库，而得自己把这一大堆源文件拿过来。这位爷说了，这个简单，拷过来不就完了吗？不介，这些源文件大多都是不能支持直接复制的，抖这机灵没用，本文讲的就是这事。
***
### Step 1 远端仓库备份
    cd /hexo项目根目录
    git status            //提示无本地git仓库，虽然是源文件的所在地
    git init              //好吧，那咱来新建一个本地仓库
    git add .             // 将根目录下的所有文件列表提交到缓冲区
    git commit -m 'comment of what u have done'   //真正提交并执行动作
    git branch hexo       //新建一个以hexo命名的本地仓库分支，其他名亦可
    git checkout hexo     //切换到本地仓库新建hexo分支下
    git push origin hexo  //将本地仓库push到GitHub，并以新建hexo为分支名
  
  注：在执行 *git add .* 之前，要将hexo项目根目录下的 **themes/** 文件夹内NexT主题文件夹中的 **.git** 文件夹整体删除掉，否则整个主题文件夹的内容是无法add到缓存的，当然也就无法备份到GitHub仓库了，直接后果就是在克到的新平台上 **hexo g -d** 后静态网页上啥都没有了。
  
   当然，如果想删除分支，见下：
       
    git branch -d 'branch name'    //删除本地分支
    git push origin --delete hexo  //在GitHub远端仓库删除名为hexo的分支

备份完成后，现阶段的情况就是本地和远端仓库各有两个分支了，master和hexo *（可以不叫hexo）*。本地仓库的两个分支都存的是源文件，**hexo branch** 一个后，另外一个就在文件夹里隐藏了；远端仓库的两个分支master存的是静态网页，而新建的hexo存的就是刚刚push过去的源文件。但是心思缜密的你会发现push到远端的文件要比本地文件少啊，原因参见：[简书-Hexo博客备份](https://www.jianshu.com/p/57b5a384f234) 。

接下来一步就是把远端仓库里面这个分支的内容搞到新平台里面。 

****
### Step 2 新平台本地克隆
由于吧，哥们这新平台有点儿葛，是Android的本，所以没办法直接装Git，所以就得先在play里面装个模拟器，**Termux** ，接着走起来！

    apt install git
    apt install nodejs
    git clone -b hexo https://github.com/username/username.github.io
    cd ～/username.github.io
    npm install

得嘞，这就算完了。看一眼chromebook里会在termux的文件系统里生成一个以**username.github.io** 命名的文件夹，里面就是克隆下来的远端仓库源文件。但是由于没法root chromebook，所以在模拟器里面的文件是无法直接修改的。要编辑博文需要用到第三方工具，这篇博文就是用马克飞象写的。
***
### Step 3  走起来
老平台，还是沿用hexo作为本地仓库分支；
在任何平台上都用如下套路发文即可：

    git pull origin hexo    //每次先从GitHub仓库同步源文件，有可能别人改了
    hexo n ‘’
    hexo g -d
    git add source          //因为也不干别的，没必要-a
    git commit -m ‘’
    git push origin hexo    //每次完工，别忘了再把本地源文件push到远端仓库
    
    


### tips：NexT主题优化：
[基本主题配置](https://www.jianshu.com/p/d350dec39078)
[四卷真经](https://www.jianshu.com/p/3ff20be8574c)
[进阶超炫](https://www.jianshu.com/p/9f0e90cc32c2)




