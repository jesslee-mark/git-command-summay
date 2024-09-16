# Git系列技术文档总结

#### Git系列介绍
git常用命令含义用法选项示例详解


1. [【git系列】git-add 含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681865228)
2. [【git系列】git-commit含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681865407)
3. [【git系列】 git-clone含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681891267)
4. [【git系列】git-pull 含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681853996)
5. [【git系列】git push含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681893299)
6. [【git系列】git merge含义用法选项示例详解](https://zhuanlan.zhihu.com/p/693932900)
7. [【git系列】git-revert含义用法选项示例详解](https://zhuanlan.zhihu.com/p/694784138)
8. [【git系列】git restore含义用法选项示例详解](https://zhuanlan.zhihu.com/p/694909148)
9. [【git系列】git switch含义用法选项示例详解](https://zhuanlan.zhihu.com/p/694808166)
10. [【git系列】git rebase含义用法选项示例详解](https://zhuanlan.zhihu.com/p/694919552)
11. [【git系列】git remote含义用法选项示例详解](https://zhuanlan.zhihu.com/p/694960607)
12. [【git系列】git-branch 含义用法选项示例详解](https://zhuanlan.zhihu.com/p/719637118)




![img](https://picx.zhimg.com/80/v2-60db15c2daaab221a4422485d43ef982_720w.png?source=d16d100b)



## [【git系列】 git-clone含义用法选项示例详解](https://zhuanlan.zhihu.com/p/681891267)

*源自专栏《*[*Gradle ScalaTest markdown idea Git中文实用教程目录*](https://zhuanlan.zhihu.com/p/679330466)*?》*

## 描述

git clone命令用于将**存储库克隆到一个新目录**中。

它会创建一个新的目录，并在其中克隆指定的存储库。该命令还会为**克隆的存储库的每个分支创建远程跟踪分支**（可以使用git branch --remotes查看），并创建和检出一个从克隆存储库当前活动分支派生的初始分支。

在克隆之后，执行git fetch命令（不带参数）将更新所有远程跟踪分支，执行git pull命令（不带参数）将合并远程主分支到当前主分支（如果有的话）。这是默认配置，通过在refs/remotes/origin下创建对远程分支头的引用，并初始化remote.origin.url和remote.origin.fetch配置变量来实现。

## 语法

```
git clone [--template=<template-directory>]
      [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
      [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
      [--dissociate] [--separate-git-dir <git-dir>]
      [--depth <depth>] [--[no-]single-branch] [--no-tags]
      [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
      [--[no-]remote-submodules] [--jobs <n>] [--sparse] [--[no-]reject-shallow]
      [--filter=<filter> [--also-filter-submodules]] [--] <repository>
      [<directory>]
```

## 示例

1.  克隆一个存储库：    shell    $ git clone <repository>    这将克隆指定的存储库到当前目录中，并在新创建的目录中初始化一个Git存储库。 
2.  克隆指定分支的存储库：    shell    $ git clone -b <branch> <repository>    这将克隆指定分支的存储库。 
3.  克隆具有限深度的存储库：    shell    $ git clone --depth <depth> <repository>    这将以指定的深度克隆存储库，仅包含最近的个提交。 
4.  从上游克隆： 

$ git clone git://git.kernel.org/pub/scm/.../linux.git my-linux    $ cd my-linux    $ make

1. 在不检出任何内容的情况下，创建一个借用当前目录的本地克隆：

$ git clone -l -s -n . ../copy    $ cd ../copy    $ git show-branch

1. 在借用现有本地目录的同时，从上游克隆：

$ git clone --reference /git/linux.git \     git://git.kernel.org/pub/scm/.../linux.git \     my-linux    $ cd my-linux

1. 创建一个裸仓库以发布您的更改给公众：

$ git clone --bare -l /home/proj/.git /pub/scm/proj.git

总之，git clone命令用于将存储库克隆到一个新的目录中。可以使用不同的选项来自定义克隆过程。

## 简化选项

以下是一些常用的git clone命令选项：

- --template=<template-directory>：指定模板目录，该目录中的文件和目录将被复制到新的存储库中。
- -b <name>：指定要克隆的分支名称。
- --depth <depth>：指定克隆的深度，即克隆历史记录的最大提交数量。
- --single-branch：只克隆指定的分支，而不是克隆整个存储库。
- --no-tags：不克隆标签。
- --recurse-submodules：递归地克隆子模块。
- --jobs <n>：指定并发克隆的作业数。

## 全部选项

### -l, --local

当要克隆的仓库位于本地机器上时，此选项绕过正常的"Git aware"传输机制，并通过复制HEAD和objects以及refs目录下的所有内容来克隆仓库。.git/objects/目录下的文件在可能的情况下采用硬链接以节省空间。

如果将仓库指定为本地路径（例如，/path/to/repo），则这是默认设置，--local实际上是一个无操作。如果将仓库指定为URL，则此选项将被忽略（我们不会使用本地优化）。指定--no-local将覆盖使用常规的Git传输而不是给出/path/to/repo时的默认设置。

如果仓库的$GIT_DIR/objects具有符号链接或者是符号链接，克隆将失败。这是一种安全措施，以防止意外解引用符号链接而复制文件。

注意：此操作与对源仓库进行并发修改类似，类似于在修改src时运行cp -r src dst。

### --no-hardlinks

强制从本地文件系统上的仓库中复制.git/objects目录下的文件，而不是使用硬链接。如果您想备份您的仓库，这可能是有用的。

### -s, --shared

当要克隆的仓库位于本地机器上时，自动设置.git/objects/info/alternates以与源仓库共享对象，而不是使用硬链接。结果仓库一开始没有任何自己的对象。

注意：这是一个可能危险的操作；除非您了解其作用，请不要使用它。如果使用此选项克隆您的仓库，然后删除分支（或使用任何使任何现有提交不可引用的Git命令），则某些对象可能变得不可引用（或悬空）。这些对象可能会被正常的Git操作（例如git commit）删除，该操作会自动调用git maintenance run --auto（参见git-maintenance[1]）。如果这些对象被删除且被克隆仓库引用，则克隆仓库将变得损坏。

请注意，在使用--shared选项克隆的仓库中运行git repack而不带--local选项时，会将来自源仓库的对象复制到克隆仓库中的pack文件中，从而移除了使用clone --shared的磁盘空间节省。但是，运行git gc是安全的，默认情况下它使用--local选项。

如果要打破使用--shared克隆的仓库对源仓库的依赖关系，只需运行git repack -a，将所有对象从源仓库复制到克隆仓库的pack文件中。

### --reference[-if-able] <repository>

如果参考仓库位于本地机器上，则自动设置.git/objects/info/alternates以从参考仓库获取对象。使用已经存在的仓库作为参考将需要从正在克隆的仓库复制更少的对象，从而减少网络和本地存储成本。当使用--reference-if-able时，如果不存在指定的目录，则跳过并发出警告，而不是中止克隆。

注意：请参阅--shared选项的注释，以及--dissociate选项。

### --dissociate

只借用--reference选项指定的参考仓库的对象来减少网络传输，并在完成克隆后通过进行必要的本地对象副本制作来停止从它们借用。当从已经从另一个仓库借用对象的仓库进行本地克隆时，也可以使用此选项 - 新仓库将从同一仓库借用对象，并且可以使用此选项来停止借用。

### -q, --quiet

静默操作，不向标准错误流报告进度状态。

### -v, --verbose

详细运行。不会影响将进度状态报告给标准错误流。

### --progress

默认情况下，如果标准错误流连接到终端，则在标准错误流上报告进度状态，除非指定了--quiet。该选项强制报告进度状态，即使标准错误流未定向到终端。

### --server-option=<option>

在使用协议版本2进行通信时，将给定的字符串传输给服务器。给定的字符串不能包含NUL或LF字符。服务器对服务器选项的处理（包括未知选项）是特定于服务器的。当给出多个--server-option=<option>时，它们按照命令行上列出的顺序全部发送到另一侧。

### -n, --no-checkout

克隆完成后不执行HEAD的检出操作。

### --[no-]reject-shallow

如果源仓库是一个浅仓库，则失败。可以使用clone.rejectShallow配置变量指定默认设置。

### --bare

创建一个裸Git仓库。也就是说，不是在中创建.git目录并放置管理文件，而是将本身作为$GIT_DIR。这显然意味着--no-checkout，因为没有地方可以检出工作树。此外，远程的分支头将直接复制到相应的本地分支头，而不是将其映射到refs/remotes/origin/。当使用此选项时，不会创建remote-tracking分支和相关的配置变量。

### --sparse

使用稀疏检出，最初只有顶级目录中的文件存在。可以使用git-sparse-checkout[1]命令根据需要扩展工作目录。

### --filter=<filter-spec>

使用部分克隆功能，并请求服务器根据给定的对象过滤器发送一组可达对象的子集。使用--filter时，提供的将用于部分克隆过滤器。例如，--filter=blob:none将在Git需要时过滤掉所有blob（文件内容）。另外，--filter=blob:limit=<size>将过滤掉大小至少为的所有blob。有关过滤器规范的更多详细信息，请参阅git-rev-list[1]中的--filter选项。

### --also-filter-submodules

还将部分克隆过滤器应用于仓库中的任何子模块。需要--filter和--recurse-submodules。可以通过设置clone.filterSubmodules配置选项来默认开启此功能。

### --mirror

设置源仓库的镜像。这意味着--bare。与--bare相比，--mirror不仅将源的本地分支映射到目标的本地分支，还映射所有引用（包括远程跟踪分支、注释等），并设置了一个refspec配置，以便在目标仓库中通过git remote update覆盖所有这些引用。

### -o <name>, --origin <name>

不使用remote名称origin来跟踪上游仓库，而是使用。这将覆盖配置中的clone.defaultRemoteName。

### -b <name>, --branch <name>

不将新创建的HEAD指向克隆仓库的HEAD所指向的分支，而是指向分支。在非裸仓库中，这将是要检出的分支。--branch还可以接受标签，并将HEAD分离到结果仓库中的该提交。

### -u <upload-pack>, --upload-pack <upload-pack>

如果给定，并且要克隆的仓库通过ssh访问，则指定在远程端运行的非默认路径的命令。

### --template=<template-directory>

指定要使用的模板目录；（参见git-init[1]中的"TEMPLATE DIRECTORY"部分）。

### -c <key>=<value>, --config <key>=<value>

在新创建的仓库中设置配置变量；此操作在初始化仓库后立即生效，但在获取远程历史记录或检出任何文件之前。键与git-config[1]期望的格式相同（例如，core.eol=true）。如果为同一个键提供了多个值，则每个值都将写入配置文件。这使得它是安全的，例如，向origin远程添加其他fetch refspecs。

由于当前实现的限制，某些配置变量在初始获取和检出之后才生效。已知不会生效的配置变量有：remote.<name>.mirror和remote.<name>.tagOpt。请改为使用--mirror和--no-tags选项。

### --depth <depth>

创建一个浅克隆，历史记录被截断为指定数量的提交。除非给出--no-single-branch来获取所有分支附近的历史记录，否则默认为--single-branch。如果要浅克隆子模块，请同时传递--shallow-submodules。

### --shallow-since=<date>

创建一个浅克隆，历史记录在指定时间之后。

### --shallow-exclude=<revision>

创建一个浅克隆，历史记录中排除从指定的远程分支或标签可达的提交。此选项可以多次指定。

### --[no-]single-branch

仅克隆到单个分支的末端历史记录，可以通过--branch选项或主分支remote的HEAD指向来指定。对结果仓库的进一步获取将仅更新使用此选项进行初始克隆的分支的远程跟踪分支。如果远程的HEAD在进行--single-branch克隆时不指向任何分支，则不会创建远程跟踪分支。

### --no-tags

不克隆任何标签，并在配置中设置remote.<remote>.tagOpt=--no-tags，确保未来的git pull和git fetch操作不会跟随任何标签。随后的显式标签获取仍然有效（请参阅git-fetch[1]）。

可以与--single-branch结合使用，以克隆和维护仅有一个克隆分支以外没有其他引用的分支。例如，对于某些仓库的默认分支进行最小克隆以供搜索索引使用。

### --recurse-submodules[=<pathspec>]

创建克隆后，在基于提供的路径规范的子模块中初始化和克隆。如果没有提供路径规范，则初始化和克隆所有子模块。此选项可以多次给出，用于由多个条目组成的路径规范。结果克隆的submodule.active设置为所提供的路径规范，或者如果未提供路径规范，则为"."（表示所有子模块）。

子模块使用其默认设置进行初始化和克隆。这相当于在克隆完成后立即运行git submodule update --init --recursive <pathspec>。如果克隆的仓库没有工作树/检出（即，如果传递了任何--no-checkout/-n，--bare或--mirror），则忽略此选项。

### --[no-]shallow-submodules

所有被克隆的子模块将是浅层的，深度为1。

### --[no-]remote-submodules

所有被克隆的子模块将使用子模块的远程跟踪分支的状态来更新子模块，而不是使用超级项目记录的SHA-1。等效于在git submodule update中传递--remote。

### --separate-git-dir=<git-dir>

将克隆仓库放置在指定的目录，而不是放在其应该的位置，然后在那里创建一个与文件系统无关的Git符号链接。结果是Git仓库可以与工作树分离。

### -j <n>, --jobs <n>

同时获取的子模块数。默认为submodule.fetchJobs选项的值。

### <repository>

要克隆的（可能是远程的）仓库。有关指定仓库的更多信息，请参见下面的GIT URLS部分。

### <directory>

要克隆到的新目录的名称。如果没有明确指定目录，则使用源仓库的“humanish”部分（/path/to/repo.git的repo和host.xz:foo/.git的foo）。只有目录为空时才允许将克隆放在现有目录中。

### --bundle-uri=<uri>

从远程获取之前，从给定的<uri>获取一个bundle，并将数据解包到本地仓库。bundle中的引用将存储在隐藏的refs/bundle/*命名空间下。此选项与--depth、--shallow-since和--shallow-exclude不兼容。

## GIT URLS

一般来说，URL包含有关传输协议、远程服务器地址和仓库路径的信息。根据传输协议的不同，可能会缺少其中的一些信息。

**Git支持ssh、git、http和https协议**（另外，可以使用ftp和ftps进行获取，但这是低效且已被弃用的，请不要使用它们）。

本地传输（即git:// URL）不进行身份验证，应谨慎在未安全网络上使用。

以下语法可与它们一起使用：

```
ssh：//[user@]host.xz[:port]/path/to/repo.git/

git：//host.xz[:port]/path/to/repo.git/

http[s]：//host.xz[:port]/path/to/repo.git/

ftp[s]：//host.xz[:port]/path/to/repo.git/
```

还可以使用类似scp的语法与ssh协议一起使用：

[user@]host.xz:path/to/repo.git/

只有在第一个冒号之前没有斜杠时才会识别此语法。这有助于区分包含冒号的本地路径。例如，本地路径foo:bar可以指定为绝对路径或./foo:bar以避免被解释为ssh url。

ssh和git协议还支持~username扩展：

```
ssh：//[user@]host.xz[:port]/~[user]/path/to/repo.git/

git：//host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/
```

对于本地仓库，Git原生支持以下语法：

```
/path/to/repo.git/

file：///path/to/repo.git/
```

这两种语法基本上是等效的，只是前者暗示了--local选项。

git clone、git fetch和git pull，但不包括git push，也可以接受适当的捆绑文件。请参阅git-bundle[1]。

当Git不知道如何处理某个传输协议时，它会尝试使用remote-远程助手（如果存在）。为了显式请求远程助手，可以使用以下语法：

::

其中

可以是路径、服务器和路径，或特定远程助手可识别的任意类似URL的字符串。有关详细信息，请参阅git-remote-helpers[7]。 

如果有大量具有类似名称的远程仓库，并且您想为它们使用不同的格式（使您使用的URL将被重写为有效的URL），可以创建以下形式的配置部分：

```
[url "<actual url base>"]
    insteadOf = <other url base>
```

例如，使用以下内容：

```
[url "git://git.host.xz/"]
    insteadOf = host.xz:/path/to/
    insteadOf = work:
```

像"work:repo.git"或"host.xz:/path/to/repo.git"这样的URL将在任何需要URL的上下文中被重写为"git://git.host.xz/repo.git"。

如果您只想重写推送的URL，可以创建以下形式的配置部分：

```
[url "<actual url base>"]
    pushInsteadOf = <other url base>
```

例如，使用以下内容：

```
[url "ssh://example.org/"]
    pushInsteadOf = git://example.org/
```

像"git://example.org/path/to/repo.git"这样的URL将在推送时被重写为"ssh://example.org/path/to/repo.git"，但拉取仍将使用原始URL。

## 配置

以下是此部分中包含的来自git-config[1]文档的选择性内容。

内容与文档中相同：

-  init.templateDir    指定将从中复制模板的目录。（参见git-init[1]中的"TEMPLATE DIRECTORY"部分。） 
-  init.defaultBranch   允许覆盖默认的分支名称，例如在初始化新仓库时。 
-  clone.defaultRemoteName   克隆仓库时要创建的远程名称。默认为origin，并且可以通过传递--origin命令行选项给git-clone[1]进行覆盖。 
-  clone.rejectShallow   拒绝克隆浅仓库；可以通过在命令行上使用--reject-shallow选项来覆盖此设置。参见git-clone[1]。 
-  clone.filterSubmodules   如果提供了部分克隆过滤器（参见git-rev-list[1]中的--filter），并且使用了--recurse-submodules选项，则还将过滤器应用于子模块。 

  
