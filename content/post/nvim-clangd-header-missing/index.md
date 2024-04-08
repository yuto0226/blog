---
title: "Windows 11 中 Neovim clangd 找不到標頭檔"
slug: neovim-clangd-no-found-header-file
description: 解決 Neovim LSP 設定中，clangd 找不到標頭檔的問題。紀錄 debug 紀錄以及解決方法。
date: 2024-04-07T01:37:32+08:00
image: cover.png
math: true
draft: false
categories:
    - 計算機科學
    - Troubleshooting
tags:
    - Neovim
    - LSP
    - Clang
    - GCC
---
近日在使用一個 Neovim 的發行版 NVChad，設定 C/C++ 的 LSP Server。然後就遇到了標頭檔找不到的問題。

<img src="image.png" alt="標頭檔找不到" width="800"/>

可以看到 Neovim 裡面的介面上面出現警告資訊：

```shell
'stdio.h' file not found
```

這就很奇怪了，根據我過往使用 gcc 的經驗，C library 應該是不用再額外引入的。

## 找資料

我的第一步就是直接上 Google 找：

```text
nvim clangd
```

於是我就找到了這一篇 stack overflow 的文章

- [What standard C library does Clang use? glibc, its own, or some other one?](https://stackoverflow.com/questions/59019932/what-standard-c-library-does-clang-use-glibc-its-own-or-some-other-one)

上面就詢問了 clang 是使用了哪一個 C 的函式庫。

>Clang does not come with its own C standard library. Rather, it ["supports a wide variety of C standard library implementations"](https://clang.llvm.org/docs/Toolchain.html#c-standard-library).
>
>Unix-like systems including Mac OS ship with their own. Windows does not. On Windows the default arrangement requires Microsoft's Visual C libraries to be installed. It seems that it's also possible to use Clang on Windows with MinGW's libraries though.
><br>╴<i class="fa-solid fa-user"></i> <em>hippietrail</em>

回覆的大略是說，Clang 並沒有自己的 C 函式庫。其中最引人注目的便是他所引入的網址了，妥妥的一手資料，是絕佳的參考資料。

因此我接著去找 Clangd 的官方文檔，我找到了這段說明

-

>If you’re using an unusual compiler (e.g. a cross-compiler for a different platform, or MinGW on Windows) you may want to pass --query-driver=/path/to/mygcc or --query-driver=/path/to/mygcc,/path/to/myg++ when using C++ to allow clangd to extract the include paths from it directly.

這跟我的情況很像，Clang 找不到我的 gcc 帶的 C library。於是我參考了 Configuration 中的指示去把 `--query-driver=C:\Users\USER\scoop\apps\gcc\current\bin` 的編譯參數寫入 Clang 的 `C:\Users\USER\AppData\Local\clangd\config.yaml`，來調整預設的編譯參數。

```yaml
CompileFlags:
    - --query-driver: C:\Users\USER\scoop\apps\gcc\current\bin
```

但很顯然的結果並不那麼美好

<img src="image.png" alt="標頭檔找不到" width="800"/>

基本上還是一樣的狀況。但隨後我就在 issue 中找到了一篇跟我狀況相似的，同樣是 Windows 作業系統，同樣是用 `--query-driver`。

- [https://github.com/clangd/clangd/issues/537#issuecomment-1479544442](https://github.com/clangd/clangd/issues/537#issuecomment-1479544442)

## 總結

上述那篇 issue 的留言給出了一個解法

```yaml
CompileFlags:
    - --target=x86_64-w64-windows-gnu
```

## 參考資料

- [Clangd:Troubleshooting-Can’t find standard library headers (<map>, <stdio.h> etc)](https://clangd.llvm.org/troubleshooting#cant-find-standard-library-headers-map-stdioh-etc)
- [Clangd:Configuration-Files](https://clangd.llvm.org/config#files)
- [--query-driver not having any effect #537](https://github.com/clangd/clangd/issues/537#issuecomment-1479544442)
