*Concepts you may want to Google beforehand: control structures,
function calling, strings<br/>你可能想要事先谷歌概念：control structures,
function calling, strings*

**Goal: Learn how to code basic stuff (loops, functions) with the assembler<br/>目标：学习如何用汇编程序编写基本的代码（循环、函数）**

We are close to our definitive boot sector.<br/>我们离我们确定的引导部门很近。

In lesson 7 we will start reading from the disk, which is the last step before
loading a kernel. But first, we will write some code with control structures,
function calling, and full strings usage. We really need to be comfortable with
those concepts before jumping to the disk and the kernel.<br/>在第7课中，我们将开始从磁盘读取，这是加载内核之前的最后一步。但首先，我们将编写一些带有控制结构、函数调用和完整字符串用法的代码。在跳到磁盘和内核之前，我们真的需要熟悉这些概念。


Strings<br/>字符串
-------

Define strings like bytes, but terminate them with a null-byte (yes, like C)
to be able to determine their end.<br/>定义类似字节的字符串，但是用一个空字节终止它们（是的，类似于C），以便能够确定它们的结束。

```nasm
mystring:
    db 'Hello, World', 0
```

Notice that text surrounded with quotes is converted to ASCII by the assembler,
while that lone zero will be passed as byte `0x00` (null byte)<br/>请注意，汇编程序将用引号括起来的文本转换为ASCII，而单独的零将作为字节`0x00`（空字节）传递


Control structures<br/>控制结构
------------------

We have already used one: `jmp $` for the infinite loop.<br/>我们已经使用了一个：`jmp $`作为无限循环。

Assembler jumps are defined by the *previous* instruction result. For example:<br/>汇编程序跳转由*上一个*指令结果定义。例如：

```nasm
cmp ax, 4      ; if ax = 4
je ax_is_four  ; do something (by jumping to that label)
jmp else       ; else, do another thing
jmp endif      ; finally, resume the normal flow

ax_is_four:
    .....
    jmp endif

else:
    .....
    jmp endif  ; not actually necessary but printed here for completeness

endif:
```

Think in your head in high level, then convert it to assembler in this fashion.<br/>在您的头脑中进行高级思考，然后以这种方式将其转换为汇编程序。

There are many `jmp` conditions: if equal, if less than, etc. They are pretty 
intuitive but you can always Google them<br/>有许多`jmp`条件：如果相等，如果小于，等等。它们是非常直观的，但是你可以随时用谷歌搜索它们。


Calling functions<br/>调用函数
-----------------

As you may suppose, calling a function is just a jump to a label.<br/>正如您可能认为的，调用函数只是跳转到标签

The tricky part are the parameters. There are two steps to working with parameters:<br/>棘手的部分是参数。使用参数有两个步骤:

1. The programmer knows they share a specific register or memory address<br/>程序员知道他们共享一个特定的寄存器或内存地址。
2. Write a bit more code and make function calls generic and without side effects<br/>写更多的代码，使函数调用通用化，没有副作用

Step 1 is easy. Let's just agree that we will use `al` (actually, `ax`) for the parameters.<br/>

```nasm
mov al, 'X'
jmp print
endprint:

...

print:
    mov ah, 0x0e  ; tty code
    int 0x10      ; I assume that 'al' already has the character
    jmp endprint  ; this label is also pre-agreed
```

You can see that this approach will quickly grow into spaghetti code. The current
`print` function will only return to `endprint`. What if some other function
wants to call it? We are killing code reusage.<br/>

The correct solution offers two improvements:<br/>

- We will store the return address so that it may vary<br/>
- We will save the current registers to allow subfunctions to modify them
  without any side effects<br/>

To store the return address, the CPU will help us. Instead of using a couple of
`jmp` to call subroutines, use `call` and `ret`.<br/>

To save the register data, there is also a special command which uses the stack: `pusha`
and its brother `popa`, which pushes all registers to the stack automatically and
recovers them afterwards.<br/>


Including external files<br/>
------------------------

I assume you are a programmer and don't need to convince you why this is
a good idea.<br/>

The syntax is<br/>
```nasm
%include "file.asm"
```


Printing hex values<br/>
-------------------

In the next lesson we will start reading from disk, so we need some way
to make sure that we are reading the correct data. File `boot_sect_print_hex.asm`
extends `boot_sect_print.asm` to print hex bytes, not just ASCII chars.<br/>


Code! <br/>
-----

Let's jump to the code. File `boot_sect_print.asm` is the subroutine which will
get `%include`d in the main file. It uses a loop to print bytes on screen.
It also includes a function to print a newline. The familiar `'\n'` is
actually two bytes, the newline char `0x0A` and a carriage return `0x0D`. Please
experiment by removing the carriage return char and see its effect.<br/>

As stated above, `boot_sect_print_hex.asm` allows for printing of bytes.<br/>

The main file `boot_sect_main.asm` loads a couple strings and bytes,
calls `print` and `print_hex` and hangs. If you understood
the previous sections, it's quite straightforward.<br/>
