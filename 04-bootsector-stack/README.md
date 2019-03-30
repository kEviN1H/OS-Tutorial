*Concepts you may want to Google beforehand: stack<br/>你可能想要事先谷歌概念：stack*

**Goal: Learn how to use the stack<br/>目标：学习如何使用堆栈**

The usage of the stack is important, so we'll write yet another boot sector
with an example.<br/>堆栈的使用非常重要，因此我们将用一个例子来编写另一个引导扇区。

Remember that the `bp` register stores the base address (i.e. bottom) of the stack,
and `sp` stores the top, and that the stack grows downwards from `bp` (i.e. `sp` gets
decremented)<br/>记住，`bp`寄存器存储堆栈的基址（即底部），`sp`存储堆栈的顶部，堆栈从`bp`向下增长（即`sp`递减）。

This lesson is quite straightforward, so jump ahead to the code.<br/>这一课很简单，所以请跳到代码前面。

I suggest that you try accessing in-stack memory addresses by yourself, 
at different points in the code, and see what happens.<br/>我建议您尝试自己在代码的不同点访问堆栈内存中的地址，然后看看会发生什么。
