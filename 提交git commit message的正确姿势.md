# 1、触发事件
我有这样一个版本库，里面包含两个学习用的练习项目：BookStore（以下简称BS）和PictureFriend（以下简称PF）<br>

我在更改PF以后，未进行提交，同时又到BS中优化了一下文件夹结构，然后此时我commit，提交备注信息为“添加图友网项目，更改为Maven形式，报错找不到spring监听器，待解决”，提交成功，似乎没什么问题。<br>

但是当我在github上看到的情况如下，我知道我没有处理好：<br>
<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/gitCommit_badExample.png" width="700"  /><br>

BookStore项目实际上跟这个备注并没有关系，而是PictureFriend才主要是这次commit的内容，只是因为我将两个项目的操作在同一次commit中进行提交，造成了这样的情况。可见如果是正式的项目，如此的提交是多么混乱，他人将难以维护和修改。<br>

究其原因，主要还是在正确的git提交姿势上知之甚少：
1. 不同的要分别分次提交，（这里不同指 如：不同的修改类型//优化还是新增etc.//，不同的模块，不同的功能等）；
2. 提交的信息要进行一定程度的格式化。

---

# 2、知之为知之
commit的写法规范有很多，以下参考网络相关文章，并进行简化以定义个人风格。<br>

参考链接：
- [《阮一峰的网络日志：Commit message 和 Change log 编写指南》][1]
- [《写好 Git Commit 信息的 7 个建议》][2]

## 2.1 Commit message的格式化
每次提交，Commit message 都包括两个核心部分：**标题** 和 **内容**。
``` stylus
<类型>: <主题>
// 空一行
<内容>
```
<br>
其中，**标题 是必需的**，内容无需过多描述的话，正文内容部分可以省略。<br>

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。<br>

### 2.1.1 标题

标题部分只有一行，包括字段：**类型** 和 **主题**。<br>

**标题限制总字数在50个字符以内，以保证容易阅读。**<br>

e.g.

``` stylus
feat: init LearnGit.git

I got a wrong-style git commit, so I init a .git for learning
how to write a git commit message in right way.

And the last line just write here for a simple test,
it's useless acturally.
```
<br>

#### 2.1.1.1 类型
类型 用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动
<br>

#### 2.1.1.2 主题
主题 是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）
<br>
<br>

### 2.1.2 内容
内容部分是对本次 commit 的详细描述，可以分成多行，正文在 72 个字符处换行。<br>

使用正文解释是什么和为什么，而不是如何做，以及与以前行为的对比。

---

## 2.2 格式化后Commit message的好处
### 2.2.1 提供更多的历史信息，方便快速浏览

直接使用git log你得到的是：
<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git log.png" width="400"  /><br>

比如，下面的命令显示上次发布后的变动，每个commit占据一行。你只看行首，就知道某次 commit 的目的。

``` stylus
$ git log <last tag> HEAD --pretty=format:%s
```

<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git format.png" width="400"  /><br>

关于更多git log的输出格式，参考以下：
- [个性化你的 Git Log 的输出格式][3] 
<br>

### 2.2.2 可以过滤某些commit（比如文档改动），便于快速查找信息

比如，下面的命令仅仅显示feat类型的commit。

``` stylus
$ git log <last release> HEAD --grep feat
```
<br>
<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git grep.png" width="400"  /><br>

当然，你还可以这样：<br>
<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git format grep.png" width="400"  /><br>

关于更多过滤规则，参考以下：
- [5.3 Git log高级用法 过滤提交历史][4]
<br>

e.g.
<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git filter.png" width="400"  /><br>

<img src="https://github.com/deng-cc/LearnGit/raw/master/pics/git ignoreCase.png" width="400"  /><br>


  [1]: http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html
  [2]: http://blog.jobbole.com/92713/
  [3]: https://ruby-china.org/topics/939
  [4]: https://github.com/geeeeeeeeek/git-recipes/wiki/5.3-Git-log%E9%AB%98%E7%BA%A7%E7%94%A8%E6%B3%95#toc7