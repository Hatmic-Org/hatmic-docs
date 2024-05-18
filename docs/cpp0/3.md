# C++ 基础语法 - 3 循环结构

## 3.1 for 循环

在 C++ 中，循环结构用于重复执行一段代码，让代码在满足一定条件下反复执行。

for 循环是竞赛中最常用的循环结构，其语法如下：

```cpp
for (初始化表达式; 循环条件; 更新表达式) {
    // 循环体
}
```

初始化表达式在循环开始时执行的，一般用于初始化循环变量。

循环条件在每次迭代前都会被检查，如果条件为真，则继续循环；否则循环结束。

更新表达式在每次循环结束后执行，一般用于更新循环变量的值。

举一个例子：

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}
```

其中，`i++` 和 `i += 1` 的意思是一样的；还有 `i--` 和 `i -= 1` 的意思是一样的。

在初始化表达式中，要确保 `int i = 0` 这样的语句不要和在本函数内的变量和全局变量有冲突。不过像这样的，在初始化表达式中声明的变量只在这个循环中生效，你完全可以像这样写：

```cpp
int main () {
    for (int i = 0; i < 5; i++) {
        cout << i << endl;
    }

    for (int i = 0; i < 5; i++) {
        cout << i << endl;
    }


    int i = 10;
    cout << i << endl;

    return 0;
}
```

如果你想用一个已经声明过的变量，那你可以这样写 `for (i = 0; i < n; i++)` 也是完全没有问题的。

例如：

```cpp
int main () {
    int i;
    for (i = 0; i < 5; i++) {
        cout << i << endl;
    }

    return 0;
}
```

在一些情况下，初始化表达式和循环条件都是可以被省略的。比如你在前面已经初始化过循环变量，那就不需要再初始化了，你可以这样写：`for ( ; i < 5; i++)`；或者你不需要循环条件，即进行无限循环，那你可以这样写：`for (int i = 0; ; i++)`。但在大多数情况下，我们不会省略更新表达式，那样做是没有意义的。

## 3.2 while 循环

除了 for 循环，在竞赛中 while 循环也是很常见的。

while 循环在每次迭代之前检查循环条件，只有在条件为真时才执行循环体。其语法如下：

```cpp
while (循环条件) {
    // 循环体
}
```

示例：

```cpp
int i = 0;
while (i < 5) {
    cout << i << endl;
    i++;
}
```

请注意，在写 while 循环中一定要记着迭代循环变量，否则你会陷入死循环。这个问题在新人中很常见，并且在当你应对一些复杂题目中这样的错误很难被发现。

我们如何像 for 循环那样做一个无限循环呢？只需要让循环条件永远是 true 即可。你可以这样写：`while (2 > 1)`，很显然 $2$ 是永远大于 $1$ 的；或者直接这样写：`while (true)`。

## 3.3 break 与 main 函数中的 return 0;

当我们在循环中想要结束循环时，我们可以用 C++ 中的关键字 `break;` 或在 main 函数中使用 `return 0;` 来结束循环。

`break;` 的作用是 **结束这一循环，去执行后面的内容**。例如：你在无限循环中找到了一个是 $100$ 的倍数的数，你想赶快地结束循环并且输出 `I found it!`，那你可以这样做：

```cpp
int i = 0;
while (1) {
    i++;
    if(i % 100 == 0) {
        break; // 结束循环，去执行后面的内容
    }
}

cout << "I found it!" << endl;
```

而 **在 main 函数中**，`return 0;` 表示结束程序。如果程序执行到 `return 0;` 的时候，程序就停止运行了。`return 0;` 不仅可以写在 main 函数的末尾，也可以写在程序中。还是刚才的例子，我们可以这样编写程序：

```cpp
int i = 0;
while (1) {
    i++;
    if(i % 100 == 0) {
        cout << "I found it!" << endl;
        return 0; // 输出后，直接结束程序
    }
}
```

请注意，`return 0;` 一定要编写在合适的地方，否则可能会在程序应继续运行的时候停止运行。

## 3.4 题目 - 最大值

这道题是对于初学者的很常见的，你可以在 AtCoder 上提交这道题。题目在 [A - 最大値](https://atcoder.jp/contests/chokudai_S001/tasks/chokudai_S001_a) 这里。

题意很好理解：给你一个数字 $n$，然后给出长度为 $n$ 的序列，让你求序列中的最大值。

我们一共做 $n$ 次输入，这当然可以用循环来做。对于每一次输入，我们用变量 $x$ 来记录这个数字，再用变量 $maxx$ 来保存序列当前的最大值。那如何保存最大值呢？我们可以判断一下，如果 $maxx < x$，那说明此时 $maxx$ 就不是序列中的最大值了，我们就把 $maxx$ 赋值为 $x$；否则不改变 $maxx$ 的值。

当然，随便给 $maxx$ 设置一个数是不可靠的。我们在一开始把 $maxx$ 设置为序列中的第一个数就可以了。

代码如下：

```cpp
#include <iostream>

using namespace std;

int main () {
    int n;
    cin >> n;
    int maxx;

    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;

        if (i == 0) { // 如果是第一次输入 x，那就给 maxx 设置初始值为 x
            maxx = x;
        } else if (maxx < x) { // 如果当前 maxx 小于 x，那就把 maxx 赋值为 x
            maxx = x;
        }
    }

    cout << maxx << endl;
    return 0;
}
```

通过这个题目，我们可以很简单地想到如何求最小值，读者们可以去尝试一下。

<script src="https://giscus.app/client.js"
        data-repo="hatmic/hatmic-docs"
        data-repo-id="R_kgDOL9L8Zg"
        data-category="General"
        data-category-id="DIC_kwDOL9L8Zs4Cfc2T"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="light_tritanopia"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>