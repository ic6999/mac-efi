# mac-efi

【H310m+i3-8100】✔️ 
@硬件：
-核显：UHD 630/注入00009B3E/07009B3E
-声卡：ALC887/897
Layout-ID 通常用1或11
-网卡：RTL8111H/RealtekRTL8111.kext
⚙️ BIOS 设置：
-关闭：Secure Boot（安全启动）、Fast Boot（快速启动）、CSM、VT-d、CFG Lock（若找不到此项，需在 OC 中勾选 AppleCpuPmCfgLock）。
-开启：AHCI Mode（SATA 模式）、Above 4G Decoding、XHCI Hand-off。

🛠️详细步骤：
⚙️首先准备空闲磁盘空间，命名如mac以便安装时确认。
💡机械硬盘亦可。
1.构建EFI:命令行CLI工具Opcore-simplify-main自动生成配置文件及最新驱动。
⚠️图形版不可用（缺主驱动）
2.获取镜像和制度作U盘：
⚠️不能用kenmac“在线恢复版”镜像！
【OCLP下载镜像和U盘制作】
💡macos环境
①下载安装OCLP:
https://github.com/dortania/OpenCore-Legacy-Patcher/releases
②setting:model
③Create macOS Installer
选择可用镜像-download
（关闭代理！）
安装文件.app保存在：应用程序
④制作U盘：选择上面app文件写入。
⑤替换macos安装U盘EFI:
diskutil list
找到U盘EFI分区disk?
sudo diskutil mountdisk /dev/disk?
桌面出现EFI磁盘，替换第一步创建的EFI即可。
3. 从U盘安装-选择install macos... →磁盘工具→抹掉准备好的mac为APFS →重新安装macos... 重启N次
4. 安装成功后拷贝替换EFI文件夹到macos安装磁盘的ESP分区，并设置为第一启动项。
5．去除-v调试啰嗦模式：
OCAT 加载 EFI/OC/config.plist。
-NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 →boot-args替换干净的启动参数（不含 -v）如：
alcid=11 agdpmod=pikera brcl=2 debug=0 kext-dev-mode=1 -no_compat_check -wegnoegpu

@校准时间
启用网络时间
sudo systemsetup -setusingnetworktime on
设为中国时区（上海）
sudo systemsetup -settimezone Asia/Shanghai
立即强制同步（国内授时中心）
sudo sntp -sS ntp.ntsc.ac.cn
