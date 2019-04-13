---
title: 实用 jar 包反编译工具
date: 2019-04-13 22:12:27
tags:
 - 反编译
 - Java
---

<!-- toc -->

查看源码一定是广大程序员的刚需，对于 .Net 平台，Jetbrains 有 [dotPeek](https://www.jetbrains.com/decompiler/) 支持，界面和 Visual Studio 类似，使用体验也很不错。

![image-20190413222128381](./assets/decompiler_overview.png)

对于 Java 的反编译工具，目前有 JD-GUI, luyten 等等。看官网的界面设计觉着很一般，琢磨有没有插件能够直接将 jar 包反编译出整个工程，这样用 IDEA 还是 VSC 都可以看。发现其实 IDEA 内置的反编译插件 `java-decompiler.jar` 就可以。利用它即可恢复出整个工程目录，这样就不用额外下载第三方的反编译查看工具了。下面介绍步骤。

## 使用 java-decompiler.jar 反编译

Mac 用户如果安装了 IDEA 一般在

```shell
/Applications/IntelliJ IDEA.app/Contents/plugins/java-decompiler/lib/
```

这个位置（Win 的位置不知道，应该也在 IDEA 的安装目录）。

进入目录，执行：

```shell
java -cp java-decompiler.jar org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler /path/to/test.jar /target/
```

即可在 `/target/` 生成一个 `test.jar` 文件，你可能会疑惑怎么还是个 jar 包，其实这个 jar 包里的 class 文件已经被反编译成 java 文件了，将 jar 包解压即可得到完整的工程目录：

```shell
unzip test.jar
```

到此就算完了，为了方便下次使用可以在 bash 里设置一个 alias（Win 的 Git Bash 应该也可以）。

## 设置 alias

可以在 `.bash_profile` 或者 `.zshrc` 给 `java -cp ~/Desktop/Velen/Java/lib/java-decompiler.jar org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler` 设置一个 alias，比如：

```shell
alias decjava='java -cp ~/Desktop/Velen/Java/lib/java-decompiler.jar org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler'
```

这样下次只要运行：

```shell
decjava /path/to/test.jar /target/dir/
```

就可以反编译 jar 包了。





