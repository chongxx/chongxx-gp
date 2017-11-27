+++
showonlyimage = false
draft = false
image = "https://i.ytimg.com/vi/FiOgz3nKpgk/maxresdefault.jpg"
date = "2014-11-05T18:25:22+05:30"
title = "使用Hugo打造Github Page 博客"
weight = 1
+++

__Time：2017-11-25__


**这篇blog介绍一下如何使用[hugo](https://gohugo.io/)在github page上创建个人博客**

<!--more-->

### 创建Github Page

---

##### 1、第一步你需要先有一个github账

##### 2、在你的github上创建一个仓库名为__\<username\>.github.io__的空代码仓库

##### 3、克隆这刚刚创建的项目到本地，请把username换成你的github username
```console
$ git clone https://github.com/username/username.github.io.git
```

##### 4、在项目的根部创建一个`index.html`文件，这个文件将作为你github page的首页
```console
$ echo 'hello world' > index.html
```

##### 5、push代码到github
```console
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```

##### 到这一步其实你的github page就已经上线，快的话现在浏览器打开__\<username\>.github.io__就可以看到刚刚提交的页面了,如下：（也有可能是404需要等1~15分钟才能看到）
<img src="http://oxp6uindp.bkt.clouddn.com/blog/blog171125-1.png" style="width: 100%;"/>

### 使用Hugo来完善Github Page
---

> 但这样实在是太简陋了，接下我们使用hugo来丰富一下这个blog

##### 1、直接下载hugo编译好的二进制文件到本地解压后把hugo放到环境变量中 [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases)（我认为这是最快的方法，当然你也可以看[hugo quick start](https://gohugo.io/getting-started/quick-start/) 的Quick Start来安装）

##### 2、hugo已经安装好了，这时候我们可以使用hugo来生成一个静态网站
```console
$ hugo new site blog
```
##### 3、去[https://themes.gohugo.io/](https://themes.gohugo.io/)挑选一个你喜欢的网站主题吧
如果你想快点看到效果，也可以使用目前我使用的这个网站主题，进入到第2步创建的hugo项目中

```console
$ mkdir themes
$ cd themes
$ git clone --depth=1 https://github.com/kishaningithub/hugo-creative-portfolio-theme.git
$ rm -rf hugo-creative-portfolio-theme/.git
$ cp -r hugo-creative-portfolio-theme/exampleSite/* ../
$ cd ..
$ hugo server
```

##### 4、hugo已经开启了一个本地server打开[http://127.0.0.1:1313](http://127.0.0.1:1313)就可以在本地看到hugo生成的静态站点了
<img src="http://oxp6uindp.bkt.clouddn.com/blog/blog171125-2.png" style="width: 100%;"/>

##### 5、删除hugo生成的项目里的`public`文件夹，把`username.github.io`项目clone到这个hugo项目中命名为public，作为这个项目的子模块（`public`文件夹就是hugo生成整个静态网站）
```console
$ rm -rf public
$ git clone https://github.com/username/username.github.io.git public
```

##### 6、回到hugo项目的根目录运行命令生成静态站点，把静态站点push到`username.github.io`
```console
$ hugo
$ cd public
$ git add .
$ git commit -m"Used Hugo create Blog"
$ git push -u origin master
```
大功告成，再次访问`http://username.github.io`,就可以看到你的Github Page博客了（一样的，可能会有1~15分钟的延迟）

### 最后
---

##### 那我们怎么开始写blog呢？
已有的文章内容是这个主题的示例在`content`文件夹里，你可以全部删掉或修改在`content`文件夹里（About和Contact也一样）

##### 修改或者新发布文章怎么操作？
在`content/portfolio` 里修改或新增对应的markdown文章，然后是hugo命令生成静态站点文件在`public`文件里，再进入`public`文件夹使用git push修改到`username.github.io`仓库就OK了

##### 上面的这个过程还是有点麻烦，所以我写了对应的bash脚本来完成这个操作，保存到hugo项目的根目录为deploy.sh，每次修改或新增文章后运行一下脚本就OK了`$ bash deploy.sh`，脚本内容如下
```console
hugo \
&& cd public \
&& git add . \
&& git commit -m"update `date "+DATE: %Y-%m-%d TIME: %H:%M"`" \
&& git push
```

<br/>
### 最最最后再提醒下
---

1. 每次修改文章后建议先在本地运行`$ hugo server`看看blog运行是否正常，再push
2. Github Page 还有很多细节比如自定义域名等，请看相关文档 [https://github.io](https://github.io)
3. Hugo 也还有很多细节，请看相关文档[https://gohugo.io/](https://gohugo.io/)
4. 主页的菜单、联系方式等配置都可以在根目录的`_config.toml`中修改
5. 想要自定义主题样式怎么办？当然是看hugo的文档啦!这还用问我~
6. 谢谢~
