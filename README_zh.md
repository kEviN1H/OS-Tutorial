### os-tutorial教程
===========

How to create an OS from scratch!<br/>
如何从头开始创建一个操作系统！

I have always wanted to learn how to make an OS from scratch. In college I was taught
how to implement advanced features (pagination, semaphores, memory management, etc)
but:<br/>
我一直想学习如何从头开始制作操作系统。在大学里，我学习了如何实现高级功能（分页、信号量、内存管理等）
但是：

- I never got to start from my own boot sector
- 我从来没有从我自己的引导区开始过。
- College is hard so I don't remember most of it.
- 大学很难，所以我不记得大部分了。
- I'm fed up with people who think that reading an already existing kernel, even if small, is 
a good idea to learn operating systems.
- 我受够了那些认为阅读一个已经存在的内核（即使很小）是学习操作系统的好主意的人。

Inspired by [this document](http://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf)
and the [OSDev wiki](http://wiki.osdev.org/), I'll try to make short step-by-step READMEs and
code samples for anybody to follow. Honestly, this tutorial is basically the first document but
split into smaller pieces and without the theory.<br/>
根据[这份文档](http://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf)和[操作系统开发维基](http://wiki.osdev.org/),我将尝试一步一步地做一些简短的自述和代码示例，供任何人使用。老实说，本教程基本上是第一个文档，但是分成了更小的部分，没有理论。

### Features特征<br/>
- This course is a code tutorial aimed at people who are comfortable with low level computing. For example, programmers who have curiosity on how an OS works but don't have the time or willpower to start reading the Linux kernel top to bottom.
- 本课程是一个代码教程，针对那些熟悉低级计算的人。例如，对操作系统如何工作有好奇心但没有时间或意志力从头到脚阅读Linux内核的程序员。
- There is little theory. Yes, this is a feature. Google is your theory lecturer. Once you pass college, excessive theory is worse than no theory because it makes things seem more difficult than they really are.
- 几乎没有什么理论。是的，这是一个功能。谷歌是你的理论讲师。一旦你通过了大学，过度理论比没有理论更糟糕，因为它使事情看起来比实际困难。
- The lessons are tiny and may take 5-15 minutes to complete. Trust me and trust yourself. You can do it!<br/>
- 课程很小，可能需要5-15分钟才能完成。相信我，相信你自己。你能行！

### How to use this tutorial怎样使用这个教程
1. Start with the first folder and go down in order. They build on previous code, so if you jump right to folder 05 and don't know why there is a mov ah, 0x0e, it's because you missed lecture 02. Really, just go in order. You can always skip stuff you already know.<br/>从第一个文件夹开始，按顺序向下。它们建立在以前的代码之上，所以如果你直接跳到05文件夹，不知道为什么会有一个mov ah，0x0e，那是因为你错过了02课。真的，按顺序走。你可以跳过你已经知道的东西。
2. Open the README and read the first line, which details the concepts you should be familiar with before reading the code. Google concepts you are not familiar with. The second line states the goals for each lesson. Read them, because they explain why we do what we do. The "why" is as important as the "how".<br/>打开自述文件并阅读第一行，其中详细介绍了在阅读代码之前应该熟悉的概念。谷歌你不熟悉的概念。第二行说明了每节课的目标。阅读它们，因为它们解释了我们为什么要做我们所做的。“为什么”和“如何”一样重要。
3. Read the rest of the README. It is **very concise**.<br/>阅读自述文件的其余部分。它**非常简洁**。
4. (Optional) Try to write the code files by yourself after reading the README.<br/>(可选)在阅读自述文件后，尝试自己编写代码文件。
5. Look at the code examples. They are extremely well commented.<br/>看看代码示例。他们评论得非常好。
6. (Optional) Experiment with them and try to break things. The only way to make sure you understood something is trying to break it or replicate it with different commands.<br/>(可选)尝试它们，尝试打破事物。确保您理解某件事情的唯一方法是尝试破坏它或用不同的命令复制它。

TL;DR: First read the README on each folder, then the code files. If you're brave, try to code them yourself.<br/>首先阅读每个文件夹的自述文件，然后阅读代码文件。如果你很勇敢，试着自己编代码。

