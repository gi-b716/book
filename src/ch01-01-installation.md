## 安装

> 文件：[ch01-01-installation.md](https://github.com/gi-b716/book/blob/cn/src/ch01-01-installation.md)\
> 提交哈希：`369386fefd1138cbdf50ae628bae1ffc4ffce669`\
> 译文更新日期：2025/11/9

第一步是安装 Rust。我们将通过 `rustup` 下载 Rust，这是一个用于管理 Rust 版本和相关工具的命令行工具。你需要互联网连接才能下载。

> 注意：如果你因某些原因不想使用 `rustup`，请参阅[其他 Rust 安装方法页面][otherinstall]了解更多选项。

以下步骤将安装最新稳定版本的 Rust 编译器。Rust 的稳定性保证确保本书中所有能编译的示例在更新的 Rust 版本中也能继续编译。不同版本之间的输出可能略有不同，因为 Rust 经常改进错误消息和警告。换句话说，使用这些步骤安装的任何更新的稳定版本的 Rust 都应该能够按预期与本书的内容一起工作。

> ### 命令行符号
>
> 在本章和整本书中，我们将展示一些在终端中使用的命令。你应该在终端中输入的行都以 `$` 开头。你不需要输入 `$` 字符；它是命令行提示符，用于指示每个命令的开始。不以 `$` 开头的行通常显示前一个命令的输出。此外，PowerShell 特定的示例将使用 `>` 而不是 `$`。

### 在 Linux 或 macOS 上安装 `rustup`

如果你使用的是 Linux 或 macOS，打开终端并输入以下命令：

```console
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

该命令下载一个脚本并开始安装 `rustup` 工具，该工具会安装最新稳定版本的 Rust。你可能会被提示输入密码。如果安装成功，将出现以下行：

```text
Rust is installed now. Great!
```

你还需要一个 _链接器_，这是 Rust 用来将其编译输出合并到一个文件中的程序。你可能已经有一个了。如果遇到链接器错误，你应该安装一个 C 编译器，它通常会包含一个链接器。C 编译器也很有用，因为一些常见的 Rust 包依赖于 C 代码，需要 C 编译器。

在 macOS 上，你可以通过运行以下命令获得 C 编译器：

```console
$ xcode-select --install
```

Linux 用户通常应该根据其发行版的文档安装 GCC 或 Clang。例如，如果你使用 Ubuntu，可以安装 `build-essential` 包。

### 在 Windows 上安装 `rustup`

在 Windows 上，访问 [https://www.rust-lang.org/tools/install][install]<!-- ignore
--> 并按照说明安装 Rust。在安装过程中的某个时刻，你会被提示安装 Visual Studio。这会提供链接器和编译程序所需的本机库。如果你在这一步需要更多帮助，请参阅
[https://rust-lang.github.io/rustup/installation/windows-msvc.html][msvc]<!--
ignore -->。

本书使用在 _cmd.exe_ 和 PowerShell 中都能运行的命令。如果有差异，我们会说明应该使用哪一个。

### 故障排除

要检查你是否正确安装了 Rust，打开 shell 并输入以下行：

```console
$ rustc --version
```

你应该看到已发布的最新稳定版本的版本号、提交哈希和提交日期，格式如下：

```text
rustc x.y.z (abcabcabc yyyy-mm-dd)
```

如果你看到这些信息，说明你已成功安装 Rust！如果没有看到这些信息，请按以下方式检查 Rust 是否在你的 `%PATH%` 系统变量中。

在 Windows CMD 中，使用：

```console
> echo %PATH%
```

在 PowerShell 中，使用：

```powershell
> echo $env:Path
```

在 Linux 和 macOS 中，使用：

```console
$ echo $PATH
```

如果一切都正确但 Rust 仍然无法工作，有很多地方可以获得帮助。在[社区页面][community]上了解如何与其他 Rustaceans（我们自称的一个有趣昵称）取得联系。

### 更新和卸载

通过 `rustup` 安装 Rust 后，更新到新发布的版本很容易。在你的 shell 中运行以下更新脚本：

```console
$ rustup update
```

如果需要卸载 Rust 和 `rustup`，在 shell 中运行以下卸载脚本：

```console
$ rustup self uninstall
```

<!-- Old headings. Do not remove or links may break. -->
<a id="local-documentation"></a>

### 本地文档

Rust 的安装还包含文档的本地副本，这样你就可以离线阅读它。运行 `rustup doc` 在浏览器中打开本地文档。

任何时候，当标准库提供了一个类型或函数，而你不确定它的作用或用法时，请使用应用程序编程接口（API）文档来找出答案！

<!-- Old headings. Do not remove or links may break. -->
<a id="text-editors-and-integrated-development-environments"></a>

### 使用文本编辑器和 IDE

本书对你用什么工具编写 Rust 代码不做任何假设。几乎任何文本编辑器都能胜任！许多文本编辑器和集成开发环境（IDE）都内置了对 Rust 的支持。你总是可以在 Rust 网站的[工具页面][tools]上找到编辑器和 IDE 的列表。

### 离线使用本书

在一些示例中，我们将使用标准库之外的 Rust 包。要完成这些示例，你需要有互联网连接，或者提前下载这些依赖项。要提前下载依赖项，你可以运行以下命令。（我们稍后会详细解释 `cargo` 是什么以及这些命令各自的作用。）

```console
$ cargo new get-dependencies
$ cd get-dependencies
$ cargo add rand@0.8.5 trpl@0.2.0
```

这将缓存这些包的下载，这样你以后就不需要下载它们了。一旦运行了这个命令，你就不需要保留 `get-dependencies` 文件夹了。如果你运行了这个命令，你可以在本书其余部分的所有 `cargo` 命令中使用 `--offline` 标志来使用这些缓存的版本，而不是尝试使用网络。

[otherinstall]: https://forge.rust-lang.org/infra/other-installation-methods.html
[install]: https://www.rust-lang.org/tools/install
[msvc]: https://rust-lang.github.io/rustup/installation/windows-msvc.html
[community]: https://www.rust-lang.org/community
[tools]: https://www.rust-lang.org/tools
