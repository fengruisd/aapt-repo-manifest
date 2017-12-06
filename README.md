# aapt-repo

查看cmake构建脚本请转移至项目 [https://github.com/lizhangqu/aapt-cmake-buildscript](https://github.com/lizhangqu/aapt-cmake-buildscript)

创建大小写敏感磁盘

```
hdiutil create -volname "aapt" -type SPARSE -fs 'Case-sensitive Journaled HFS+' -size 10g aapt.dmg
```

挂载

```
hdiutil attach aapt.dmg.sparseimage -mountpoint /Volumes/aapt
```

卸载

```
hdiutil detach /Volumes/aapt
```

安装repo

```
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

初始化repo项目

```
cd /Volumes/aapt
#如果存在repo bundle下载不下来的情况，请使用下面的命令进行手动clone
#git clone http://mirrors.ustc.edu.cn/aosp/git-repo.git/ .repo/repo
#初始化并同步源码树，约3G
repo init -u git@github.com:lizhangqu/aapt-repo.git
repo sync -j8
```

执行构建，构建过程中发生错误请自行根据提示安装对应的依赖库

```
cd /Volumes/aapt
cmake -H"./" -B"./build-cmake" 
cmake --build "./build-cmake" --target aapt
cmake --build "./build-cmake" --target aapt2
```
