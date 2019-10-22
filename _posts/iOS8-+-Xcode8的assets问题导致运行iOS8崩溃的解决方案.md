#### 1.问题描述：
当手机系统版本为iOS9.0以下版本时，会出现在运行项目时crash的情况，而crash的地方大多是因为图片资源
#### 2.崩溃原因
在Xcode8中，如果你的图片资源文件里有16位图或者图片显示模式为P3，并且Deployment Target是iOS9.3以下的就会出现这个问题。如果你的App需要支持wide color functionality，那你就必须设置Deployment Target为iOS9.3以上。如果你的APP不需要支持wide color functionality并且你希望兼容iOS老版本，那么你需要将所有16-bit or P3 assets的图片转换为8-bit sRGB assets
#### 3.解决方法
暴力处理所有的图片
````
#!/bin/bash
DIRECTORY=$1
echo "------------------------------"
echo "Passed Resources with xcassets folder argument is <$(pwd)>"
echo "------------------------------"
echo "Processing asset:"
XSAASSETSD="$(find "$(pwd)" -name '*.xcassets')"
for xcasset in $XSAASSETSD
do
    echo "---$xcasset"
    IMAGESETS="$(find "$xcasset" -name '*.imageset')"
    for imageset in $IMAGESETS
    do
        echo "------$imageset"
        FILES="$(find "$imageset" -name '*.png')"
        for file in $FILES 
        do
            echo "---------$file"
            sips -m "/System/Library/Colorsync/Profiles/sRGB Profile.icc" $file --out $file
        done
    done
done
echo "------------------------------"
echo "script successfully finished"
echo "------------------------------"
````
1.将以上的脚本生成一个bash.sh文件
2.将该文件放于项目当中(AppDelegate.h同一级目录下)
3.打开终端，一直cd到bash.sh的文件夹所在位置
4.终端输入命令：touch bash.sh  ▸ chmod 777 bash.sh ▸ ./bash.sh
5.完成标识如下：
![QQ20180531-173736@2x.png](https://upload-images.jianshu.io/upload_images/6941348-761daf985c7b85f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



