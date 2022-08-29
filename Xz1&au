★原帖： https://forum.xda-developers.com/xperia-xz1-compact/development/devonly-exploits-temp-root-to-backup-t3795510 
★欢迎捐助原作者： https://j4nn.github.io/donate 
★结合了：xda 用户 munted 写的 pdf 教程，原帖地址： https://forum.xda-developers.com/showpost.php?p=78255334&postcount=382 
★翻译：酷安@正好也在 ；译者所注的中文补充说明用中括号“[]”标出。 
★免责声明：刷机有风险，请谨慎操作，而且务必提前备份好手机上的资料；变砖了一般都可以救，别打我[受虐滑稽]；祝你成功！[玫瑰]

※文中提到的所有文件、本文 pdf 版教程、各机型受支持的 8.0 固件链接：https:请//cloud.删189.掉cn/t/6zAryqUF7zuy
(访问码:mxs6) [2021年4月4日更新]

为了老铁们看得明白，我们先看一下本教程的大纲框架：

# 一、	备份和恢复 TA 分区（内含 DRM 文件）
## 0、简介 
刷过大法机器的酷友们应该都知道，索尼手机想要解锁 bootloader 就要承受 DRM 文件被清除的后果，而这样就会让一些很重要的功能丢失，其中最恼人的就是相机直出的图片纯绿[流汗滑稽]（Android Oreo 测试结果）。以往，前几代机型的解锁大多需要靠 TA 分区备份才能使 DRM 文件得以被导出和恢复。一年多前，XDA 大神 j4nn 开发出了一套工具，可以用来备份 XZ1/XZP/XZ1C 机型的整个 TA 分区（Trim　Area　Partition），能够实现访问索尼 DRM keys 的device master key，以及在 bootloader 解锁后恢复 TA 分区。有了这个工具，相机等重要功能就又能在任一索尼原生固件上正常工作了。[牛啤][牛啤]

