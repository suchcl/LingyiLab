###windows版本的下载地址

windows版本的下载地址，切记：

<fontcolor="#f20">https://github.com/git-for-windows/git</font>

不要从官网上去找，官网上只有最新的版本。最新的版本，有着比较新的特性，但是我们使用的gitlab服务器没有更新到最新版本的时候，需要配置一些东西，感觉没有必要，就找一个旧一点的git版本使用吧。

### mac安装git

Mac，默认已经安装了git，不需要安装，如果想自己安装的话，可以通过Homebrew去安装。

```bash
brewinstallgit
```

### 检查git是否安装成功

无论windows还说 mac，安装了git后，可以通过在终端执行git指令在检测git是否安装成功

```bash
xxx@xxxx ~ % git
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone             Clone a repository into a new directory
   init              Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add               Add file contents to the index
   mv                Move or rename a file, a directory, or a symlink
   restore           Restore working tree files
   rm                Remove files from the working tree and from the index
   sparse-checkout   Initialize and modify the sparse-checkout

examine the history and state (see also: git help revisions)
   bisect            Use binary search to find the commit that introduced a bug
   diff              Show changes between commits, commit and working tree, etc
   grep              Print lines matching a pattern
   log               Show commit logs
   show              Show various types of objects
   status            Show the working tree status

grow, mark and tweak your common history
   branch            List, create, or delete branches
   commit            Record changes to the repository
   merge             Join two or more development histories together
   rebase            Reapply commits on top of another base tip
   reset             Reset current HEAD to the specified state
   switch            Switch branches
   tag               Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch             Download objects and refs from another repository
   pull              Fetch from and integrate with another repository or a local branch
   push              Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```
在执行了git指令后，只要出现了类似的信息，就表示git已经安装成功，就可以使用git了。

