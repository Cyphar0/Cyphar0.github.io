---
layout: post
title: "BUUCTF-reverse-easyre1(非常简单的逆向)"
category: reverse
date: 2025-02-06
---

将解压出的easyre.exe放入studyPE查壳：

无壳，是一个c++文件

![1](\assets\images\easyre1\1.png)

IDA打开后，呃…

![2](\assets\images\easyre1\2.png)

结构很简单，那就从头开始拆解一下程序在做什么…

```c++
b= dword ptr -8
a= dword ptr -4
```

a、b两个整数变量在栈里的偏移量分别为-8和-4（地址）

```c++
push    rbp
mov     rbp, rsp
sub     rsp, 30h
```

前期准备可忽略，先保存旧的rbp用于回溯，mov把rsp赋给rbp，设置新的栈帧基址，sub为局部变量分配0x30（48）字节的空间

```c++
call    __main
lea     rdx, [rbp+b]
lea     rax, [rbp+a]
mov     r8, rdx
mov     rdx, rax
lea     rcx, Format     ; "%d%d"
;   try {
call    scanf
```

rdx指向a的地址，r8指向b的地址，这段只是main通过scanf读取两个整数，存在a和b中

```c++
mov     edx, [rbp+a]
mov     eax, [rbp+b]
cmp     edx, eax
jnz     short loc_40152F
```

关键只有这个，cmp比较a和b，如果 `a ≠ b`，跳转到 `loc_40152F`；如果 `a == b`，则继续执行后续代码

要得到flag，即让程序跳转到左边，给a、b赋相同的值就行

![3](\assets\images\easyre1\3.png)



工具太强大会丧失很多趣味性啊