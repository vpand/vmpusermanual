# ClangVMP User Manual
## UltimateVMP
**UltimateVMP** (Ultimate Virtual Machine Protection), is an **arm/arm64/x86/x86_64** assembly level code virtualization encryption software for Darwin (**macOS/iOS**), **Linux** (Ubuntu/**Android**), **Windows** and other operating systems. It re-encodes the binary instructions of the target function into a private instruction format and then interprets the encoded instruction directly at run time. Unlike low-intensity code encryption such as obfuscation and shell, VMP code will not restore the original instruction throughout the whole execution process, so it can achieve high code encryption strength, greatly raising the threshold of reverse engineering, so as to achieve the purpose of protecting software assets. UltimateVMP currently supports platforms including **macOS, iOS, Linux, Android, Windows**, and supported architectures including **x86, x86_64, arm, and arm64**.

UltimateVMP includes two products. One is [ClangVMP](https://github.com/vpand/vmpusermanual/blob/main/ClangVMP.md)(based on the [Clang](https://clang.llvm.org/) compiler), it encodes **C/C++/ObjC/ObjC++/Swift**/etc.(static native programming language) function into VMP data during compilation process. The other is [PhoneVMP](https://github.com/vpand/vmpusermanual/blob/main/PhoneVMP.md), it encodes assembly instructions into VMP data from binary file(like **MachO/ELF/PE**). All of them are based on virtual processor infrastructure [UraniumVM](https://github.com/vpand/uvmsdkusermanual) from [vpand.com](https://vpand.com/). Their relationship is as following:
![relationship](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/relationship-1.svg)

This manual focuses on ClangVMP.

## ClangVMP
**ClangVMP** is a [Clang/LLVM](https://clang.llvm.org/) based code virtualized compiler. It encodes **C/C++/ObjC**/ObjC++/Swift/etc.(static native programming language) function into its private VMP data during compilation process. The VMP data will be directly interpreted by ClangVMP runtime library without restoring the original instructions. Because of this mechanism, reverse engineering on this kind of code will be much more harder than raw machine code.

Till now, ClangVMP supports running on **macOS, Windows and Linux**, and supported virtualized architectures including **x86_64 and arm64**. The following is a sample for version output on macOS installed to Xcode toolchain directory:
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
The Visual Studio installation type will install ClangVMP as a llvm toolchain for its project solution file. Its bin directory is as following:
![clangvmpvsbin](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpvsbin.png)
To apply this llvm like toolchain to Visual Studio project, you should do the following steps:
 * 1. Copy the Directory.build.props to your .sln located directory:
![clangvmpvsset0](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpvsset0.png)
 * 2. In Visual Studio Solution Property Pages, set General/Platform Toolset as LLVM(clang-cl):
![clangvmpvsset1](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpvsset1.png)
 * 3. In Visual Studio Solution Property Pages, set Advanced/LLVM Toolset Version as LLVM-Main-Version.Year.Month(e.g.: 19.2024.3, this is defined by ClangVMP llvm toolchain):
![clangvmpvsset2](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpvsset2.png)
 * 4. Make a test build to check whether everything goes well:
![clangvmpvsbuild](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmpvsbuild.png)
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
 * **Firstly**, look for clangvmp.json in the folder where the input **source code file** is located, if found, use this configuration, otherwise go to Secondly; 
 * **Secondly**, look for clangvmp.json in the **current working path** of the compiler (for Xcode, this is the path where xcodeproj is located; for NDK, this is the parent directory of jni). 
If found, use this configuration, otherwise turn to normal compilation;
![clangvmpjsonsearch](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmp.json-1.svg)
### Key source file
source_name.ext: source code file name including its extension, such as helloworld.c, helloworld.cpp, helloworld.cc, helloworld.m and helloworld.mm. If this file name as a key in clangvmp.json, then the compiler will apply its symbol array to virtualize or obfuscate that matched function.
### Key vmpre
vmpre(VMP regular expression): any function name symbol which matches this regular expression array will be **VMP virtualized**. e.g.: ".*" means all symbols, "vmpfn" means symbols contain substring vmpfn.
### Key obfre
obfre(Obfuscation regular expression): any function name symbol which matches this regular expression array will be **OLLVM obfuscated**.
### Demo
The following clangvmp.json means:
 * All the function symbols in **UVMInterpreter.cpp** contain substring "interp" will be virtualized, contain substring "main" will be obfuscated.
 * All the function symbols in **UVMRuntime.cpp** contain substring "exec" will be virtualized, contain substring "load" will be obfuscated.
```json
{
    "UVMInterpreter.cpp" : {
        "vmpre" : ["interp"],
        "obfre" : ["main"]
    },
    "UVMRuntime.cpp" : {
        "vmpre" : ["exec"],
        "obfre" : ["load"]
    }
}
```
## Raw vs VMP
### Raw
Normal compilation with clang compiler, we'll get the following assembly function:
```assembly
.text._Z7do_mainiPPKc:0000000000000004 ; int do_main(int argc, const unsigned __int8 **argv)
.text._Z7do_mainiPPKc:0000000000000004                 EXPORT _Z7do_mainiPPKc
.text._Z7do_mainiPPKc:0000000000000004 _Z7do_mainiPPKc                         ; CODE XREF: main+24↓p
.text._Z7do_mainiPPKc:0000000000000004
.text._Z7do_mainiPPKc:0000000000000004 var_90          = -0x90
.text._Z7do_mainiPPKc:0000000000000004 ptr             = -0x88
.text._Z7do_mainiPPKc:0000000000000004 var_8           = -8
.text._Z7do_mainiPPKc:0000000000000004 var_s0          =  0
.text._Z7do_mainiPPKc:0000000000000004 var_s10         =  0x10
.text._Z7do_mainiPPKc:0000000000000004 var_s20         =  0x20
.text._Z7do_mainiPPKc:0000000000000004 var_s30         =  0x30
.text._Z7do_mainiPPKc:0000000000000004 var_s40         =  0x40
.text._Z7do_mainiPPKc:0000000000000004 var_s50         =  0x50
.text._Z7do_mainiPPKc:0000000000000004
.text._Z7do_mainiPPKc:0000000000000004 ; __unwind {
.text._Z7do_mainiPPKc:0000000000000004                 SUB             SP, SP, #0xF0
.text._Z7do_mainiPPKc:0000000000000008                 STP             X29, X30, [SP,#0x90+var_s0]
.text._Z7do_mainiPPKc:000000000000000C                 STP             X28, X27, [SP,#0x90+var_s10]
.text._Z7do_mainiPPKc:0000000000000010                 STP             X26, X25, [SP,#0x90+var_s20]
.text._Z7do_mainiPPKc:0000000000000014                 STP             X24, X23, [SP,#0x90+var_s30]
.text._Z7do_mainiPPKc:0000000000000018                 STP             X22, X21, [SP,#0x90+var_s40]
.text._Z7do_mainiPPKc:000000000000001C                 STP             X20, X19, [SP,#0x90+var_s50]
.text._Z7do_mainiPPKc:0000000000000020                 ADD             X29, SP, #0x90
.text._Z7do_mainiPPKc:0000000000000024                 MRS             X8, #3, c13, c0, #2
.text._Z7do_mainiPPKc:0000000000000028 argc = X19                              ; int
.text._Z7do_mainiPPKc:0000000000000028                 MOV             W19, W0
.text._Z7do_mainiPPKc:000000000000002C                 STR             X8, [SP,#0x90+var_90]
.text._Z7do_mainiPPKc:0000000000000030                 ADRP            X0, #byte_180@PAGE
.text._Z7do_mainiPPKc:0000000000000034                 ADD             X0, X0, #byte_180@PAGEOFF ; name
.text._Z7do_mainiPPKc:0000000000000038                 LDR             X8, [X8,#0x28]
.text._Z7do_mainiPPKc:000000000000003C                 STUR            X8, [X29,#var_8]
.text._Z7do_mainiPPKc:0000000000000040                 BL              getenv
.text._Z7do_mainiPPKc:0000000000000044                 CMP             W19, #1
.text._Z7do_mainiPPKc:0000000000000048                 B.LT            loc_E8
.text._Z7do_mainiPPKc:000000000000004C                 MOV             W20, WZR
.text._Z7do_mainiPPKc:0000000000000050                 ADD             X27, SP, #0x90+ptr
.text._Z7do_mainiPPKc:0000000000000054                 ADRP            X21, #byte_227@PAGE
.text._Z7do_mainiPPKc:0000000000000058                 ADD             X21, X21, #byte_227@PAGEOFF
.text._Z7do_mainiPPKc:000000000000005C                 ADRP            X22, #byte_239@PAGE
.text._Z7do_mainiPPKc:0000000000000060                 ADD             X22, X22, #byte_239@PAGEOFF
.text._Z7do_mainiPPKc:0000000000000064                 ADRP            X23, #byte_23B@PAGE
.text._Z7do_mainiPPKc:0000000000000068                 ADD             X23, X23, #byte_23B@PAGEOFF
.text._Z7do_mainiPPKc:000000000000006C                 ADRP            X28, #byte_1E7@PAGE
.text._Z7do_mainiPPKc:0000000000000070                 ADD             X28, X28, #byte_1E7@PAGEOFF
.text._Z7do_mainiPPKc:0000000000000074                 ADRP            X26, #byte_1E2@PAGE
.text._Z7do_mainiPPKc:0000000000000078                 ADD             X26, X26, #byte_1E2@PAGEOFF
.text._Z7do_mainiPPKc:000000000000007C                 ADRP            X24, #byte_18B@PAGE
.text._Z7do_mainiPPKc:0000000000000080 i = X20                                 ; int
.text._Z7do_mainiPPKc:0000000000000080                 ADD             X24, X24, #byte_18B@PAGEOFF
.text._Z7do_mainiPPKc:0000000000000084
.text._Z7do_mainiPPKc:0000000000000084 loc_84                                  ; CODE XREF: do_main(int,char const**)+E0↓j
.text._Z7do_mainiPPKc:0000000000000084                 MOV             X0, X21 ; filename
.text._Z7do_mainiPPKc:0000000000000088                 MOV             X1, X22 ; modes
.text._Z7do_mainiPPKc:000000000000008C                 BL              fopen
.text._Z7do_mainiPPKc:0000000000000090                 MOV             X25, X0
.text._Z7do_mainiPPKc:0000000000000094                 ADD             X0, SP, #0x90+ptr ; ptr
.text._Z7do_mainiPPKc:0000000000000098                 MOV             W1, #1  ; size
.text._Z7do_mainiPPKc:000000000000009C                 MOV             W2, #0x7F ; n
.text._Z7do_mainiPPKc:00000000000000A0                 MOV             X3, X25 ; stream
.text._Z7do_mainiPPKc:00000000000000A4                 BL              fread
.text._Z7do_mainiPPKc:00000000000000A8                 STRB            WZR, [X27,X0]
.text._Z7do_mainiPPKc:00000000000000AC                 MOV             X0, X25 ; stream
.text._Z7do_mainiPPKc:00000000000000B0                 BL              fclose
.text._Z7do_mainiPPKc:00000000000000B4                 ADD             X0, SP, #0x90+ptr ; haystack
.text._Z7do_mainiPPKc:00000000000000B8                 MOV             X1, X23 ; needle
.text._Z7do_mainiPPKc:00000000000000BC                 BL              strstr
.text._Z7do_mainiPPKc:00000000000000C0                 CMP             X0, #0
.text._Z7do_mainiPPKc:00000000000000C4                 MOV             X0, X24 ; format
```
If we decompile it in IDA or any other decompiler tool, we'll get a perfect pseudo C source code implementation like this:
```c
__int64 __fastcall do_main(int argc, const unsigned __int8 **argv)
{
  int v2; // w19
  unsigned int v3; // w20
  FILE *v4; // x25
  const unsigned __int8 *v5; // x2
  __int64 result; // x0
  unsigned __int64 v7; // [xsp+0h] [xbp-90h]
  char ptr[128]; // [xsp+8h] [xbp-88h]
  __int64 v9; // [xsp+88h] [xbp-8h]

  v2 = argc;
  v7 = _ReadStatusReg(ARM64_SYSREG(3, 3, 13, 0, 2));
  v9 = *(_QWORD *)(v7 + 40);
  getenv((const char *)byte_180);
  if ( v2 >= 1 )
  {
    v3 = 0;
    do
    {
      v4 = fopen((const char *)byte_227, (const char *)byte_239);
      ptr[fread(ptr, 1uLL, 0x7FuLL, v4)] = 0;
      fclose(v4);
      if ( strstr(ptr, (const char *)byte_23B) )
        v5 = byte_1E7;
      else
        v5 = byte_1E2;
      printf((const char *)byte_18B, v3, v5);
      sleep(2u);
      ++v3;
    }
    while ( v2 != v3 );
  }
  result = puts((const char *)byte_1ED);
  if ( *(_QWORD *)(v7 + 40) == v9 )
    result = 0LL;
  return result;
}
```
### VMP
Virtualized compilation with clangvmp compiler, we'll get the following assembly function:
```assembly
.text._Z7do_mainiPPKc:0000000000000004 ; __int64 __fastcall do_main(int, const char **)
.text._Z7do_mainiPPKc:0000000000000004                 EXPORT _Z7do_mainiPPKc
.text._Z7do_mainiPPKc:0000000000000004 _Z7do_mainiPPKc                         ; DATA XREF: .data.rel.ro..L.vpand_com_ClangVMP_0:0000000000000398↓o
.text._Z7do_mainiPPKc:0000000000000004
.text._Z7do_mainiPPKc:0000000000000004 var_400         = -0x400
.text._Z7do_mainiPPKc:0000000000000004 var_3F0         = -0x3F0
.text._Z7do_mainiPPKc:0000000000000004 var_3E0         = -0x3E0
.text._Z7do_mainiPPKc:0000000000000004 var_3D0         = -0x3D0
.text._Z7do_mainiPPKc:0000000000000004 var_3C0         = -0x3C0
.text._Z7do_mainiPPKc:0000000000000004 var_3B0         = -0x3B0
.text._Z7do_mainiPPKc:0000000000000004 var_3A0         = -0x3A0
.text._Z7do_mainiPPKc:0000000000000004 var_390         = -0x390
.text._Z7do_mainiPPKc:0000000000000004 var_380         = -0x380
.text._Z7do_mainiPPKc:0000000000000004 var_370         = -0x370
.text._Z7do_mainiPPKc:0000000000000004 var_360         = -0x360
.text._Z7do_mainiPPKc:0000000000000004 var_350         = -0x350
.text._Z7do_mainiPPKc:0000000000000004 var_340         = -0x340
.text._Z7do_mainiPPKc:0000000000000004 var_330         = -0x330
.text._Z7do_mainiPPKc:0000000000000004 var_320         = -0x320
.text._Z7do_mainiPPKc:0000000000000004 var_310         = -0x310
.text._Z7do_mainiPPKc:0000000000000004
.text._Z7do_mainiPPKc:0000000000000004 ; __unwind {
.text._Z7do_mainiPPKc:0000000000000004                 SUB             SP, SP, #0x400
.text._Z7do_mainiPPKc:0000000000000008                 STP             X0, X1, [SP,#0x400+var_400]
.text._Z7do_mainiPPKc:000000000000000C                 STP             X2, X3, [SP,#0x400+var_3F0]
.text._Z7do_mainiPPKc:0000000000000010                 STP             X4, X5, [SP,#0x400+var_3E0]
.text._Z7do_mainiPPKc:0000000000000014                 STP             X6, X7, [SP,#0x400+var_3D0]
.text._Z7do_mainiPPKc:0000000000000018                 STP             X8, X9, [SP,#0x400+var_3C0]
.text._Z7do_mainiPPKc:000000000000001C                 STP             X10, X11, [SP,#0x400+var_3B0]
.text._Z7do_mainiPPKc:0000000000000020                 STP             X12, X13, [SP,#0x400+var_3A0]
.text._Z7do_mainiPPKc:0000000000000024                 STP             X14, X15, [SP,#0x400+var_390]
.text._Z7do_mainiPPKc:0000000000000028                 STP             X16, X17, [SP,#0x400+var_380]
.text._Z7do_mainiPPKc:000000000000002C                 STP             X18, X19, [SP,#0x400+var_370]
.text._Z7do_mainiPPKc:0000000000000030                 STP             X20, X21, [SP,#0x400+var_360]
.text._Z7do_mainiPPKc:0000000000000034                 STP             X22, X23, [SP,#0x400+var_350]
.text._Z7do_mainiPPKc:0000000000000038                 STP             X24, X25, [SP,#0x400+var_340]
.text._Z7do_mainiPPKc:000000000000003C                 STP             X26, X27, [SP,#0x400+var_330]
.text._Z7do_mainiPPKc:0000000000000040                 STP             X28, X29, [SP,#0x400+var_320]
.text._Z7do_mainiPPKc:0000000000000044                 STP             X30, X17, [SP,#0x400+var_310]
.text._Z7do_mainiPPKc:0000000000000048                 BL              vpand_com_ClangVMP_9d4bf2e9b10ef523_1
.text._Z7do_mainiPPKc:000000000000004C                 MOV             X3, X0
.text._Z7do_mainiPPKc:0000000000000050                 BL              vpand_com_ClangVMP_9d4bf2e9b10ef523_0
.text._Z7do_mainiPPKc:0000000000000054                 MOV             X2, #0
.text._Z7do_mainiPPKc:0000000000000058                 B               vpand_com_ClangVMP_entry
```
If we decompile it in IDA or any other decompiler tool, we'll get a perfect pseudo C source code implementation like this:
```c
__int64 __usercall do_main@<X0>(const char **a1@<X1>, __int64 a2@<X0>, __int64 a3@<X2>, __int64 a4@<X3>, __int64 a5@<X4>, __int64 a6@<X5>, __int64 a7@<X6>, __int64 a8@<X7>, __int64 a9@<X8>)
{
  __int64 v9; // x9
  __int64 v10; // x0

  vpand_com_ClangVMP_9d4bf2e9b10ef523_1(a2, a1, a3, a4, a5, a6, a7, a8, a2, a1, a3, a4, a5, a6, a7, a8, a9, v9);
  v10 = vpand_com_ClangVMP_9d4bf2e9b10ef523_0();
  return vpand_com_ClangVMP_entry(v10);
}
```
Oops, we can see nothing about this function, all of the raw instructions are encoded as ClangVMP runtime data. As so, reverse engineering will be extremely hard. This is the core value of ClangVMP.
## Trial version
The default installation without a valid license is a trial version for code virtualized compilation test, the result cannot run. If you want to apply it to your real products, please contact us to buy a license.
```shell
ClangVMP@vpand.com android % ndk-build -B
[arm64-v8a] Compile++      : antidebug <= antidebug.cpp
There's no license file ~/VPAssistant/license/clangvmp.license, please contact us to buy a license.
----------------------------WARNING----------------------------
This trial version of ClangVMP is just used for compilation test, the result cannot run!
---------------------------------------------------------------
Using config file jni/../../clangvmp.json.
Using global vmp config key : *.
vmpre: main
vmp: _Z7do_mainiPPKc
vmp: main
+> Encoding UraniumVCPU function _Z7do_mainiPPKc (1/2)...
+> Encoding UraniumVCPU function main (2/2)...
[arm64-v8a] Executable     : antidebug
```
## Licensed version
If you want to upgrade to a licensed version, here's the steps:
 * 1. Contact us to pay for your license;
 * 2. Send your computer os-arch-hwid(copy from VPAssistant startup log) to us;
 * 3. Switch to VPAssistant License tab widget, click Install button to download and install the license file;

![clangvmplicense](https://raw.githubusercontent.com/vpand/imgres/main/ultimatevmp/clangvmplicense.jpg)
With this license, we can virtualized compile our final executable product:
```shell
ClangVMP@vpand.com android % ndk-build -B
[arm64-v8a] Compile++      : antidebug <= antidebug.cpp
Using config file jni/../../clangvmp.json.
Using global vmp config key : *.
vmpre: main
vmp: _Z7do_mainiPPKc
vmp: main
+> Encoding UraniumVCPU function _Z7do_mainiPPKc (1/2)...
+> Encoding UraniumVCPU function main (2/2)...
[arm64-v8a] Executable     : antidebug
```
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
