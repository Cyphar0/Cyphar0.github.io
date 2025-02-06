---
layout: post
title: "BUUCTF-reverse-reverse1"
category: reverse
date: 2025-02-06
---

解压得到reverse1.exe，IDA打开

![1](\assets\images\reverse1\1.png)

```c++
jmp     main_0
```

提示跳转到main_0的地址，来看看main_0的构造

![2](\assets\images\reverse1\2.png)

转换成代码

![3](\assets\images\reverse1\3.png)

下面的if在判别Str1, Str2的前v5位字符是否匹配，相同输出right，不同输出wrong

Str1需要用户输入，从前面的流程图可以看到Str2就是{hello_world}，或者双击Str2变量可以直接看到

![404](\assets\images\reverse1\4.png)

往上看一个for循环

```c
  for ( j = 0; ; ++j )
  {
    v10 = j;
    if ( j > j_strlen(Str2) )
      break;
    if ( Str2[j] == 111 )
      Str2[j] = 48;
  }
```

这段对Str2进行了修饰，遍历Str2，把Str2中ascII等于111的字符转换为ascII48

选中数字按R（注意大写）可以转成char

![999](\assets\images\reverse1\5.png)

它把o改成了0

最终得到{hell0_w0rld}

也是很简单的题，下次找个难一点的（…

