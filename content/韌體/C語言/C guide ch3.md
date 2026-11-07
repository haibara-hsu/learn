---
title: C guide ch3：變數、運算子與流程控制
tags: [C語言, Beej, 韌體]
---

> 教材：Beej's Guide to C Programming，第 3 章
> 上一章：[[C guide ch2]]

## 本章架構

- **變數 Variables**：`int`、`float`、`char`、`bool`
- **運算子 Operators**
  - 算術運算子：`+ - * / %`
  - 三元運算子：`? :`
  - 前置 / 後置的遞增與遞減：`++ --`
  - 比較運算子（書上叫 conditional operators）：`== != < > <= >=`
  - 布林運算子：`! && ||`
  - `sizeof`
- **流程控制 Flow Control**：`if-else`、`while`、`do-while`、`for`、`switch`

## 1. 變數型別

| 型別 | 存什麼 | 例子 |
|---|---|---|
| `int` | 整數 | `int x = 10;` |
| `float` | 小數 | `float f = 3.14f;` |
| `char` | 一個字元，本質上是一個小整數 | `char c = 'A';` |
| `bool` | 真 / 假 | `bool ok = true;`（C23 之前要 `#include <stdbool.h>`） |

> [!note] C 裡的真假
> **0 是假，其他任何值都是真**。比較運算的結果是 `1`（真）或 `0`（假）。

## 2. 三元運算子 `? :`

```c
條件 ? 成立時的值 : 不成立時的值
```

```c
y += x > 10 ? 17 : 37;
y += (x > 10) ? 17 : 37;   // 加上括號比較好讀
```

意思是：如果 `x > 10`，`y` 就加 17，否則加 37。它是一個「會產生值」的 `if-else`。

## 3. 前置 / 後置遞增 `++i` vs `i++`

![[Pasted image 20261107115515.png]]

| 寫法 | 順序 | `i = 10; j = 5 + ___;` 的結果 |
|---|---|---|
| `i++`（後置） | **先拿 i 的舊值來用**，再把 i 加 1 | `i = 11, j = 15` |
| `++i`（前置） | **先把 i 加 1**，再拿新值來用 | `i = 11, j = 16` |

單獨寫成一行 `i++;` 時，兩種寫法的效果一樣，只有放在算式裡才會有差別。

## 4. `sizeof`

`sizeof` 會告訴你一個型別或變數佔幾個 **byte**：

```c
printf("%zu\n", sizeof(int));   // 在 Mac 上是 4
```

- 它是**運算子**，不是函式，而且在**編譯時期**就算好了
- 印 `sizeof` 的結果要用 `%zu`，因為它的型別是 `size_t`

> [!warning] 韌體重點
> `int` 有幾個 byte **要看平台**。所以韌體裡會用 `<stdint.h>` 的 `uint8_t`、`int16_t`、`uint32_t`，明確寫出位元數，因為暫存器的大小是固定的。

## 5. 流程控制

### while vs do-while

| | 順序 | 至少跑幾次 |
|---|---|---|
| `while` | **先檢查**條件，再執行 | 0 次 |
| `do-while` | **先執行**一次，再檢查條件 | 1 次 |

```c
while (i < 10) { ... }

do { ... } while (i < 10);   // 結尾的分號別忘了
```

### for vs while 怎麼選

- **知道要跑幾次** → 用 `for`
- **要跑到某個條件發生為止** → 用 `while`

```c
for (int i = 0; i < 10; i++) { ... }   // 跑 10 次
while (!button_pressed) { ... }        // 一直等到按鈕被按下
```

### switch

`switch` 會依照**整數值**找到對應的 `case` 來執行：

```c
switch (key) {
    case 1:
        unlock();
        break;      // 一定要 break，不然會繼續往下執行下一個 case
    case 2:
        lock();
        break;
    default:        // 都沒對上的時候
        beep();
        break;
}
```

> [!warning] 兩個重點
> 1. **每個 case 結尾都要 `break`**，否則會「掉下去」（fall-through），接著執行下一個 case。
> 2. `switch` 只能用**整數**來判斷（`int`、`char`、`enum`），不能用 `float` 或字串。

> [!tip] 跟密碼鎖的關係
> 密碼鎖 v2 的**狀態機（FSM）**，最常見的寫法就是 `switch (state) { case IDLE: ... case INPUT: ... }`，這一章的內容會直接用到。

關於快速cd到路徑的方法
1. 先輸入cd，用Tab自動補完
2. 先輸入cd，直接拖移

利用mv 資料一 資料夾二 
可以將檔案進行整理