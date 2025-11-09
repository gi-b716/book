## Hello, World!

> 文件：[ch01-02-hello-world.md](https://github.com/gi-b716/book/blob/cn/src/ch01-02-hello-world.md)\
> 提交哈希：`f660f341887c8bbcd6c24fbfdf5d2a262f523965`\
> 译文更新日期：2025/11/9

现在你已经安装了 Rust，是时候编写你的第一个 Rust 程序了。
学习新语言时，传统做法是编写一个小程序，在屏幕上打印文本 `Hello, world!`，所以我们在这里也会这样做！

> 注意：本书假定你对命令行有基本的了解。
> Rust 对你的编辑工具、工具链或代码存放位置没有特定要求，所以如果你更喜欢使用 IDE 而不是命令行，请随意使用你喜欢的 IDE。
> 现在许多 IDE 都有一定程度的 Rust 支持；查看 IDE 的文档了解详情。
> Rust 团队一直专注于通过 `rust-analyzer` 实现出色的 IDE 支持。
> 有关更多详细信息，请参阅[附录 D][devtools]<!-- ignore -->。

<!-- Old headings. Do not remove or links may break. -->
<a id="creating-a-project-directory"></a>

### 项目目录设置

首先，你要创建一个目录来存储你的 Rust 代码。
Rust 不关心你的代码存放在哪里，但对于本书中的练习和项目，我们建议在你的主目录中创建一个 _projects_ 目录，并将所有项目都放在那里。

打开终端并输入以下命令，创建一个 _projects_ 目录，以及在 _projects_ 目录中为 "Hello, world!" 项目创建一个目录。

对于 Linux、macOS 和 Windows 上的 PowerShell，输入以下命令：

```console
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

对于 Windows CMD，输入以下命令：

```cmd
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

<!-- Old headings. Do not remove or links may break. -->
<a id="writing-and-running-a-rust-program"></a>

### Rust 程序基础

接下来，创建一个新的源文件并将其命名为 _main.rs_。
Rust 文件总是以 _.rs_ 扩展名结尾。
如果你要在文件名中使用多个单词，一个通常的做法是是使用下划线分隔它们。例如，使用 _hello_world.rs_ 而不是 _helloworld.rs_。

现在打开你刚刚创建的 _main.rs_ 文件，并输入清单 1-1 中的代码。

<Listing number="1-1" file-name="main.rs" caption="一个打印 `Hello, world!` 的程序">

```rust
fn main() {
    println!("Hello, world!");
}
```

</Listing>

保存文件并返回到 _~/projects/hello_world_ 目录中的终端窗口。
在 Linux 或 macOS 上，输入以下命令来编译和运行文件：

```console
$ rustc main.rs
$ ./main
Hello, world!
```

在 Windows 上，输入命令 `.\main` 而不是 `./main`：

```powershell
> rustc main.rs
> .\main
Hello, world!
```

无论你使用什么操作系统，字符串 `Hello, world!` 都应该打印到终端。
如果你没有看到这个输出，请参考安装部分的[“故障排除”][troubleshooting]<!-- ignore -->部分来获取帮助。

如果 `Hello, world!` 确实打印出来了，恭喜你！
你已经正式编写了一个 Rust 程序。这使你成为了一名 Rust 程序员——欢迎！

<!-- Old headings. Do not remove or links may break. -->

<a id="anatomy-of-a-rust-program"></a>

### Rust 程序剖析

让我们详细回顾这个 "Hello, world!" 程序。这是拼图的第一块：

```rust
fn main() {

}
```

这些行定义了一个名为 `main` 的函数。
`main` 函数很特殊：它始终是每个可执行 Rust 程序中运行的第一段代码。
这里，第一行声明了一个名为 `main` 的函数，它没有参数且不返回任何内容。
如果有参数，它们会放在括号 `()` 内。

函数体包裹在 `{}` 中。Rust 要求在所有函数体周围使用花括号。
好的代码风格是将左花括号放在函数声明的同一行，并在它们之间添加一个空格。

> 注意：如果你想在 Rust 项目中保持使用标准风格，可以使用名为 `rustfmt` 的自动格式化工具，以特定风格格式化你的代码（有关 `rustfmt` 的更多信息，请参阅[附录 D][devtools]<!-- ignore -->）。
> Rust 团队已将此工具包含在标准 Rust 发行版中，就像 `rustc` 一样，因此它应该已经安装在你的计算机上！

`main` 函数的主体包含以下代码：

```rust
println!("Hello, world!");
```

这一行完成了这个小程序中的所有工作：它将文本打印到屏幕上。
这里有三个重要的细节需要注意。

首先，`println!` 调用了一个 Rust 宏。如果它调用的是函数，则会是 `println`（没有 `!`）。
Rust 宏是一种编写代码以生成代码来扩展 Rust 语法的方式，我们将在[第 20 章][ch20-macros]<!-- ignore -->中详细讨论它们。
现在，你只需要知道使用 `!` 意味着你正在调用宏而不是普通函数，并且宏并不总是遵循与函数相同的规则。

其次，你看到了 `"Hello, world!"` 字符串。
我们将此字符串作为参数传递给 `println!`，然后字符串被打印到屏幕上。

第三，我们用分号（`;`）结束该行，这表示此表达式已结束，下一个表达式准备开始。
大多数 Rust 代码行都以分号结尾。

<!-- Old headings. Do not remove or links may break. -->
<a id="compiling-and-running-are-separate-steps"></a>

### 编译和执行

你刚刚运行了一个新创建的程序，现在让我们倒回来看看这个过程中的每个步骤。

在运行 Rust 程序之前，你必须使用 Rust 编译器编译它，方法是输入 `rustc` 命令并传递源文件的名称，如下所示：

```console
$ rustc main.rs
```

如果你有 C 或 C++ 的背景，你会注意到这类似于 `gcc` 或 `clang`。
编译成功后，Rust 会输出一个二进制可执行文件。

在 Linux、macOS 和 Windows 上的 PowerShell 上，你可以通过在 shell 中输入 `ls` 命令来查看可执行文件：

```console
$ ls
main  main.rs
```

在 Linux 和 macOS 上，你会看到两个文件。
在 Windows 上使用 PowerShell，你会看到与使用 CMD 时相同的三个文件。
在 Windows 上使用 CMD 时，你需要输入以下内容：

```cmd
> dir /B %= /B 选项表示只显示文件名 =%
main.exe
main.pdb
main.rs
```

这显示了带有 _.rs_ 扩展名的源代码文件、可执行文件（在 Windows 上是 _main.exe_，但在所有其他平台上是 _main_），以及在使用 Windows 时，一个包含调试信息的带有 _.pdb_ 扩展名的文件。
从这里，你运行 _main_ 或 _main.exe_ 文件，如下所示：

```console
$ ./main # 或在 Windows 上使用 .\main
```

如果你的 _main.rs_ 是 "Hello, world!" 程序，这一行命令会将 `Hello, world!` 打印到你的终端。

如果你更熟悉动态语言，如 Ruby、Python 或 JavaScript，你可能不习惯将编译和运行程序作为单独的步骤。
Rust 是一种 _提前编译_ 语言，这意味着你可以编译一个程序并将可执行文件提供给其他人，即使他们没有安装 Rust，他们也可以运行它。
如果你给某人一个 _.rb_、_.py_ 或 _.js_ 文件，他们需要分别安装 Ruby、Python 或 JavaScript 实现。但在这些语言中，你只需要一个命令来编译和运行你的程序。
一切都是语言设计中的权衡。

对于简单的程序，仅使用 `rustc` 编译就可以了，但随着项目的增长，你会想要管理所有选项并使共享代码变得容易。
接下来，我们将向你介绍 Cargo 工具，它将帮助你编写真实世界的 Rust 程序。

[troubleshooting]: ch01-01-installation.html#故障排除
[devtools]: appendix-04-useful-development-tools.html
[ch20-macros]: ch20-05-macros.html
