# Commit messages guide

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

本教程旨在展现提交信息(commit message)的重要性, 以及如何编写好的提交信息.

接下来会提到什么是提交(commit), 为什么好的提交信息很重要, 一些实践以及书写好的提交历史纪录的建议.

## 翻译

- [English](README.md)
- [Português](README_pt-BR.md)
- [Deutsch](README_de-DE.md)
- [中文](README_zh_CN.md)

## 什么是"提交"(commit)?

简而言之, 一次提交是对你本地文件的一个 _快照(snapshot)_, 它被记录在你本机的仓库里.
与一些人认为的不同, [git 不是只储存不同版本文件之间的差异, 它储存了所有文件的全部版本.](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
对于在没有变更的文件, git仅储存一个指向之前版本的相同文件的链接.

这幅图展示了git如何储存数据, 每个版本(Version)是一次提交.

![](https://i.stack.imgur.com/AQ5TG.png)

## 为什么提交信息是重要的?

- 为了提高速度以及streamline形式的代码审查
- 帮助人理解一次修改
- 解释代码所不能准确描述的"为什么"
- 帮助未来的开发者搞清楚为/什么改变被做出, 更简单地发现问题以及debug
  
 为了最大化学习效果, 在接下来的部分我们通过一些好的例子以及标准化的描述来进行学习.

## 好的例子/实践

从我的亲身经历, 网络文章以及其他指南中, 我收集了许多例子. 如果你有其他的(或者不同意其中一些), 请 pull request.

### 用祈使句形式

```
# 好的
Use InventoryBackendPool to retrieve inventory backend
```

```
# 不好的
Used InventoryBackendPool to retrieve inventory backend
```

_为什么使用祈使句?_

提交信息描述了这次提交/改变实际上做了什么以及它的效果, 不是你做了什么.

[Chris Beams 的文章](https://chris.beams.io/posts/git-commit/) 提供了可以帮助我们更好地写祈使句形式的提交信息的简单句.

```
如果通过/被应用, 这次提交将会 <提交信息>
```

(//译者: 好的提交信息要能完美地嵌套进上面那个句子里.)

例子: 

```
# 好的
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# 坏的
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 首字母大写

```
# 好的
Add `use` method to Credit model
```

```
# 坏的
add `use` method to Credit model
```

根据语法规则, 句子的首字母要大写.

也许不同的人/团队/语言 采纳或不采纳这条建议. 首字母大写与否, 重要的是要保持前后一致(若大写便坚持大写).

### 提供足够的信息, 使人不需要参考源代码就能理解commit


```
# 好的
Add `use` method to Credit model

```

```
# 坏的
Add `use` method
```

```
# 好的
Increase left padding between textbox and layout frame
```

```
# 坏的
Adjust css
```

在许多情景下, 例如有许多提交/重构, 帮助其他人理解提交者是怎么想的往往很有用/比较.

### 在信息正文里解释 "why"原因, "for what"目的, "how"如何 和其他细节

提交信息有标题(summary)和正文(description), 把细节的内容写在正文里.

```
# 好的
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# 好的
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# 好的
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

用空行分开信息的主题和正文. 信息的正文包括额外的空行. 

`-`, `*`, `\`等符号可以帮助提升可读性

### 避免太宽泛或者没有内容的信息

```
# 坏的
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 控制列数

[这篇文章](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)建议大家最提不要超过50字符, 正文不要超过72字符.

### 保持语言的一致性

对于项目拥有者: 选择一种语言然后所有提交信息都用这种语言. 最理想的情况下, 它应该与代码注释一致, 默认根据地方翻译(对于地方性的项目).

对于贡献者来说: 用与提交历史中相同的语言来写你的提交信息.

```
# 好的
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# 好的 (葡萄牙语)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# 不好的 (混合英语与葡萄牙语)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### 模板

这里有一个模板, [最初是 Tim Pope 写的](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), 后来出现在 [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)中.

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

```
用50个或者更少的字母来总结修改.

如果需要更多细节的解释, 简写到大约72个字母. 在一些情境下, 第一行被看作提交的主题, 其余的文字是正文. 用空行把总结和正文分开. (除非你完全忽略正文); 同时使用一些工具, 比如`log`, `shortlog`, `rebase`, 可能会使人跟到困惑.

解释这次提交解决的问题. 聚焦于你问什么要这么做而不是如何做(代码解释了这一点). 这次更改有边缘效应(side effect)或者其他意料之外的情况吗(unintuitive consequences)? 在正文中解释它们.

如果有更多的段落, 用空行分隔开.

 - 分点是可以的

 - 一般破折号或者星号被用来作为分点的标志, 前面空一格, 根据情况用空行分隔.

如果你解决了一个issue, 在最下面引用它一下, 像这样,

解决: #123
See also: #456, #789
```

## Rebase vs. Merge

这一节是对 Atlassian的教程["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)的一个总结.

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

总结: 将你的分支的多个提交, _一个一个_ 的应用到原始的分支, 生成一个新的tree.

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

总结: 创建一个新的提交, 叫做 _合并提交(merge commit)_, 其中包含两个分支的不同(differences).

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 为什么有些人更喜欢 rebase?

我更喜欢 rebase 而不是 merge. 原因包括:

* 它生成一个"干净(clean)"的历史纪录, 没有不必要的合并提交
* _所见即所得_, 在代码审查中, 所有变更都师出有名(来自特定的有题目的提交), 避免将变更隐藏在合并提交中.
* 许多合并可以被提交者分解, 每个合并变更都在一个有充足/合适信息的提交里
  * 人们往往不会深入研究合并提交, 所以避免merge确保了所有变更(change)都有一个自己的提交(commit)

### 什么时候压缩提交(squash)?

"压缩提交"是指将一系列的提交压缩为一个提交.

它在许多情况下很有用, 例如

- 减少提交没有什么信息的提交(修改错字, 格式, 忘掉的东西)
- 在提交时, 将单独的变更联合起来往往更有意义
- 重复写 _正在进行的工作_ 的提交.

### 什么时候避免rebase或squash?

在公共提交或者许多人一起工作的共享的分支中避免rebase.

## 实用的 git 指令

### rebase -i

用它去压缩提交, 编辑信息, 重写/删除 提交, 或者改变顺序.

```
pick 002a7cc Improve description and update document title
pick 897f66d Add contributing section
pick e9549cf Add a section of Available languages
pick ec003aa Add "What is a commit" section"
pick bbe5361 Add source referencing as a point of help wanted
pick b71115e Add a section explaining the importance of commit messages
pick 669bf2b Add "Good practices" section
pick d8340d7 Add capitalization of first letter practice
pick 925f42b Add a practice to encourage good descriptions
pick be05171 Add a section showing good uses of message body
pick d115bb8 Add generic messages and column limit sections
pick 1693840 Add a section about language consistency
pick 80c5f47 Add commit message template
pick 8827962 Fix triple "m" typo
pick 9b81c72 Add "Rebase vs Merge" section

# Rebase 9e6dc75..9b81c72 onto 9e6dc75 (15 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into the previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
# 这些行的顺序可以改变, 它们被从上到下执行的
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# 如果你删除这里的任一行, 提交将会缺失.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

#### fixup

