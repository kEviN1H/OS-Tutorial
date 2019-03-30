*Concepts you may want to Google beforehand: interrupts, CPU registers<br/>你可能想要事先谷歌概念：interrupts, CPU
registers*

**Goal: Make our previously silent boot sector print some text<br/>目标：让我们以前无声的引导扇区打印一些文本**

We will improve a bit on our infinite-loop boot sector and print something on the screen. We will raise an interrupt for this.<br/>
我们将改进无限循环引导扇区，并在屏幕上打印一些内容。我们将为此提出一个中断。


On this example we are going to write each character of the "Hello" word into the register `al` (lower part of `ax`), the bytes `0x0e` into `ah` (the higher part of `ax`) and raise interrupt `0x10` which is a general interrupt for video services.<br/>
在本例中，我们将把“hello”字的每个字符写入寄存器“al”（ax的下半部分）、字节“0x0e”写入“ah”（ax的上半部分）并引发中断“0x10”，这是视频服务的一般中断。


`0x0e` on `ah` tells the video interrupt that the actual function
we want to run is to 'write the contents of `al` in tty mode'.<br/>
` 0x0E`on`ah`告诉视频中断实际功能我们要运行的是“在tty模式下写入”al“的内容”。


We will set tty mode only once though in the real world we 
cannot be sure that the contents of `ah` are constant. Some other
process may run on the CPU while we are sleeping, not clean
up properly and leave garbage data on `ah`.<br/>
我们将只设置一次tty模式，但在现实世界中不能确定'ah'的内容是常量。其他一些进程可能在我们睡觉时在CPU上运行，而不是干净的正确启动并将垃圾数据保留在“ah”上。


For this example we don't need to take care of that since we are the only thing running on the CPU.<br/>
对于这个例子，我们不需要考虑这个问题，因为我们是CPU上唯一运行的东西。


Our new boot sector looks like this:<br/>我们的新引导扇区如下：


```nasm
mov ah, 0x0e ; tty mode
mov al, 'H'
int 0x10
mov al, 'e'
int 0x10
mov al, 'l'
int 0x10
int 0x10 ; 'l' is still on al, remember?
mov al, 'o'
int 0x10

jmp $ ; jump to current address = infinite loop

; padding and magic number
times 510 - ($-$$) db 0
dw 0xaa55 
```

You can examine the binary data with `xxd file.bin`<br/>
您可以使用`xxd file.bin`检查二进制数据


Anyway, you know the drill:<br/>
不管怎样，你知道这个练习：


`nasm -fbin boot_sect_hello.asm -o boot_sect_hello.bin`

`qemu boot_sect_hello.bin`

Your boot sector will say 'Hello' and hang on an infinite loop<br/>
您的引导扇区会说“你好”，并挂起一个无限循环。

