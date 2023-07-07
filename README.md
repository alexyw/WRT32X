# WRT32X双分区都是openwrt情况下刷回Linksys原厂固件

Linksys WRT32X机器很不错，但如果双分区都不小心刷成了openwrt，想直接利用原厂固件刷回原厂心是不能成功的。

经各种分析琢磨，给大家介绍一个超级简单的办法

1.下载flat-FW_WRT32X_1.0.180404.58.7z，解压后通过scp协议上传到路由器，文件路径假设为/tmp/flat.img

2.SSH进入openwrt，输入命令确定当前系统分区: fw_printenv -n boot_part

3.如果上面显示1，那就接着输入命令：mtd -e kernel2 -r write /tmp/flat.img kernel2 ,如果上面显示2，命令为：mtd -e kernel1 -r write /tmp/flat.img kernel1

4.命令执行完后系统会重启，正常重启后再次SSH进入，假如当前分区为1，输入命令：fw_setenv boot_part 2 && reboot

5.搞定，现在你已经进入原厂系统了
