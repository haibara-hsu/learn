---
title: C guide ch2：Hello World 與編譯流程
tags: [C語言, Beej, 韌體]
---

> 教材：Beej's Guide to C Programming，第 2 章
> 練習檔位置：`韌體/核心底層能力：進階 C 語言與記憶體管理/:code/Ch2/Ch2.2/hello.c`
> 下一章：[[C guide ch3]]

## 1. 單字

| 單字 | 意思 |
|---|---|
| octothorpe | 井字號 `#`（開玩笑的說法，一般叫 hash） |
| gratuitously | 沒必要地、多此一舉地 |
| squirrelly | 彎彎曲曲的，指大括號 `{ }`（squirrelly braces） |
| semicolon | 分號 `;`，C 的每個陳述句都以它結尾 |

## 2. 編譯並執行

```bash
cc -Wall -Wextra -std=c11 hello.c -o hello && ./hello
```

![[Pasted image 20261107103840.png]]

| 片段 | 意思 |
|---|---|
| `cc` | 呼叫 C 編譯器（Mac 上的 `gcc` / `cc` 其實都是 clang） |
| `-Wall` | 打開常見的警告（W = Warning） |
| `-Wextra` | 再多打開一組額外的警告 |
| `-std=c11` | 指定要用哪一版的 C 標準（c11 是數字 11，不是兩個 l） |
| `-pedantic` | 嚴格遵守該版標準，用到編譯器自己的擴充語法也會警告 |
| `hello.c` | 原始碼 |
| `-o hello` | 輸出檔叫 `hello`（o = output）。不寫的話，預設叫 `a.out` |
| `&&` | 前一個指令成功，才執行後面那個 |
| `./hello` | 執行目前資料夾裡的 `hello` |

更嚴格的版本：

```bash
cc -Wall -Wextra -std=c23 -pedantic hello.c -o hello
```

> [!tip] 為什麼要加 `./`？
> 終端機只會到 `PATH` 列出的資料夾（例如 `/usr/bin`）找程式，**不會找目前所在的資料夾**，這是為了安全。所以執行自己編譯出來的程式，要用 `./` 指明「就是這裡的這個」。

> [!tip] 為什麼要開警告？
> 警告抓的是「能編譯過，但很可能是 bug」的寫法，例如 `if (a = 5)`、變數沒有初始值、有號數和無號數比較。業界常要求**零警告**，有些專案甚至加上 `-Werror`，有警告就直接編譯失敗。

### 我踩過的錯

![[Pasted image 20261107104355.png]]

| 錯誤訊息 | 原因 |
|---|---|
| `cd: too many arguments` | 路徑裡有空格，要用 `"..."` 把路徑包起來 |
| `unknown argument '-wall'` | 參數有分大小寫，要寫 `-Wall` |
| `invalid value 'cll'` | `c11` 打成了兩個英文字母 l |
| `no such file or directory: ./hello` | 前面編譯失敗，所以根本沒有產生執行檔 |
| `permission denied: ./hello.i` | `.i` 是文字檔不是程式，只能用「看」的，不能執行 |
| `duplicate symbol '_main'` | 兩個 `.c` 都有 `main()`，一起編譯時在 Link 階段衝突 |

## 3. 編譯的四個階段

```
hello.c ─(1)前處理─► hello.i   展開 #include、#define
        ─(2)編譯───► hello.s   組合語言
        ─(3)組譯───► hello.o   目的檔（機器碼，還不能執行）
        ─(4)連結───► hello     可執行檔（Linker 把多個 .o 和函式庫接起來）
```

可以分別停在每個階段，看它的產物：

```bash
cc -E hello.c -o hello.i   # 1. 前處理後的原始碼
cc -S hello.c -o hello.s   # 2. 組合語言
cc -c hello.c -o hello.o   # 3. 目的檔
```

多個檔案一起編譯時，每個 `.c` 會**各自**變成 `.o`，最後才由 Linker 接起來：

```bash
cc -o awesomegame ui.c characters.c npc.c items.c
```

### 怎麼看這些檔案

`.i` 和 `.s` 是**文字檔**：

```bash
open hello.i       # 用文字編輯器打開
tail -15 hello.i   # 在終端機看最後 15 行
less hello.i       # 從頭慢慢翻（空白鍵往下翻，q 離開）
```

> `hello.c` 只有 14 行，`hello.i` 卻有 580 行，因為 `#include <stdio.h>` 就是把整份標頭檔**原封不動貼進來**。

`.o` 是**二進位檔**，要用 `nm` 看裡面的符號：

```bash
nm hello.o
```

![[Pasted image 20261107110100.png]]

| 符號 | 意思 |
|---|---|
| `T _main` | T = Text：這個檔案裡**定義**了 `main` |
| `U _printf` | U = Undefined：這個檔案有用到，但定義在別處，要等 Linker 去找來接上 |

## 4. 跟韌體的關係

- STM32 用的也是同一套流程，只是編譯器換成 `arm-none-eabi-gcc`，最後再用 **Linker Script（`.ld`）** 決定程式放在 Flash 的哪裡、變數放在 RAM 的哪裡，產出 `.elf` / `.bin` / `.hex`
- **Makefile** 就是把這些指令寫成腳本
- 面試常考：
  - `.c` 變成 `.hex` 的過程中發生了什麼？
  - compile error 和 link error 差在哪？
