# Nokia N1 B19 ROOT 教程

​																					*By sukanka*

---

**Note: ROOT 教程对A5CNB19 无效,执行步骤之后没有 ROOT. ** 只能使用 ivoyroot 的方法获取临时root. 参见 [这里](https://github.com/jemyzhang/iovyroot/tree/nokia-n1) 

也有其他方法ROOT, 参见百度贴吧. 图片载入出了问题, 以后修正. 

## 文件下载

所有文件可从 链接: https://pan.baidu.com/s/1KTmXyjIgBHd0AY3X7YTpXw 提取码: 2333 下载到 (我不会使用 glf) , 该连接比本文多两个大文件.

| 文件               | 说明         |
| ------------------ | ------------ |
| A5CNB19_update.zip | A5CNB19 固件 |
| A5FMB19_update.zip | A5FMB19 固件 |



## 文件说明

| 文件                               | 说明                         |
| ---------------------------------- | ---------------------------- |
| boot-cnb19.img                     | A5CNB19 固件的 boot 文件     |
| boot-fmb19.img                     | A5FMB19 固件的 boot 文件     |
| LICENSE                            | MIT 许可证文件               |
| Magisk-v18.1.zip                   | Magisk18.1, 用于 Root        |
| n1_twrp3.0_rec.img                 | 网友编译的 3.0 的 twrp, 英文 |
| platform-tools_r28.0.1-windows.zip | ADB 驱动文件                 |
| README.md                          | 本文件                       |
| recovery-cnb19.img                 | A5CNB19 固件的 recovery 文件 |
| recovery-fmb19.img                 | A5FMB19 固件的 recovery 文件 |
| twrp2.8.7.1-nokia-n1.img           | 网友编译的 2.8 的 twrp, 英文 |
| twrp2.8.7.1-nokia-n1-zh.img        | 网友编译的 2.8 的 twrp, 中文 |
| Images                             | 用于存放本文图片的文件夹     |



## 前期准备

1. 在设置>关于平板电脑 连点5次版本号,启动开发者选项

![img](file:///C:/Users/suhan/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

2. 在开发者选项打开OEM 解锁和USB 调试.

![img](file:///C:/Users/suhan/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

3. 准备好需要的资料.

![img](file:///C:/Users/suhan/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

A5CNB19 是大陆B19包, A5FMB19 是台版, Magisk-18.1.zip 是ROOT 的工具. 最后的两个recovery 也是同理. n1_twrp_rec.img 是twrp 的recovery. 下载你需要的东西,通常需要一个固件(B19), 对应的 recovery, 以及 twrp 的rec, Magisk-18.1.zip. 其中 Magisk 的安装包可以在XDA 下载到.

4. 设置好ADB工具.

使用 `platform-tools.zip` 中的文件更新你的 `adb` 到最新版, 最新版的 `platform-tools` 可以在 [Android Developers](https://developer.android.com/studio/releases/platform-tools) 下载到, 本文仅提供 windows 版, 其他版本请到 [Android Developers](https://developer.android.com/studio/releases/platform-tools)  下载.

你可以打开 Powershell 输入 `adb version` 查看当前的 `adb` 版本, 

![1550334251915](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334251915.png)

如果你输入过后报错,说明你没有将 adb 添加到系统环境变量, 按如下步骤将它添加到系统环境变量:

* 将 `platform-tools.zip` 的文件解压到一个你喜欢的文件夹,例如 `C:\Android`

![1550334443564](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334443564.png)

* 用小娜搜索系统环境变量,进入
* ![1550334505458](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334505458.png)
* 选择环境变量

![1550334540565](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334540565.png)

* 选择**系统变量**的 `Path` 选择编辑

![1550334621569](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334621569.png)

* 选择**新建**, 输入你的存放 adb 文件的文件夹, 比如我的 `C:\Android` ,一路点击确定,直到退出.

![1550334677703](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550334677703.png)

* 再次尝试 ` adb version` 命令.

## 基本步骤

下面是基本步骤

1. 进入bootloader, 解锁
2. 将你需要的ROM 的recovery 刷入 boot 分区, 正常重启, 进入recovery 分区,使用sideload 刷入需要的ROM.
3. 重启
4. 将 Magisk , 对应的boot.img文件以及twrp_rec 复制到N1.
5. 重启到bootloader
6. 将twrp_rec 刷入 boot 分区
7. 在twrp 中刷入boot.img 到boot分区, 再刷入 Magisk
8. 重启, 完毕!

## 详细步骤(以刷A5CNB19为例)

我想从 A5FMB19 刷到 A5CNB19 并且我已经解锁了,如果你没有解锁, 你需要先将N1连接到电脑,然后打开 Powershell (或者Cmd), 输入 

```
adb reboot bootloader
```

重启到 bootloader

![1550154019971](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550154019971.png)

由于我的已经解锁,因此显示 `DEVICE STATE - unlocked. 如果你的显示 locked, 你需要先输入 

```
fastboot oem unlock
```

注意解锁会失去所有数据!

然后将  recovery 刷入到 boot 分区, 提示, 可直接将 recovery 拖到 powershell 中 

```
fastboot flash  boot recovery-cnb19.img
```

![1550155476110](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550155476110.png)

然后按电源键启动, 看到 Start 界面再次按电源键开机, 然后看到倒地的机器人, 同时按一下电源键和音量加。看到这个界面，按音量减键选择第二项 apply update from ADB， 然后按音量加确认

在电脑端输入

```
adb sideload A5CNB19_update.zip
```

![1550156134665](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550156134665.png)

等到 100% 就会自己重启，就好了。完成了是这样的

![1550156569994](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550156569994.png)

然后重启到系统，把其他东西(boot, Magisk, twrp_rec) 复制到 N1，我把这些都复制过去了。

![Screenshot_2019-02-14-23-14-08](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-23-14-08.png)

然后重启到 bootloader， 刷入 twrp_rec.

```
fastboot flash  boot n1_twrp_rec.img
```

![1550157604099](C:\Users\suhan\AppData\Roaming\Typora\typora-user-images\1550157604099.png)

然后重启， 在Start 界面按下电源键， 进入 twrp

![Screenshot_2019-02-14-09-24-42](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-24-42.png)

将最下面的滑块滑到最右边， 进入主菜单，

![Screenshot_2019-02-14-09-21-19](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-21-19.png)

选择 `INSTALL` 再选择你存放资料的文件夹，选择 `Install Image`

![Screenshot_2019-02-14-09-22-35](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-22-35.png)

![Screenshot_2019-02-14-09-22-42](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-22-42.png)

刷入 boot, 选择刷入到boot 分区,滑块滑到最右边

![Screenshot_2019-02-14-09-23-08](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-23-08.png)

![Screenshot_2019-02-14-09-23-17](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-23-17.png)

再返回那个文件夹，选择 Install Zip, 安装Magisk，

![Screenshot_2019-02-14-09-22-35](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-22-35.png)

滑块滑到最右边，

![Screenshot_2019-02-14-09-24-42](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-24-42.png)



刷完先 Wipe cache/dalvik, 滑动滑块确认。之后直接重启， 选择Reboot System. 在Start 界面按下电源键， 开机！![Screenshot_2019-02-14-09-25-24](D:\Users\suhan\Pictures\Camera Roll\Screenshot_2019-02-14-09-25-24.png)

## 致谢

首先感谢所有为 Nokia N1 root 而努力的人们.

以下是资料的来源(顺序不代表重要程度)

1. 百度贴吧 @850935381的帖子 [国行cnb19救砖工具](http://c.tieba.baidu.com/p/5072783903?fr=good) 获得国行 B19 的recovery
2. 从XDA 获得 Magisk-v18.1.zip [来源点此处](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445) 
3. 其他资源获得的时间太早, 来源记不清了. 在此鸣谢