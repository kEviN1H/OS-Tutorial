*Concepts you may want to Google beforehand: memory offsets, pointers<br/>你可能想要事先谷歌概念：memory offsets, pointers*

**Goal: Learn how the computer memory is organized<br/>目标：了解计算机内存的组织方式**

Please open page 14 [of this document](http://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf)<sup>1</sup>and look at the figure with the memory layout.<br/>
请打开[本文件](http://www.cs.bham.ac.uk/~exr/scheases/opsys/10_11/scheases/os-dev.pdf)<sup>1</sup>第14页。并查看带有内存布局的图。

The only goal of this lesson is to learn where the boot sector is stored<br/>本课的唯一目的是了解引导扇区的存储位置

I could just bluntly tell you that the BIOS places it at `0x7C00` and
get it done with, but an example with wrong solutions will make things clearer.<br/>
我可以直截了当地告诉你，bios将它放在“0x7c00”并完成它，但是一个错误解决方案的例子将使事情变得更清楚。

We want to print an X on screen. We will try 4 different strategies
and see which ones work and why.<br/>我们想在屏幕上打印一个X。我们将尝试4种不同的策略，看看哪种策略有效，为什么有效。

**Open the file `boot_sect_memory.asm`<br/>打开文件`boot_sect_memory.asm`**

First, we will define the X as data, with a label:<br/>首先，我们将x定义为数据，并带有一个标签：
```nasm
the_secret:
    db "X"
```

Then we will try to access `the_secret` in many different ways:<br/>然后我们将尝试以多种不同的方式访问“秘密”：

1. `mov al, the_secret`
2. `mov al, [the_secret]`
3. `mov al, the_secret + 0x7C00`
4. `mov al, 2d + 0x7C00`, where `2d` is the actual position of the 'X' byte in the binary其中，`2d`是二进制中“x”字节的实际位置

Take a look at the code and read the comments.<br/>查看代码并阅读注释。

Compile and run the code. You should see a string similar to `1[2¢3X4X`, where
the bytes following 1 and 2 are just random garbage.<br/>编译并运行代码。您应该看到类似于`1[2¢3X4X`的字符串，其中1和2后面的字节只是随机垃圾。

If you add or remove instructions, remember to compute the new offset of the X
by counting the bytes, and replace `0x2d` with the new one.<br/>如果添加或删除指令，请记住通过计算字节来计算x的新偏移量，并将`0x2d`替换为新的偏移量。

Please don't continue onto the next section unless you have 100% understood
the boot sector offset and memory addressing.<br/>请不要继续下一节，除非您100%了解引导扇区偏移量和内存寻址。


The global offset<br/>全局偏移
----

Now, since offsetting `0x7c00` everywhere is very inconvenient, assemblers let
us define a "global offset" for every memory location, with the `org` command:<br/>
现在，由于到处偏移`0x7c00`非常不方便，汇编程序允许我们用`org`命令为每个内存位置定义一个"global offset":

```nasm
[org 0x7c00]
```

Go ahead and **open `boot_sect_memory_org.asm`** and you will see the canonical
way to print data with the boot sector, which is now attempt 2. Compile the code
and run it, and you will see how the `org` command affects each previous solution.<br/>
继续并**打开`boot_sect_memory_org.asm`** 您将看到用引导扇区打印数据的规范方法，现在尝试2。编译代码并运行它，
您将看到`org`命令如何影响前面的每个解决方案。

Read the comments for a full explanation of the changes with and without `org`<br/>阅读评论以获得对有或无`org`的更改的完整解释

-----


[1] This whole tutorial is heavily inspired on that document. Please read the
root-level README for more information on that.<br/>[1] 整个教程都受到了该文档的启发。有关详细信息，请阅读根级自述文件。
