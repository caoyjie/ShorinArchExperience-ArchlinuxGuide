
## 下载 ISO

去想要安装的 Linux 系统的官网下载 ISO（系统镜像）文件。官网下载慢的话可以找一找你所在地区的镜像站，主流 Linux 发行版通常会在下载页面提供镜像站链接。

- [Arch Linux](https://archlinux.org/download/)
- [CachyOS](https://cachyos.org/download/)
- [Linux Mint](https://linuxmint.com/download.php)


## 制作系统盘

>**⚠️注意备份重要数据⚠️**

- 方法一：[Ventoy（推荐）](https://www.ventoy.net/cn/index.html)

    Ventoy 制作的系统盘可以存放多个系统镜像。

- 方法二：压缩卷（没有 U 盘使用这个方法）

    1. Windows 系统内 `Win+X` 键打开菜单；选择`磁盘管理`；找到想安装 Arch Linux 的磁盘，右键，选择`压缩卷`，空出磁盘空间。

    2. 右键空出的空间选择`新增简单卷`，大小设置为 4096MB（足够装下 ISO 里面的文件就行），盘符随意，格式化选择 `FAT32`。

    3. 双击打开上一步下载的 ISO，把里面的内容粘贴进新建的盘符里。

## Windows 下的准备工作

如果你要安装双系统，以下工作是必须的。

1. 解决安装 Linux 后 Windows 时间错乱

    >[双系统时间同步-CSDN 博客](https://blog.csdn.net/zhouchen1998/article/details/108893660) | [系统时间 - Arch Linux 中文维基](https://wiki.archlinuxcn.org/wiki/%E7%B3%BB%E7%BB%9F%E6%97%B6%E9%97%B4)

    Linux 把主板时间改成标准 UTC 时间后根据系统设置的时区对 UTC 时间进行加减后显示出来。 Windows 直接读取主板时间显示出来，所以此时你 Windows 显示的时间就变成了 UTC 时间，表面上看像是 Windows 的时间错乱了。Windows 下管理员身份打开 PowerShell 运行：

    ```powershell
    Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
    ```

    <details close><summary>命令解释</summary>

    >`Reg add` 添加一个注册表项目

    >`HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation` 是路径

    >`/v RealTimeIsUniversal` `/v` 指定项目名称

    >`/t REG_DWORD` `/t` 指定数据类型为 REG_DWORD（32 位无符号整数）

    >`/d 1` `/d` 指定具体的值，1 代表启用

    上面这条命令修改注册表，让 Windows 采用和 Linux 相同的策略，默认主板时间为 UTC，根据系统设置的时区进行相应的加减后再显示。
    </details>

    另一种方法是让 Linux 使用本地时间 `timedatectl set-local-rtc 1`，我没试过，说不定会在日志、定时任务之类的地方出问题。由于我主要使用 Linux，所以使用上面的方法。

2. 关闭快速启动

    搜索 `电源` --> `选择电源计划` --> `选择电源按钮的功能` --> `更改当前不可用的设置` --> 确认关闭了 `快速启动`

3. 关闭 BitLocker

    系统设置里搜索到后关闭。BitLocker 加密会阻碍 Linux 访问硬盘。

4. 预留硬盘空间

    右键任务栏上的 Windows logo 打开磁盘管理。右键你要使用的硬盘分区，通过压缩卷腾出空间给 Linux。

## BIOS 设置

重启电脑进入 BIOS。不同的机器进 BIOS 方法不同，现代电脑通常是 `Esc`、`F2`、`F7`、`Delete`，如果不行的话查找一下自己主板进 BIOS 的方法。

1. 关闭安全启动（Secure Boot）

    > 部分发行版已支持安全启动，可以查阅官方文档。

    重启电脑进入 BIOS 关闭安全启动。

2. 关闭 TPM

    开启 TPM 可能会在 Linux 下出现异常。

3. 调整启动项顺序

    启动项第一个设置成刚刚制作的系统盘。

    >如果知道自己的快速启动项菜单的按键是什么的话可以不调整顺序

4. 保存并退出

    通常是 `F10` 键

## 下一节：[Arch Linux 安装教程](./archlinux/安装ArchLinux.md) | [Linux Mint 入门指南](./linuxmint/Linuxmint入门.md) | [CachyOS 入门指南](./cachyos/CachyOS.md)

