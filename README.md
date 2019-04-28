# 黑苹果 四叶草 for AMD Ryzen系列 与 FX系列

##不需替换内核、可用FaceTime/iMessage、直接升级！

前几天我写了一篇文章，借助KVM，能让Ryzen处理器不破解内核就用上iMessage和FaceTime，传送门：[AMD Ryzen黑苹果新姿势：借助KVM实现CPU变频、随意升级](https://www.itmanbu.com/ryzen-hackintosh-using-kvm-proxmox.html) 但是KVM也有一个明显的缺陷，就是无法充分压榨机器的性能。

那么对于传统替换内核的方案，有没有更好的解决方案？相信大家都见到过Clover的KernelToPatch功能，它的功能就是动态给内核打补丁。能不能像KextsToPatch那样，“无伤”的修改内核？

结果这两天就发现了一个神器：[https://github.com/AMD-OSX/AMD_Vanilla](https://github.com/AMD-OSX/AMD_Vanilla)，该Repo做到了使用动态内核补丁功能，AMD处理器（FX系列与Ryzen系列）都不再需要替换prelinkedkernel，也不需要替换kernel。

经过我自己的体验，能够直接安装10.14.1的原版系统，并且在APP Store中直接升级到了10.14.4。整个过程丝滑流畅，非常美妙。

# 硬件配置

## 硬件1：

- 主板：华擎 太极系列 Asrock Taichi x370
- CPU：AMD Ryzen 7 1700x
- 显卡：蓝宝石 白金版 Sapphire Nitro+ RX570 4G
- 内存：科赋 雷霆系列KLEVV BOLT 16G 3000@2933MHz + 海盗船 复仇者系列Corsair LPX 16G 3000@2933MHz
- SSD：阿斯加德Asgard AN 256G
- 电源：安钛克Antec AP500

## 硬件2：

- 主板：技嘉 Gigabyte GA-780T-D3L
- CPU：AMD FX6300
- 显卡：小影霸 GT440 512M
- 内存：8G+4G DDR3 1600
- 硬盘：西部数据500G机械硬盘
- 电源：不知名250W

# 使用说明

## 详细说明：

这里：[https://hack.slim.ovh](https://hack.slim.ovh/)

在amd-osx.com上的教程还需要替换prelinkedkernel，但我测试并不需要。

## 简略教程：

1. 制作macOS启动盘：参照[黑果小兵的部落阁](https://blog.daliansky.net)

2. 挂载U盘的EFI分区，将本REPO的内容复制进去。

3. 像白果一样装系统。

## FX系列特殊说明：

Ryzen系列的主板都支持UEFI方式启动，因此不管如何制作启动盘，都是可以启动的。

但是FX系列很多主板，比如我的GA-780T-D3L都不支持UEFI启动，此时推荐使用[Boot Disk Utility](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)来制作启动盘。它的使用方式略复杂，建议参照上面的详细说明来操作。

# 优缺点分析

## 优点：

### 1. 性能强悍：

以GeekBench跑分为例

裸机安装macOS：https://browser.geekbench.com/v4/cpu/12935915

单核：5113     多核：33311

非常恐怖的分数，我非常怀疑GeekBench在macOS下有“魔法”加成。

裸机安装Windows：https://browser.geekbench.com/v4/cpu/12893803

单核：4503     多核：26849

KVM安装macOS：https://browser.geekbench.com/v4/cpu/12893704

单核：4413     多核：27114

因此，追求极致macOS性能的童鞋们可以行动起来了！

### 2. 由于系统内核与驱动文件均完整，iMessage与FaceTime也可以激活。

### 3. 可以直接在App Store下升级系统。

### 4. 你甚至可以完全开启系统完整性保护功能，安全性与白果无异。

## 缺点：

由于其本质仍然是对内核打补丁，所以：

1. PhotoShop等专业软件仍无法运行——不过大多数专业软件都已经有解决方案了。

2. 所有需要用到虚拟化的地方，例如Docker、VMware、Parallels Desktop均无法运行。因为Mac只使用Intel处理器，所以Mac下的虚拟化软件都只支持Intel VT-x。如果Mac下有支持AMD SVM的软件，自然也是可以运行的。

对于我自己来说，由于不需要用FCPX、AE这种巨型软件，倒是需要用到Docker和虚拟机，所以无疑还是KVM的方案更适合我。

# 致谢

- [Apple](https://www.apple.com)：研发的 macOS 系统
- [Clover EFI bootloader](https://sourceforge.net/projects/cloverefiboot/)：强大的通用操作系统引导器
- @[**vit9696**](https://github.com/vit9696)：制作 Lilu & AppleALC
- @[**XLNC**](https://github.com/XLNCs) & @[**Shaneee92**](https://github.com/Shaneee92)：对macOS内核(XNU)做出的卓越的研究，使得破解内核安装AMD成为可能
- @[**AlGreyy**](https://github.com/AlGreyy)：对AMD使用Clover的KernelToPatch功能的研究与使用
- @[**Aamir Farooq**](https://github.com/SlimShadyIAm/)：整合以上资源制作Vanilla AMD安装教程
- [远景论坛](http://bbs.pcbeta.com) & [AMD-OSX](https://www.amd-osx.com) & [InsanelyMac](http://www.insanelymac.com)：提供交流的场所
