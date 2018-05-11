---
layout: post
cover: 'assets/images/cover3.jpg'
navigation: true
title: 使用CocoaPods创建私有库
date: 2018-05-10 16:56:00
tags: fables fiction
subclass: 'post tag-iOS tag-content'
logo: 'assets/images/ghost.png'
author: casper
categories: casper
disqus: true
---


#### 添加私有仓库

{% highlight objc %}
$ pod repo add 'repo name' 'repo address'
{% endhighlight %}

#### 创建lib

{% highlight objc %}
$ pod lib create 'library name'
{% endhighlight %}

#### lint lib

{% highlight objc %}
$ pod lib lint

      Validates the Pod using the files in the working directory.
{% endhighlight %}

#### lint spec

{% highlight objc %}
$ pod spec lint [NAME.podspec|DIRECTORY|http://PATH/NAME.podspec ...]

      Validates `NAME.podspec`. If a `DIRECTORY` is provided, it validates the
      podspec files found, including subfolders. In case the argument is
      omitted, it defaults to the current working dir.
{% endhighlight %}

#### 推送到仓库

{% highlight objc %}
 $ pod repo push REPO [NAME.podspec]

      Validates `NAME.podspec` or `*.podspec` in the current working dir,
      creates a directory and version folder for the pod in the local copy of
      `REPO` (~/.cocoapods/repos/[REPO]), copies the podspec file into the
      version directory, and finally it pushes `REPO` to its remote.
{% endhighlight %}

#### tips

如果Lib里面依赖了不同仓库的Pod, pod lib lint, pod spec lint 的时候需要添加 --sources 参数

{% highlight objc %}
pod lib lint pod.podspec --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git
{% endhighlight %}

可以在~/.bash_profile 定义函数来省去重复的输入

{% highlight objc %}

function podlint() { pod $@ lint --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git; }

function podpush() { pod repo push $@ --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git; }

{% endhighlight %}

使用方式

{% highlight objc %}

podlint lib

podlint spec

podpush pod.spec

{% endhighlight %}


