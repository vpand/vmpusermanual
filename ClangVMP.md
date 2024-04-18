# ClangVMP
**ClangVMP** is a [Clang/LLVM](https://clang.llvm.org/) based code virtualized compiler. It encodes C/C++/ObjC/ObjC++/Swift/etc.(static native programming language) function into its private VMP data during compilation process. The VMP data will be directly interpreted by ClangVMP runtime library without restoring the original instructions. Because of this mechanism, reverse engineering on this kind of code will be much more harder than raw machine code.

Till now, ClangVMP supports running on macOS, Windows and Linux. The following is a sample for version output on macOS installed to Xcode toolchain directory:
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
## Install
### Standalone
### Visual Studio
### Xcode
### Android NDK
### Linux
## IDE Configuration
### Visual Studio
### Xcode
## VMP Configuration
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
