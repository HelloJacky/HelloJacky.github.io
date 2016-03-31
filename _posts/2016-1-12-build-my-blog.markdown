---
layout: post
title: "我的博客"
date: 2016-1-12 18:26:47
categories: 杂谈
tags: 博客 GitHubPages Jekyll
---

##开篇

折腾了两天，终于搞好了这个小博客，索性这第一篇文章就总结下搭建这博客的方法和经验得了。       

##为什么要搭建自己的博客    
总结过去(zhuang)，展望未来(b)。       

##如何搭建     

搭建博客的方式有很多，我这里用的是GitHub Pages和Jekyll，为什么用这个组合呢？   

* GitHub Pages空间免费（好像是300M），流量无限，无需购买或者搭建自己的服务器（这酸爽~）。   
* 结合Jekyll可以实现轻量级的博客系统，没有复杂的配置（So Easy！）。
* Jekyll支持Markdown，或者Textile（Cool~）。
* 多种第三方主题和插件（就喜欢能扩展的）。
* 可以绑定自己的域名（又可以装逼了）。

接下来就讲一下怎样搭建。   

###在GitHub上建立自己的站点仓库   
 去[GitHub Pages](https://pages.github.com/)按照上买的说明步骤创建你的站点仓库，我们搭建的是博客，所以类型就选择User or organzation site，然后clone你的仓库到本地，准备添加内容。   
 
###安装Jekyll
Jekyll 究竟是什么？我摘抄下官网上的介绍吧： 
   
**Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。** 
  
官方网站可以自己搜，上面有文档，不过都是英文的，英文不好的小伙伴可以看[这里](http://jekyll.bootcss.com/)（我叫雷锋），感谢Bootstrap中文网的翻译。  

安装方式在这列举**两种**：   
1. 按照官网上的步骤用 gem 安装   
2. 另一种就是GitHub上面推荐的利用Ruby软件管理工具Bundler安装（[传送门](https://help.github.com/articles/using-jekyll-with-pages/)）

博主推荐第二种方法，因为你可以轻松的管理你的软件。那既然如此，就要安装Bundler,执行命令：    
 
``gem install bundler``   

安装完成后，在你的工程目录下 新建一个Gemfile文件，添加如下代码：  

{% highlight ruby %}

source 'https://rubygems.org'  
gem 'github-pages' 
  
 {% endhighlight %}
 
 保存，然后执行  
 
 ``bundle install``  
 
 这时候bundler会分析依赖，然后逐个下载，类似CocoaPods，完成后jekyll就安装成功了。   
 
 如果将来需要更新环境的话，你只需要：
 
 ``bundle update``
    
###生成博客系统   
 接下来在你的站点仓库下新建一个Jekyll博客，执行如下命令：
   
 ``jekyll new blog``  
 
 执行完成后，你会看到生成的blog文件夹，文件夹内就是站点的所有文件，其实就是一套站点模板，现在你的仓库目录结构是  
 
 ***yourname.github.io***   
 　　|--*Gemfile*  
 　　|--***blog***   
 
如果这样子push到你的GitHub上是不行的，你生成的Jekyll文件必须全部在你的根目录下，所以你需要把blog文件夹下的文件全部移到根目录下（***yourname.github.io*** 文件夹），这样子push到你的github上，就能正常运行了，不过别着急push，现在本地看下效果，执行命令：
  
``bundle exec jekyll serve``  

你的站点在本地已经开始运行了，打开chrome输入**localhost:4000**,
就会看到生成的默认样式站点，此时是不是有点小激动(o^^o)♪，然后再把代码push到github仓库，然后在chrome输入**http://username.github.io**，然后你的博客就运行在github上了。Yes！

然后我们再回来看下这个博客系统的目录结构，在[官方文档](http://jekyll.bootcss.com/docs/structure/)中有详细介绍，我们写文章的时候只需要在***_post***文件夹下写markdown即可，其中还说明了Jekyll的核心就是一个文本转换引擎，因为GitHub Pages上只能运行静态网页，所以Jekyll的功能就是帮我们生成一个全静态页面系统，其中包括将我们写的markdown生成为静态页面。   

还有一些功能配置在文档中也有很详细的说明，在此就不细说了。

###更换主题
嫌弃默认主题丑？好的，这里有[Jekyll Themes](http://jekyllthemes.org/)，请自行挑选，别忘了给作者个赞哦~  
其实这些主题都是作者已经配置好的系统，首先删掉你站点仓库下除*Gemfile*和*Gemfile.lock*外所有的文件和文件夹，然后将下载的源码直接丢到你的站点仓库里就可以了，然后重新运行：

``bundle exec jekyll serve``  

当然你的前端功夫好的话，你也可以自己做主题，至于怎么做？看了文档中的目录介绍你就懂了。

###绑定自己的域名
先上GitHub的[说明文档](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)，然后我在解说下，首先在你的站点仓库中创建一个名为CNAME的文件（既别名记录），添加内容为你的域名，注意不要带有协议（*http://*、*https://*、...），这里你写的域名是最后映射成的域名，举例说明：
  
假如说你写的是*www.blog.com*，那么你在浏览器中输入*blog.com*还是会映射成*www.blog.com*

假如说你写的是*blog.com*，那么你在浏览器输入*www.blog.com*最后会映射成*blog.com*

映射的地址始终和你写的一样，最后还有重要的一步，就是设置你域名解析到的GitHub服务器，在你的域名解析系统里设置（没有域名的自己去买喽，装逼是要付出点代价的😂），GitHub提供的两个服务器地址：*192.30.252.154*、*192.30.252.153*，自己选一个或者都写上，在你的域名解析系统里添加A记录，如下：  
 
![图1](/images/2016-1-12-build-my-blog/image1.jpg){: image featured}  
![图2](/images/2016-1-12-build-my-blog/image2.jpg){: image featured}  

设置成功后，等待解析生效，打开浏览器，输入你的域名。。    
“卧槽，好刺眼！！”



