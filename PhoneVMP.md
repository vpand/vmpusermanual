v1.0.0
![vpand.com](https://raw.githubusercontent.com/vpand/imgres/main/vpand.png)
[vpand.com](https://vpand.com/)
#
# <p style="text-align:center;">PhoneVMP User Manual</p>
## UltimateVMP
**UltimateVMP** (Ultimate Virtual Machine Protection), is an **arm/arm64/x86/x86_64** assembly level code virtualization encryption software for Darwin (**macOS/iOS**), **Linux** (Ubuntu/**Android**), **Windows** and other operating systems. It re-encodes the binary instructions of the target function into a private instruction format and then interprets the encoded instruction directly at run time. Unlike low-intensity code encryption such as obfuscation and shell, VMP code will not restore the original instruction throughout the whole execution process, so it can achieve high code encryption strength, greatly raising the threshold of reverse engineering, so as to achieve the purpose of protecting software assets. UltimateVMP currently supports platforms including **macOS, iOS, Linux, Android, Windows**, and supported architectures including **x86, x86_64, arm, and arm64**.

UltimateVMP includes two products. One is [ClangVMP](https://github.com/vpand/vmpusermanual/blob/main/ClangVMP.md)(based on the [Clang](https://clang.llvm.org/) compiler), it encodes **C/C++/ObjC/ObjC++/Swift**/etc.(static native programming language) function into VMP data during compilation process. The other is [PhoneVMP](https://github.com/vpand/vmpusermanual/blob/main/PhoneVMP.md), it encodes assembly instructions into VMP data from binary file(like **MachO/ELF/PE**). All of them are based on virtual processor infrastructure [UraniumVM](https://github.com/vpand/uvmsdkusermanual) from [vpand.com](https://vpand.com/). Their relationship is as following:
![relationship](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/relationship-1.svg)

This manual focuses on PhoneVMP.

## PhoneVMP
## Download
All of our products are hosted in [vpand.com](https://vpand.com/), you can download the assistant tool called **VPAssistant** to fetch your interested product like PhoneVMP.

Please note that you should download **the exact platform and architecture** which matches your current running OS, all the real product download through VPAssistant highly depends on the architecture that it's running on. For the native performance, you'd better not download x86_64 version on arm64 macOS even though it can directly run on it with Rosetta 2.

![vpadownload](https://raw.githubusercontent.com/vpand/imgres/main/vpadownload.jpg)
## Install
As the VPAssistant on different platform(like Windows, Linux and macOS) is **absolutely the same**, unless some feature is just available on that specified platform, otherwise all the generic feature screenshots are from macOS. Here we go.

After download, unzip and launch VPAssistant, we're gonna be in the ClangVMP tab widget, then click the **PhoneVMP** tab to activate the assistant for PhoneVMP. The default installation path is(You can **change it with the "..." button** on the right):
```
macOS/Linux : ~/VPAssistant/product

Windows     : SysDrive:\Users\user-name\VPAssistant\product
```
Every time when VPAssistant finishes launching, at the end of logs there'll be a line for your running OS triple: os-arch-hwid. It's the key to authenticate your computer to fetch a valid PhoneVMP license, copy and send to us before you want to purchase and install a license.
```
current host hwid: mac-arm64-01ac2ad20eeca7b90f408d6be2275192
```
![vpaclangvmp](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/vpaclangvmp.jpg)
![vpaphonevmp](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/vpaphonevmp.png)
## VMP Configuration
### VMPStudio
### JSON
## Raw vs PhoneVMP
### Raw
### PhoneVMP
## Trial version
## Licensed version
If you want to upgrade to a licensed version, here's the steps:
 * 1. Contact us to pay for your license;
```
The price of PhoneVMP: 5000$/year/os-arch/license
```
 * 2. Send your computer os-arch-hwid(copy from VPAssistant startup log) to us;
```
22:53:37 I : VP Assistant v1.1.2 (Apr 19 2024), current host hwid: mac-arm64-01ac2ad20eeca7b90f408d6be2275192 .
```
 * 3. Switch to VPAssistant License tab widget, click Install button to download and install the license file;

![phonevmplicense](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/phonevmplicense.png)

## Contact us
### Email
If you have any questions or problems on our products or services, feel free to contact us via email at anytime: 
 * **neoliu2011@gmail.com**
### We-Media
Till now, we-media is our main operation method, you can also contact us via the following platforms:
 * [Facebook](https://www.facebook.com/people/Jesse-Liu/61555693542797/)
 * [YouTube](https://www.youtube.com/@JesseVPAND/)
 * [Reddit](https://www.reddit.com/user/JesseVPAND/)
 * [TikTok](https://www.tiktok.com/@jessevpand/)
 * [Instagram](https://www.instagram.com/jessevpand/)

## FAQ
### Does PhoneVMP support Windows or Linux?
In fact, we have finished the development of Windows-PE and Linux-ELF supporting. But we think ClangVMP is much better for desktop platform, so we haven't released it to current PhoneVMP version. If you do need this kind of feature, please let us know.

### What's the price of PhoneVMP license ? Could the license be purchased by quarter or month? 
The price of PhoneVMP is **5000$/year/os-arch/license**, os means **Andoid/iOS/macOS**, arch means **x86/x86_64/arm/arm64**.You can visit [vpand.com](https://vpand.com/) to check the latest price policy, all of our products are sold at expressly marked price, and the license term is by year. So till now, quarterly or monthly purchasing is not supported.

### When the license is expired, can the code virtualized before run normally?
Yes, of course, the license is for PhoneVMP tool itself, it has no effect on the virtualized code.

### Can I update the license to rebind a new computer?
In principle, this is not supported. Because all of our license are offline type, it'll never connect to our server to check the license status. So if a license is released, it can not be repealed. This is good for client, as many clients are worried about data leakage. In order to avoid data leakage, offline license is the one and only choice, because we'll never read 1 byte data for our server to check what we need.