由于这套工具的原理是利用几个 Android 8.0 版本的特定固件才存在的漏洞，所以为了能够正常使用本套工具，我们需要刷入如下受支持的固件。当然如果老铁们的手机恰好正运行这这些固件版本之一，那再幸运不过了。
[不过在 j4nn 的另一篇帖子中，他指出降级固件可能导致 Android Attest Key 的参数状态发生改变（PROVISIONED→NOT PROVISIONED），目前该改变可能带来的影响未知。（链接： https://forum.xda-developers.com/xperia-xz1-compact/help/android-attest-key-lost-bootloader-t3829945 ）楼主的手机这一项本来就是 NOT 的[受虐滑稽]，就没管它。]
请注意，表 2 中的 root 攻击工具（即所有的renoroot 工具）仅适用于表 1 提到的固件版本（相应的二进制内核 builds 版本号）。其他机型、或其他内核版本都不可能可用——请不要尝试，不会好使的[受虐滑稽]。

[★此处提到的 root 攻击工具、以及后面说的临时 root shell 与大众意义上的手机 Root 没有关系，只把它当作卡 bug 的工具就好。下文解锁后通过 Magisk 才能获得可靠稳定的手机 Root 状态。]

可能有的执着老铁还想问，这套工具能否往其他固件版本或其他机型移植/适配呢？工具本身是依靠的是某内核下未修复的几个漏洞，主要漏洞是 CVE-2017-7533，这个漏洞随后就被谷歌打补丁修复了（2017-12-05 安全补丁程序级别，参见 https://source.android.com/security/bulletin/2017-12-01 ）。这就意味着我们只能刷入一个含有较早的安全补丁的固件。想方设法把这套工具适配给新的机型或固件（比如说XZ2 Compact）是没有意义的 [XZ2 发布时间压根没赶上那个漏洞，好像谷歌给堵死了之后 XZ2 才发布，所以根本没有降级回滚卡 bug 这条路[受虐滑稽][喝酒]]。

## 【建议：在一切刷写操作之前，请开启开发者选项菜单里的「OEM解锁」选项。如果是跨机型刷固件，请不要刷写 bootloader，您需要在运行 newflasher 开始刷机前彻底移除 boot 文件夹里的文件。】 
请老铁们遵循如下官方最新操作指南。如果一些内容写的不是很明白，老铁们可以查看用户munted 制作的 pdf 指南（文章开头有），内含更多细节、截图以及 Windows 环境下的一些辅助指导。

## 1、	备份想保留的手机资料，因为所有用户数据都将被清除。
推荐使用 Xperia Transfer Mobile、 http://www.coolapk.com/apk/net.donething.android.privbackup 。除了完成许多软件自带的账户同步、通话记录短信联系人、聊天记录、文档图片音视频录音备份，月度数据用量、闹钟列表、浏览器标签页和书签也可以截图记录。建议在刷机之前就做一次恢复出厂设置，这样可以解绑 Google 账户，这样做的好处是刷完机之后，如果没插 sim 卡、跳过 WiFi 连接配置，就可以避免 Google 的强制联网（验证）或账户登入。[建议刷机前在设置里把手机锁屏、PIN 密码都取消了，不然后续很麻烦。]

## 2、	刷入受支持的固件
按照上面的表 1 下载自己机型对应的固件，之后参照此帖 https://www.coolapk.com/feed/16717137 刷机，刷完我等你回来进入下一步。
[*可选] j4nn 建议，在刷机前截一张 Security 信息的图，并把它备份到电脑或其他设备 [电话拨号键盘输入*#*#7378423#*#*进入Service Menu→Service tests→Security；安卓 9 的手机在 Service info 里找；如果键盘输入没反应请到设定将预设电话应用程序改为系统自带电话应用][译者全程截了但感觉没什么用[doge笑哭][流汗滑稽]这一步如果老铁们对自己的操作很有信心，此处及后面让截 Security 信息的步骤可以不做]

## 3、	为 renoroot 准备环境 
(1) 刷完降级固件开机之后，不要连网（方法：选择仅 WiFi→不进行配置），跳过账户登入。 
尽快完成设置向导，什么推荐都点取消或者不要，之后关掉WiFi，移动数据，以避免收到和下载系统更新。 
(2) 同时，到「设定」里的「系统」「软件更新」点击右上角三个点「设置」，把「自动下载系统更新」和「自动更新应用程序」都设成关闭。以此取消应用和系统的自动更新。 
在设置里面把主题从动态背景改成一个静态的。 
(3)「设定」「系统」「关于手机」连续点击7次版本号码，以激活开发者模式。 
(4) 返回到「设定」下的「系统」菜单，前往「开发人员选项」，开启「USB调试/USB偵錯/USB Debugging」，关掉「通过USB验证应用程序」，打开「不锁定屏幕/Stay awake/熒幕不休眠」。准备视频我会上传至网盘。 
(5)[可选] 拨号键盘输入*#*#7378423#*#*，去 Service tests 里再次截一张 Security 信息的图，并把它备份到电脑或其他设备。 
(6) 再次确保 WiFi 和移动数据连接关掉了，不要让后台有任何的数据连接。 
(7) 不关机，通过数据线连接到电脑，不安装Xperia Companion，选择「传输文件」。环境准备工作到此结束。

## 4、	配置工具 
(1)下载并解压 renoroot.zip。
(2)现在，我们需要再下载一个 ADB 开发工具，把所有文件解压到 renoroot 所在文件夹。
(3)下载 ADB 工具所需的驱动 [在网盘中“各机型 ADB 驱动”文件夹]，解压到一个文件夹。 
(4)手机开机连接电脑。在设备管理器中找到一个叫「ADB Interface」的感叹号设备，
双击之，更新驱动，选择「这台电脑上的文件夹」，选择驱动解压到的文件夹，
下一步确定，显示已成功安装驱动。

(5)这时在手机上会弹出「允许 USB 调试吗」的问询框，当然要允许了，记得勾选上「信任这台电脑」。 
(6)在 renoroot 文件夹里按住 Shift 键不放同时右击鼠标，选择「在此处打开 Powershell 窗口」[也可以 CMD 命令提示符用 cd 命令定位到这个文件夹操作，去掉以下每条命令的「.\」就好]

## 5、	执行命令以安装 apk 程序并获取临时 root shell 
(1)使用下面的 adb 命令来把工具传入手机 [要一条一条地复制粘贴按回车，不要一股脑都整进去，电脑会懵的[受虐滑稽]；下同] 
代码： 
.\adb push renoroot /data/local/tmp 
.\adb push renoshell /data/local/tmp 
.\adb push renosploit /data/local/tmp 
.\adb install -r renotrap.apk 
如图

(2)下面的步骤意思是启动工具，以获取临时root shell，这里我们需要使用使用 adb shell 命令行终端 
代码： 
.\adb shell

(3)使用 Powershell 命令窗口的老铁们请注意，下面的代码前面不用加「.\」了。 
代码： 
cd /data/local/tmp 
chmod 755 reno* 
./renoroot
上面最后一个命令将开始攻击漏洞，一旦我们看到命令窗口的光标前有＃号时，就表示获取临时 root shell 成功了。如下图。
而这一过程中，手机会出现 renotrap 应用程序的界面。等那些 events 跑完大约需要15分钟。 
因为程序内所进行的覆写操作有可能没有击中所需的成形堆对象 [我也不知道啥意思，这句话机翻的[流汗滑稽]]，此时手机可能会重启。（手机开机后，您可能需要等待加载几分钟，因为初次启动过程耗时较长。参见网盘里的视频）
(4)只要电脑窗口出现＃号那么就可以直接略过此步进入第 ##6 大步。但如果还没等电脑窗口出现＃号，手机就在这一过程中重启，那么我们需要再次把这第 5 大步的命令敲一遍，即从 
.\adb push renoroot /data/local/tmp 这行代码开始，一直到手机上的 renotrap 程序再跑一遍 events。
等到命令窗口光标前再次出现#号时，就说明我们完成了 temp root。
而手机上应该如图所示：
接下来进入第 6 步。

## 6、	备份 TA 分区 
(1)接下来，我们就可以在 root shell 里用如下命令备份 TA 分区了： 
代码： 
cd /data/local/tmp 
dd if=/dev/block/bootdevice/by-name/TA of=TA-locked.img 
chown shell:shell TA-locked.img 
sync 
sync
如图所示：
(2)不要关闭这个命令提示窗口，再在 renoroot 文件夹内按住 Shift 并右键开启一个 Powershell 窗口或 CMD 窗口，输入如下命令并回车， 
代码： 
.\adb pull /data/local/tmp/TA-locked.img

(3)上步这条命令的作用是读取 TA 分区文件，并把它传输到电脑上。这时我们应该在 renoroot 文件夹里发现多了一个 TA-locked.img 文件。
这个文件非常重要，没有它解锁 bl 后手机拍照就好不了了，务必备份多处，C 盘一个 D 盘一个，给自己邮箱发一个，云盘里再存一个，谨防丢失。

## 7、	使用索尼提供的解锁码来解锁 bootloader 
索尼官方在 https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader/how-to-unlock-bootloader 给出了解锁步骤，下面我们将遵循索尼网站上的说明进行解锁 Bootloader 操作。 
※请注意：解锁 bootloader 操作不可逆，重新上锁 bootloader 是不可能的（恢复 TA-locked 并不能使 bootloader 重新上锁），而以后的日子每次开机时警告屏都将伴君左右，请做好心理准备。
(0)再次强调，解 bootloader 前一定要确保 TA-locked.img 文件已经成功被导出到电脑上。解锁操作会清除手机数据。 
(1)去开发者选项里检查手机「OEM 解锁」状态。手机里如果「OEM 解锁」选项是灰的，无法将其开启，那么我们需要能够连接到 Google 一次。之后就会发现这个可以打开了。(网盘有视频)
(2)检查手机是否允许解锁 Bootloader。电话拨号键盘输入*#*#7378423#*#*进入Service Menu→Service info→Configuration→Root Status，只有里面的 Bootloader unlock allowed 这一项显示的是「Yes」才可以解锁[皱眉][如果键盘输入没反应请到设定将预设电话应用程序改为系统自带电话应用]
[*可选] 应该不用安装 google usb driver，如果老铁们照下面解锁步骤操作后不能识别 fastboot devices 或者怎样，那么可以尝试安装，即网盘里的 usb_driver_r12_windows.zip 文件。
(3)下载 Flashtool-drivers.exe，在 win10 环境下，我们需要进设置→更新和安全→恢复→高级启动-立即重新启动，然后选择「疑难解答」→高级选项→启动设置→重启→「7) 禁用驱动程序强制签名」，然后找到下载好的 Flashtool-drivers.exe，双击安装；在 win7 中下载好直接运行就行，建议右键管理员模式运行。
(4)只勾选「Fastboot Drivers」即可。
(5)点击「Install」安装，win7 将出现下图，选择无论如何仍要安装，然后确保最后状态符合下图，所安装的驱动状态是绿色的✅。
(6)马上要解锁了老铁们，解锁会自动恢复出厂设置，请确保备份好资料。手机关机，按住「音量+」，连接到电脑，看到手机 LED 灯变蓝且听到电脑噔当啷噔的提示音后我们进入下一步。
(7)回到 renoroot文件夹，shift+右键 新建一个 powershell 窗口，输入代码：
.\fastboot devices
如上图，输入并回车之后会出现一行 BH 开头的代码，这个是连接的手机；如果什么都没显示，那么设备就没有成功进入 Fastboot 模式，请关机重连再试一次。
(8)前往 https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader/#unlock-code ，通过输入手机 IMEI，获取解锁码。这一过程会涉及到 recapcha 人机验证，可能需要外网环境。
(9)老铁们，呃 shuī 然不是同一时间，但是呢是同一电脑，拿到解锁码后，在 fastboot 这个命令窗口中输入
.\fastboot -i 0x0fce oem unlock 0x解锁码

把「解锁码」三个字换成获取的解锁码，回车，嗷利给，干了！如图：
诶放错了应该是这个[流汗滑稽][受虐滑稽]：
解锁操作结束会提示 OKAY。手机应该会自动恢复出厂设置。 
(10)在解锁 bootloader 之后，先不要刷入任何固件。开机进入当前系统就好。这次开机就又出现了设置向导，和之前一样，断网开飞行模式，进入设定→系统→关于手机→连击 7 次版本号激活开发者模式，返回「系统」设置列表，在「开发者选项」中打开「USB 调试/偵錯/Debugging」，关掉「通过 USB 验证应用」，打开「保持唤醒/熒幕不休眠/Stay Awake」。
Bootloader 的解锁，标志着 TA 分区的损坏。随后我们将恢复 TA 文件。

## 8、	再次使用临时 root 以恢复 TA 
(1)在电脑上重复第##5大步的(1)~(4)，怕超字数，这里我们用图片：
总之，完事后我们会发现在命令窗口的最后一行出现了一个#号；在这一过程中，xda 热心网友 munted 花了 30 分钟，手机上显示 51370 events 和 1 overwrites，老铁们可以参考一下。

(2)一旦命令窗口最后一行出现 # 号，我们就可以进入下一步。这时我们先备份一下当前的解锁了的 TA 分区，因为可能以后要用。随后，我们将恢复 TA，使它回到最最开始的状态。这里将用到的命令仍是 adb push。

代码： 
cd /data/local/tmp 
dd if=/dev/block/bootdevice/by-name/TA of=TA-unlocked.img 
chown shell:shell TA-unlocked.img 
sync 
sync

(3)接下来把 unlock 的 TA 文件读取出来传送到电脑上，然后把之前备份的 TA-locked.img 运回手机。在 renoroot 文件夹里新开一个Powershell 窗口进行操作，同时不要退出 renoroot 的命令窗口。

代码： 
.\adb pull /data/local/tmp/TA-unlocked.img 
.\adb push TA-locked.img /data/local/tmp
(4)接着，在 renoroot 的 Powershell 窗口里，使用 renoshell 恢复 TA：

代码： 
cd /data/local/tmp 
dd if=TA-locked.img of=/dev/block/bootdevice/by-name/TA 
sync 
sync 
如图所示
至此，TA 分区备份/恢复和 Bootloader 解锁步骤结束。

##9、	开机至当前系统，看一下相机好不好使。 
[可选:] 同样这个时候给 Security 截个屏，把截图传到电脑上。

# 二、玩机时间 
## 10、	刷入最新的官方固件 
[如果老铁们想继续使用官方固件，或者使用基于官方固件的修改包，那么可以按照其说明刷入官方固件。有些第三方包比如「LineageOS 17.1 for Sony Xperia XZ1」，明确提到「REQUIRED FIRMWARE: 47.2.A.11.228」，那么就是说我们还是要事先刷入最新索尼官方固件。 
这里我们继续使用 newflasher，参照 https://www.coolapk.com/feed/16717137 此帖操作。]

## 11、	刷入 TWRP Recovery 
(1)将 twrp 文件放在 renoroot 的文件夹内，然后再在该文件夹按住 shift 键同时右击鼠标，选择「在此处打开 Powershell 窗口」， 
(2)手机关机状态下一边按住「音量加」键一边连上电脑，直到手机 LED 灯 蓝了，电脑出现噔噔啷噔的 USB 连接音。
(3)然后在 Powershell 窗口输入：

.\fastboot devices 
回车，如果连接成功会显示已连接的设备。接着输入

.\fastboot flash recovery twrp-3.3.1-0-poplar.img 
（文件名视机型对应的twrp文件名而定）
如图，如果显示 OKAY 那就妥了。

## 12、	刷入 Magisk 
老铁们，激动人心的搞机时刻终于到来了！ 
(1)先进入刚刚刷入的 TWRP。怎么进入？关机状态下，同时按住「电源」键和「音量键」，待手机震动一下的时候松开电源键，直到显示twrp 图标就可以松手了。 
(2)在 TWRP 里可以先选 Wipe 按照预设好的模式清除数据，也可以直接安装，先在主界面选择 Mount 挂载，此时连接电脑应该可以直接往手机里复制 Magisk 的包。放到手机里之后，在 TWRP 主界面 Install 安装，浏览选择 Magisk 文件刷入即可。
(3)刷入后可以按提示清除 Cache 等文件，也可以直接重启至系统。

————————

★原帖中关于继续接收 (F)OTA 固件更新、伪装成未解锁前的状态这些部分我没有翻译（因为没看懂，而且有风险）感兴趣的老铁们可以去原帖了解一下。 
★开机后跳过谷歌验证：TWRP 里选 Advanced (高级)→Terminal (终端命令)，输入 dd if=/dev/zero of=/dev/block/bootdevice/by-name/frp，注意命令中的空格，然后确定，重启至系统。 
★如果进入 TWRP 就让输入密码，那是因为之前没有关闭手机 PIN 密码锁，输入解锁密码就行。如果密码错了或是选择 Cancel 取消，那么一会儿选择安装文件的时候你会发现文件都变成了乱码，这需要重新进入 TWRP。

教程到此结束，祝您愉快。

请不要将此内容用作商业用途。 
酷安@正好也在 编辑于 2020 年 2 月 24 日。
于 2021 年 4 月 4 日对第 ##5 (3) 步、第 ##8 步和文件链接进行了更正或替换。
#玩机技巧# #刷机# #索尼#
