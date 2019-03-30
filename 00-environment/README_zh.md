Concepts you may want to Google beforehand: linux, mac, terminal, compiler, emulator, nasm, qemu<br/>
你可能想要事先谷歌概念:linux, mac, terminal, compiler, emulator, nasm, qemu<br/>

**Goal: Install the software required to run this tutorial<br/>
目标:安装软件需要运行这个教程**

I'm working on a Mac, though Linux is better because it will have all the standard tools already available for you.<br/>
我正在开发一个Mac，不过Linux更好，因为它已经为您提供了所有的标准工具。<br/>

On a mac, install Homebrew and then brew install qemu nasm<br/>
在Mac上，[install homebrew]（http://brew.sh），然后'brew install qemu nasm`<br/>

Don't use the Xcode developer tools nasm if you have them installed, they won't work for the most cases. Always use /usr/local/bin/nasm<br/>
不要使用Xcode开发人员工具nasm如果你安装了它们，它们在大多数情况下不会工作。始终使用/usr/local/bin/nasm<br/>

On some systems qemu is split into multiple binaries. You may want to call qemu-system-x86_64 binfile<br/>
在某些系统上，QEMU被分成多个二进制。您可能需要调用qemu-system-x86二进制文件
