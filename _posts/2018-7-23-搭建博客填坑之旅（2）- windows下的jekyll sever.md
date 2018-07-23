---
layout: post
title: 搭建博客填坑之旅（2）- windows下的jekyll sever
date: 2018-7-19
tags: create_blog
---
### 说明
 - 前两天，被我拉入github博客坑的另一个友人突然问我，是不是在本地搭建过jekyll，我当然没有。因为当时想着工程也有了，博客也可以推了，本地jekyll啥的又要安装依赖又是推荐linux，我看着我的windows8完全不敢说话，笔记本上的windows也不敢说话。友人说有git bash基本的linux操作就不成问题了，我思考了一下，可能是时候搞一搞了。
 - 过程清单：问题的解决过程就不细说了，基本都是网上找的解决方法，细节和底层是真的不懂。
 - 第一步，下载rubyinstaller-2.3.3-x64和DevKit-mingw64-64-4.7.2-20130224-1432-sfx,可能需要梯子。这是我用的版本,当然不是说只能用这个版本，只是经过多测试目前只有这个版本兼容性最好，可以支持需要的所有依赖。
 - 第二步，安装ruby，最好安装在C,D,E,F...盘的根目录，然后勾选多选框的中间那项，说是可以自动配置环境变量。解压DevKit到任意位置。
 - 第三步，转到DevKit文件夹中，可以看到有一个dk.rb，打开git bash执行命令，ruby dk.rb init -> 出现了一个文件config.yml -> 打开cofig.yml在末尾加上ruby的安装位置（比如：D:\Ruby23-x64）-> 执行ruby dk.rb review -> <img src='https://dawn1432.github.io\images\搭建博客填坑之旅\ruby_review.png' align='margin-left' style=' width:600px;height:600 px'/>没说配置有问题的话就执行ruby dk.rb install。
<hr>
至此依赖完成配置。接下来需要下载一系列文件，如果嫌弃gem原本的源的话，可以添加ruby中国的源。由于有点ssl的证书信任问题，ruby中国论坛提供了一个解决方案：<a href="https://ruby-china.org/topics/33843" target="_blank">https://ruby-china.org/topics/33843</a>
<hr> 
 - 第四步，下载jekyll，执行gem install jekyll。
 - 第五步，用jekyll新建一个博客文件夹，jekyll new blog，然后转进去，cd blog/
 - 第六步，哇，现在是不是jekyll s就可以本地运行了？！！超级激动٩(๑>◡<๑)۶。先用jekyll -v试一下命令，当梦想照进现实。<img src='https://dawn1432.github.io\images\搭建博客填坑之旅\bundler_error.png' align='margin-left' style=' width:600px;height:600 px'/>
 - 看了下原模板博主的博客，好像是需要安装bundler，于是gem install bundller。然后再jekyll -v。(╯‵□′)╯︵┻━┻<img src='https://dawn1432.github.io\images\搭建博客填坑之旅\minima_error.png' align='margin-left' style=' width:900px;height:900 px'/>
 - 如此反复，大概需要执行以下几个命令gem install minima，gem install tzinfo-data，gem install wdm。如果这个新建的blog能成功运行的话，访问localhost:4000就应该可以看到一个正确的页面。
 - 接下来就不用管这新建的blog了，进入你拉取的blog仓库的位置，执行jekyll s就可以在本地看到自己的博客了。最后，如果需要用到我的模板的话大概还要安装下面两个依赖，gem install jekyll-paginate，gem install jekyll-sitema。如果执行了这两条命令，还是提示这个依赖没有的话，就检查一下博客仓库根目录下的Gemfile，照着格式把这两个的依赖加进去。
 - 老泪纵横，终于不用冒着构建失败的风险，推到github再看效果了。