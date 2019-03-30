Concepts you may want to Google beforehand: assembler, BIOS<br/>
你可能想要事先谷歌概念:assembler, BIOS<br/>

**Goal: Create a file which the BIOS interprets as a bootable disk<br/>
目标：创建一个BIOS解释为可引导磁盘的文件**

This is very exciting, we're going to create our own boot sector!
这是非常兴奋的，我们将创建自己的引导扇区！

### Theory<br/>理论<br/>
When the computer boots, the BIOS doesn't know how to load the OS, so it delegates that task to the boot sector. Thus, the boot sector must be placed in a known, standard location. That location is the first sector of the disk (cylinder 0, head 0, sector 0) and it takes 512 bytes.<br/>
当计算机启动时，BIOS不知道如何加载操作系统，因此它将该任务委托给启动扇区。因此，引导扇区必须放置在已知的标准位置。该位置是磁盘的第一个扇区（cylinder 0柱面0、head 0磁头 0、sector 0扇区0），需要512字节。<br/>

To make sure that the "disk is bootable", the BIOS checks that bytes 511 and 512 of the alleged boot sector are bytes `0xAA55`.<br/>
为了确保“磁盘是可引导的”，BIOS检查所谓引导扇区的字节511和512是字节0xAA55。<br/>

This is the simplest boot sector ever:<br/>
这是有史以来最简单的引导扇区：<br/>
```
e9 fd ff 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
[ 29 more lines with sixteen zero-bytes each ]
00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 aa
```

It is basically all zeros, ending with the 16-bit value `0xAA55` (beware of endianness, x86 is little-endian). The first three bytes perform an infinite jump<br/>
它基本上都是0，以16位值结尾` 0xAA55`（注意字节顺序，x86是小端）。前三个字节执行无限跳转<br/>

**Simplest boot sector ever<br/>
最简单的引导扇区<br/>
-------------------------**

You can either write the above 512 bytes with a binary editor, or just write a very simple assembler code:<br/>
您可以使用二进制编辑器编写上述512字节，也可以只编写一个非常简单的汇编程序代码：<br/>
```nasm
; Infinite loop (e9 fd ff)
loop:
    jmp loop 

; Fill with 510 zeros minus the size of the previous code
times 510-($-$$) db 0
; Magic number
dw 0xaa55 
```

To compile编译:<br/>
`nasm -f bin boot_sect_simple.asm -o boot_sect_simple.bin`

> OSX warning: if this drops an error, read chapter 00 again<br/>OSX警告：如果出现错误，请再次阅读第00章<br/>

I know you're anxious to try it out (I am!), so let's do it:<br/>O我知道你很想试试（我是！），让我们来做：<br/>O

`qemu boot_sect_simple.bin`

> On some systems, you may have to run `qemu-system-x86_64 boot_sect_simple.bin` If this gives an SDL error, try passing the --nographic and/or --curses flag(s).<br/>在某些系统上，您可能需要运行'qemu-system-x86_64 boot-sect_simple.bin'，如果这会导致SDL错误，请尝试传递--nographic和/或--curses标志。<br/>

You will see a window open which says "Booting from Hard Disk..." and nothing else. When was the last time you were so excited to see an infinite loop? ;-)<br/>你会看到一个窗口打开，上面写着“从硬盘启动…”，没有其他内容。上一次你如此兴奋地看到无限循环是什么时候？；-）
