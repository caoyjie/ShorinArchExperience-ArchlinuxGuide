
- 和 Windows 共用 EFI 分区时

  [(重制)彻底删除Linux卸载后的无用引导项_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV14p4y1n7rJ/?spm_id_from=333.1387.favlist.content.click)

  1. Win+X 选择磁盘管理，找到 EFI 在磁盘几的第几个分区，通常是磁盘 0 的第一个分区。

  2. Win+R 输入 `diskpart` 回车

    ```bash
    select disk 0       # 选择 EFI 分区所在磁盘
    select partition 1  # 选择 EFI 分区
    assign letter p     # 分配一个盘符
    ```

  3. 管理员运行记事本。

  4. Ctrl+S 打开保存窗口。

  5. 选择 P 盘，删除里面的 Linux 启动相关文件（通常有一个和 Linux 启动项名称相同的文件夹）。

  6. diskpart 里移除盘符

    ```bash
    remove letter p
    ```

- 单独 EFI 分区时

  [windows10删除EFI分区(绝对安全)-CSDN博客](https://blog.csdn.net/sinat_29957455/article/details/88726797)

  - 方法一：[图吧工具箱官方网站 - DIY爱好者的必备工具合集](https://www.tbtool.cn/)

    下载图吧工具箱，在磁盘工具里双击打开 DiskGenius，右键 Linux 对应分区删除，然后左上角保存。

  - 方法二：Windows 自带工具

    1. 使用 diskpart 选中 Linux 的 EFI 分区后在终端运行：

    ```bash
    SET ID=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
    ```

    2. 使用磁盘管理右键分区删除。

- 删除 NVRAM 入口

  使用 BOOTICE 这个软件的 UEFI 功能。在 UEFI 启动序列中删除你要删除的系统启动项。

## 最后：[issues](issues.md)和[附录](附录.md)
---

