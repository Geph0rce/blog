---
title: 使用CocoaPods创建私有库
---


#### 添加私有仓库

``` bash
$ pod repo add 'repo name' 'repo address'
```

#### 创建lib

``` bash
$ pod lib create 'library name'
```

#### lint lib

``` bash
$ pod lib lint

      Validates the Pod using the files in the working directory.
```

#### lint spec

``` bash
$ pod spec lint [NAME.podspec|DIRECTORY|http://PATH/NAME.podspec ...]

      Validates `NAME.podspec`. If a `DIRECTORY` is provided, it validates the
      podspec files found, including subfolders. In case the argument is
      omitted, it defaults to the current working dir.
```

#### 推送到仓库

``` bash
 $ pod repo push REPO [NAME.podspec]

      Validates `NAME.podspec` or `*.podspec` in the current working dir,
      creates a directory and version folder for the pod in the local copy of
      `REPO` (~/.cocoapods/repos/[REPO]), copies the podspec file into the
      version directory, and finally it pushes `REPO` to its remote.
```

#### tips

如果Lib里面依赖了不同仓库的Pod, pod lib lint, pod spec lint 的时候需要添加 --sources 参数

``` bash
pod lib lint pod.podspec --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git
```

可以在~/.bash_profile 定义函数来省去重复的输入

``` bash

function podlint() { pod $@ lint --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git; }

function podpush() { pod repo push $@ --sources=https://github.com/CocoaPods/Specs.git,192.168.0.100/CocoaPods/Specs.git; }

```

使用方式

``` bash

podlint lib

podlint spec

podpush pod.spec

```


