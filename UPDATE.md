$ git log
commit 53507fc2ac6098dd9b686380c28d168e2064ee5d (HEAD -> main)
Author: Anthony <9422677027@qq.com>
Date:   Wed Jun 1 16:54:40 2022 +0800

    Second commit @ 2022年6月1日 16:54:32 周三 Wednesday

commit 833319d698e6a1cf5a1a2638b8e1670f6120bd1c
Author: 4th-August <942267027@qq.com>
Date:   Mon May 30 17:16:30 2022 +0800

    first commit

----------------------

add content:

$ git log
commit b154b366b8fcc56c3c7b817378526ba5653e6565 (HEAD -> main)
Author: Anthony <9422677027@qq.com>
Date:   Wed Jun 1 17:58:12 2022 +0800

    add contents 6,8,9 and so on .

----------------------

当退回到某个提交的版本以后，再通过 git log 是无法显示在这之后的提交信息的。但是>，通过 git reflog 可以获取到操作命令的历史。

执行命令：git log 可以查看提交的信息
$ git log
b154b36 (HEAD -> main) HEAD@{0}: reset: moving to b154b36
b154b36 (HEAD -> main) HEAD@{1}: reset: moving to b154b36
b154b36 (HEAD -> main) HEAD@{2}: commit: add contents 6,8,9 and so on .
53507fc HEAD@{3}: commit: Second commit @ 2022年6月1日 16:54:32 周三 Wednesday
833319d HEAD@{4}: Branch: renamed refs/heads/master to refs/heads/main
833319d HEAD@{6}: commit (initial): first commit

这HEAD@{0}: HEAD@{1}: HEAD@{2}: HEAD@{3}: HEAD@{4}: HEAD@{6}: 前面的部分
b154b36 、 53507fc 和 833319d 都是 "commit_id"，即提交版本的ID，然后通过
git reset --hard 833319d 来回到 833319d 对应的历史版本

想要回到未来的某个提交，先通过 git reflog 从历史命令中找到想要回到的提交版
本的 ID，然后通过 git reset --hard 来切换。

    git reflog
    git reset --hard 'commit_id'

----------------------

at 2022年6月1日 18:56:35 Wednesday

solve a problem:

$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        "e \357\200\242git push\357\200\242 to publish your local commits)"
        tatus

nothing added to commit but untracked files present (use "git add" to track)


----------------------

2022年6月1日 18:50:30 Wednesday

flowing add sections:

commit 3e9fd48d112f8c8d272178ed499f3eeb5217f47b (HEAD -> main, origin/main)
Author: Anthony <9422677027@qq.com>
Date:   Wed Jun 1 18:32:24 2022 +0800

    The fourth update commit message, add contents>>UPDATE.md 6~9

commit b154b366b8fcc56c3c7b817378526ba5653e6565
Author: Anthony <9422677027@qq.com>
Date:   Wed Jun 1 17:58:12 2022 +0800

    add contents 6,8,9 and so on .

commit 53507fc2ac6098dd9b686380c28d168e2064ee5d
Author: Anthony <9422677027@qq.com>
Date:   Wed Jun 1 16:54:40 2022 +0800

    Second commit @ 2022年6月1日 16:54:32 周三 Wednesday

commit 833319d698e6a1cf5a1a2638b8e1670f6120bd1c
Author: 4th-August <942267027@qq.com>
Date:   Mon May 30 17:16:30 2022 +0800

    first commit
:

----------------------

6. 版本回退

有了 git log 来查看提交的历史记录，我们就可以通过 git reset --hard 来回退到我们需要的特定版本，然后使用当时的代码进行各种操作。

    git reset --hard HEAD^        // 回退到上一个提交版本
    git reset --hard HEAD^^        // 回退到上上一个提交版本
    git reset --hard 'commit_id'    // 会退到 commit_id 指定的提交版本

7. 回到未来的某个提交

当退回到某个提交的版本以后，再通过 git log 是无法显示在这之后的提交信息的。但是，通过 git reflog 可以获取到操作命令的历史。

因此，想要回到未来的某个提交，先通过 git reflog 从历史命令中找到想要回到的提交版本的 ID，然后通过 git reset --hard 来切换。

    git reflog
    git reset --hard 'commit_id'

8. 撤销修改

撤销修改同样包括两方面的内容，由于仓库中的文件在提交之前，可能在工作区中，尚未在版本控制范围内，也可能在暂存区中。

8.1 丢弃工作区中文件的修改

    git checkout -- Readme.md    // 如果 Readme.md 文件在工作区，则丢弃其修改
    git checkout -- .            // 丢弃当前目录下所有工作区中文件的修改

    注意： git checkout -- 中的 -- 是必须的。

8.2 丢弃已经进入暂存区的修改

git reset HEAD Readme.md // 将 Readme.md 恢复到 HEAD 提交版本的状态

9. 删除文件

在文件未添加到暂存区之前，对想删除文件可以直接物理删除。或者通过 git checkout -- file 来丢弃。如果文件已经被提交，则需要 git rm 来删除：

git rm Readme.md // 删除已经被提交过的 Readme.md

    注意： git rm 只能删除已经提交到版本库中的文件。其他状态的文件直接用这个命令操作是出错的。

git rm 与 先 rm 然后 git add 的区别

更详细的可以参考："git rm" 和 "rm" 的区别

    注意：上图中的结果是在 git 1.9.1 版本上的操作。在 git 2.0 以上两者没有区别了。

---------------------




