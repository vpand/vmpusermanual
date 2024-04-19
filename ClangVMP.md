# ClangVMP
**ClangVMP** is a [Clang/LLVM](https://clang.llvm.org/) based code virtualized compiler. It encodes **C/C++/ObjC**/ObjC++/Swift/etc.(static native programming language) function into its private VMP data during compilation process. The VMP data will be directly interpreted by ClangVMP runtime library without restoring the original instructions. Because of this mechanism, reverse engineering on this kind of code will be much more harder than raw machine code.

Till now, ClangVMP supports running on **macOS, Windows and Linux**. The following is a sample for version output on macOS installed to Xcode toolchain directory:
```shell
ClangVMP@vpand.com bin % ls -l
total 352320
lrwxr-xr-x  1 vpand  wheel         9 Apr  8 08:22 clang -> clang-vmp
lrwxr-xr-x  1 vpand  wheel         9 Apr  8 08:22 clang++ -> clang-vmp
lrwxr-xr-x  1 vpand  wheel        13 Apr  8 08:22 clang++-org -> clang-vmp-org
lrwxr-xr-x  1 vpand  wheel        13 Apr  8 08:22 clang-org -> clang-vmp-org
-rwxr-xr-x  1 vpand  wheel  82115424 Apr  7 22:19 clang-vmp
-rwxr-xr-x  1 vpand  wheel  98264160 Apr  7 11:47 clang-vmp-org
-rw-r--r--  1 vpand  wheel         6 Apr  7 22:19 version.txt

ClangVMP@vpand.com bin % ./clang-vmp --version
ClangVMP v1.1.0 Apr  7 2024 22:15:50, A LLVM/Clang(19.0.0git) based VMProtect Compiler.
Powered by http://yunyoo.cn/ , https://vpand.com/ .

clang version 19.0.0git (https://github.com/apple/llvm-project.git)
Target: arm64-apple-darwin23.4.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/ClangVMP.xctoolchain/usr/bin
```

## Download
All of our products are hosted in [vpand.com](https://vpand.com/), you can download the assistant tool called **VPAssistant** to fetch your interested product like ClangVMP.

Please note that you should download **the exact platform and architecture** which matches your current running OS, all the real product download through VPAssistant highly depends on the architecture that it's running on. For the native performance, you'd better not download x86_64 version on arm64 macOS even though it can directly run on it with Rosetta 2.

![vpadownload](https://raw.githubusercontent.com/vpand/imgres/main/vpadownload.jpg)
## Install
As the VPAssistant on different platform(like Windows, Linux and macOS) is **absolutely the same**, unless some feature is just available on that specified platform, otherwise all the generic feature screenshots are from macOS. Here we go.

After download, unzip and launch VPAssistant, we're gonna be in the **ClangVMP** tab widget. The default installation path is(You can **change it with the "..." button** on the right):
```
macOS/Linux : ~/VPAssistant/product

Windows     : SysDrive:\Users\user-name\VPAssistant\product
```
Every time when VPAssistant finishes launching, at the end of logs there'll be a line for your running OS triple: os-arch-hwid. It's the key to authenticate your computer to fetch a valid ClangVMP license, copy and send to us before you want to purchase and install a license.
```
current host hwid: mac-arm64-01ac2ad20eeca7b90f408d6be2275192
```
![vpaclangvmp](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/vpaclangvmp.jpg)
### Standalone
The standalone installation type is suitable for any platform, it's usually for user who likes **makefile**, **ninja** or **cmake** CLI build system. After installation, it's nothing special as the generic clang compiler but needs a clangvmp.json(The VMP configuration section has detailed description) configuration file to apply its virtualized compilation feature. 

Its bin and lib directory are as following(Windows and linux are nearly the same):
![clangvmpbin](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpbin.png)
![clangvmplib](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmplib.png)
### Visual Studio
### Xcode
The Xcode installation type will install ClangVMP as a toolchain package into Xcode.app. Its fixed installation path is:
```
/Applications/Xcode.app/Contents/Developer/Toolchains/ClangVMP.xctoolchain
```
During the installation, you'll be confirmed to input the root password to move ClangVMP toolchain to Xcode.app internal directory.

![clangvmpinstallxcode](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpinstallxcode.png)
If you enter the right root password, then everything is ready for you to apply virtualized compilation in Xcode IDE. 

![langvmpxctoolchain](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpxctoolchain.png)
### Android NDK
The Android NDK installation type will install ClangVMP into Android NDK LLVM toolchain. Before installation, you should select the llvm root directory of the target NDK toolchain manually.

![clangvmpndkroot](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpndkroot.png)
After installation, the ndk llvm toolchain directory will be as following:

![clangvmpinstallndk](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpinstallndk.png)
### Linux
## IDE Configuration
### Visual Studio
### Xcode
You can switch the Xcode and ClangVMP toolchain from main menu Xcode/Toolchains at anytime.

![clangvmpswitchtoolchain](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpswitchtoolchain.png)
## VMP Configuration
Unlike other Clang compiler-based source code encryption products such as **OLLVM**, ClangVMP doesn't specify the encryption configuration using command line arguments or attribute annotations, but instead uses a **clangvmp.json** encryption configuration file to specify the encryption options. The generic format of clangvmp.json is as following:
```json
{
    "source_name.ext" : {
        "vmpre" : ["symbol_regexpr"],
        "obfre" : ["symbol_regexpr"]
    }
}
```
During compilation, the loading rule for the clangvmp.json configuration file is:
 * Firstly, look for clangvmp.json in the folder where the input source code file is located, if found, use this configuration, otherwise go to Secondly; 
 * Secondly, look for clangvmp.json in the current working path of the compiler (for Xcode, this is the path where xcodeproj is located; for NDK, this is the parent directory of jni). 
If found, use this configuration, otherwise turn to normal compilation; 
### Key source file
### Key vmpre
### Key obfre
### Demo
## VMP vs Raw
## Trial version
## Licensed version
## Contact us
### Email
If you have any questions or problems on our products, feel free to contact us via email at anytime: 
 * **neoliu2011@gmail.com**
### We-Media
Till now, we-media is our main operation method, you can also contact us via the following platforms:
 * [Facebook](https://www.facebook.com/people/Jesse-Liu/61555693542797/)
 * [YouTube](https://www.youtube.com/@JesseVPAND/)
 * [Reddit](https://www.reddit.com/user/JesseVPAND/)
 * [TikTok](https://www.tiktok.com/@jessevpand/)
 * [Instagram](https://www.instagram.com/jessevpand/)
