From: 011netservice@gmail.com
Date: 2025-04-21
Subject: git, github 備忘
File: https://github.com/github-honda/GitPratice/blob/main/readme-GitHub.txt
CodeHelper\GitHub\readme-GitHub.txt
歡迎來信交流, 訂購軟體需求.

以下 #### 標記段落, **** 標記常用(流程、設定、備忘)

#### 摘要
- 觀念
1. 工具軟體可以簡化某些 git 指令的輸入, 但是不同的工具軟體操作方式、名詞定義不一致, 容易造成混淆.
2. 以指令操作 git, 較能了解 git 的運作細節. 指令也可以編寫為 script 自動化執行.

- Resources:
  https://git-scm.com/ 本文使用這個工具 git-gui, 包含指令模式 git bash 工具 and Open source. 
    全新下載: 
	  https://git-scm.com/downloads, 2.49.0
	  https://git-scm.com/downloads/win, 2.49.0, 2025-04-21
	版本更新指令: 
	  winget install --id Git.Git -e --source winget, 更新 git-gui, git bash 工具
    $ git --version
      git version 2.39.0.windows.1, 2022-12-14
      git version 2.36.0.windows.1

  https://github.com/
  https://backlog.com/git-tutorial/tw/ 繁體中文(入門、進階、命令參考)
  https://git-scm.com/docs
  https://git-scm.com/download/gui/windows  推薦工具清單
  https://sourcetreeapp.com/  網路上最常使用的工具.


- 啟動執行方式:
  檔案總管選擇目錄後, 按滑鼠右鍵, 選擇 Git Bash Here 或 Git GUI here.

- git 檔案的三種狀態:
  Modified:  已修改. 檔案已修改.
  Staged:    已暫存. 檔案標記為已暫存修改, 可準備 commit 提交.
  Committed: 已提交. 檔案已存入本地資料庫.
  
- git 三個區域:
  Working Directory:        工作目錄. 在檔案系統中的工作目錄.
  Staging Area(Index Area): 暫存區 或 索引區. 儲存(可準備 commit 提交)的資訊.
  Repository:               儲存檔案變更的資料庫.

- HEAD 代表(目前最新的分支)的(最新 commit 的指標).


#### git command reference, 2025-04-21
*代表 常用
- CLI (Command-Line Interface) 指令下載及使用方式, 可參考 https://cli.github.com/ 
- 所有的指令均可以 Pipeline 將結果倒出為檔案, 例如: git diff --name-status d54a0b4 HEAD > c:\temp\ChangeList.txt

git command reference
 $ git            | git usage help.
*$ git --version  | 檢視 git 版本
*$ git add        | 將檔案加入(暫存區)管理. Add file contents to the index
 $ git add -A     | 同 git add --all
*$ git add --all  | 將檔案及路徑加入(暫存區)管理. Update the index not only where the working tree has a file matching <pathspec> but also where the index already has an entry. This adds, modifies, and removes index entries to match the working tree.
 $ git add --no-ignore-removal | 同 git add --all
*$ git add <file> | 將<file>加入(暫存區)管理.
*$ git add *.html | 將所有的.html檔案加入(暫存區)管理. 
*$ git add .      | 將資料夾中所有檔案加入(暫存區)管理. 不包含空目錄. 空目錄習慣上可以放一個.keep 或 .gitkeep 檔案後進行提交.
*$ git add . && git commit -m "Message" | 將資料夾中所有新檔案, 加入本地資料庫後, 再 Commit 目前所有的變更.
*$ git add <path> | 將<path>加入(暫存區)管理. 空目錄是無法被提交的. 空目錄習慣上可以放一個.keep 或 .gitkeep 檔案後進行提交.
*$ git add -f <file> | 將<file>加入(暫存區)管理. -f為忽略 .gitignore 設定.
*$ git add -f <path> | 將<path>加入(暫存區)管理. -f為忽略 .gitignore 設定.
 $ git archive -o latest.zip HEAD                                  | 取得目前分支的全部最新壓縮檔案. Create a Zip archive that contains the contents of the latest commit on the current branch. Note that the output format is inferred by the extension of the output file.
 $ git archive --remote=<repository URL> | tar -t                  | 取得遠端檔案, 不會clone, 也不會有本地目錄.git
 $ git archive --remote=<repository URL> | tar -t --exclude="*/*"  | 取得第一層遠端檔案 If you need folders and files just from the first level:
 $ git archive --remote=<repository URL> | tar -t --exclude="*/*"  | grep "/"   | 只取得第一層目錄清單 To list only first-level folders of a remote repo:
 $ git blame <file> | 查詢檔案修改內容.
 $ git blame -L <range> <file> | 查詢(<file> 第line_num_from列 到 line_num_to列)的修改.
 $ git blame -L 40,+1 <file>   | 查詢(<file> 第40列)的修改.
 $ git blame -L 40,+21 <file>  | 查詢(<file> 第40列到60列)的修改.
 $ git blame -L 40,60 <file>   | 查詢(<file> 第40列到60列)的修改.
 $ git blame -L 5,10 <file>    | 查詢(<file> 第5   到10列)的修改.
*$ git branch                  | 查詢本地分支. 標示為綠色*就是目前的分支.
*$ git branch <branch>         | 建立分支. 建立新分支後, 記得要切換到新分支(git checkout <branch>), 否則仍在原分支不變.
 $ git branch -d <branch>      | 刪除分支. 
 $ git branch -f <branch>      | Shortcut for --force. 
 $ git branch --force <branch> | 強制建立分支 Reset <branch> to <startpoint>, even if <branch> exists already.
 $ git branch -M <branch>      | Shortcut for --move --force 
 $ git branch -m <branch>      | Shortcut for --move
 $ git branch -m <branchOld> <branchNew> | 將本地分支 <branchOld> 改為 <branchNew> 
 $ git branch --move <branch>  | 修改分支名稱及相關的 reflog. Move/rename a branch and the corresponding reflog.
*$ git branch -r               | 查詢遠端分支.
*$ git branch --set-upstream-to=<RemoteBranch> <LocalBranch> | 設定本地分支與遠端分支的關聯. 執行 git pull 或 git push 時可不需要指定遠端分支. 
*$ git branch --set-upstream-to=origin/<branch> main         | 設定本地分支main與遠端分支origin/<branch>的關聯範例.
 $ git branch --show-current | 查詢目前本地分支, 建議使用 git branch 就好.
 $ git branch --unset-upstream [<branchname>]                | 取消本地分支與遠端分支的關聯
*$ git branch -vv | 檢視 upstream 設定, -vv = doubly verbose. 輸出綠色*代表本地分支, 藍色代表遠端分支. 範例: * master 28b359c1 [origin/master] CodeHelper memo. 以上綠色為(* master), 藍色為 origin/master.
 $ git checkout                   | 還原目前本地分支所有(已 commit)的檔案. Switch branches or restore working tree files
*$ git checkout <commitId> <file> | 還原(指定版本)的檔案.
*$ git checkout <branch>      | 切換到分支. Switch to a branch. 若分支不存在, 則錯誤訊息.
*$ git checkout -b <newBranch>      | 切換到新分支, 若新分支不存在, 則建立新分支.
 $ git checkout <file>            | 還原(已 commit)的檔案.
 $ git clean -f | 還原工作目錄檔案 Untracked files. -f=--force Cleans the working tree by recursively removing files that are not under version control, starting from the current directory.
 $ git clean -n | 查詢將被 git clean -f 還原的清單 Untracked files. -n=--dry-run Cleans the working tree by recursively removing files that are not under version control, starting from the current directory.
*$ git clone <url.git> | Clone/Fork 複製遠端資料庫 到 新子目錄(遠端資料庫名稱)中. Clone a repository into a new directory. 同一台電腦可將相同的遠端資料庫, 複製為多份各自獨立的版本, 互不影響.
*$ git clone https://github/com/git/git | 下載更新 git 軟體為最新版本, 若需要一併更新 git-gui, git bash 工具, 則應使用 winget install 指令. 
 $ git commit --amend --no-edit        | 將本次commit 併入最後一次 commit 中. --no-edit 代表不修改訊息.
*$ git commit --amend -m "Message" | 修改最後一次提交的訊息.
 $ git commit --signoff | Sign-off is requirement for getting patches into the Linux kernel, but most projects don't actually use it.
*$ git commit -a                       | 將變更存入本地資料庫, -a = All. 不包含未納入管理的檔案.
 $ git commit -a --alow-empty -m "Commit Message" | 沒有任何檔案變更卻執行提交.
 $ git commit -a --alow-empty-message  | 將變更存入本地資料庫, -a = All, 備註文字為空白.
*$ git commit -a -m "Message"      | 將變更存入本地資料庫, -a = All, -m 加入備註文字, 否則會要求輸入.
*$ git commit -m "Message" | Commit 目前變更進本地資料庫.
*$ git config -l | 檢視設定清單. 同 --list
*$ git config --list | 檢視設定清單.
 $ git config --global gc.reflogExpire 'never'            | 修改 reflog 保存時間 (存在分支線上，預設 90 天改為無限)
 $ git config --global gc.reflogExpireUnreachable 'never' | 修改 reflog 保存時間 (不存在分支線上，預設 30 天改為無限)
*$ git config --global init.defaultBranch main | 將預設(建立本地資料庫分支名稱)設為 main.
 $ git config --global user.email "you@example.com"
 $ git config --global user.name "Your Name"
 $ git diff <old commit id> <new commit id> | 查詢版本的差異.
*$ git diff --name-status <old commit id> <new commit id> | 查詢版本之間的檔案差異.(Added, Deleted, Modified, Renamed...)
*$ git diff --name-status HEAD | 取得 最新檔案變更差異清單. (Added, Deleted, Modified, Renamed...)
*$ git diff --name-status <old commit id> HEAD > c:\\temp\\ChangeList.txt | 取得 最新 與 指定版本 的檔案變更差異清單.(Added, Deleted, Modified, Renamed...)
*$ git fetch origin/master | 下載指定的分支, 但是不會 merge
*$ git help <command> | Help command. 輔助文件, 存放位置: C:\Program Files\Git\mingw64\share\doc\git-doc\index.html
 $ git help <concept> | Help concept. 例如: attributes, cli, core-tutorial...可從 git help -g 取得 concept 清單.
 $ git help -a        | Help available subcommands.
 $ git help -g        | Help concept guides. 
 $ git init --initial-branch=main | 同 git init -b main
*$ git init -b main | 建立本地資料庫, branch=main. 舊版預設建立 master branch, 新版Git 2.28.0(2020-10-01起)響應黑人平權運動, 將 master 改為 main. 
*$ git init         | 建立本地資料庫及預設branch=main. 
 $ git log                   | 查詢 commit 紀錄.
*$ git log --oneline --graph | 查詢 commit 紀錄.
*$ git log --oneline -n      | 查詢 commit 紀錄. n是最近提交的次數.
 $ git log --stat --summary  | 查詢 commit 紀錄. 狀態摘要明細.
*$ git log <file>  | 查詢(檔案 commit 紀錄). 建議使用 GitGui 比較容易檢視, 只要在log清單畫面上選擇檔案HighLight.
*$ git ls-files -s | 檔案清單, 包括GitMode, commit紀錄.
*$ git merge <branch> | 將<branch>合併入目前分支. 快轉合併 fast-forward 將 <banch>分支併入目前的分支.
*$ git merge <branch> --allow-unrelated-histories | 將<branch>合併入目前分支. 允許合併沒有共同祖先的分支. 
 $ git mv <file1> <file2> | 變更檔案名稱並將變更移到 Staging Area. 等於先( $ mv <file1> <file2>), 再 $ git add -A).
 $ git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…​] | 清理沒用的物件. 
 $ git prune | 清理沒用的物件. 例如: $ git prune $(cd ../another && git rev-parse --all) , To prune objects not used by your repository or another that borrows from your repository via its ".git/objects/info/alternates"
*$ git pull | 下載(預設遠端分支)到本地資料庫, 同時合併分支, git pull = fetch + merge. 
*$ git pull <RemoteBranch> <LocalBranch> | 下載(遠端分支<RemoteBranch>)到本地資料庫<LocalBranch>, 同時合併分支, git pull = fetch + merge. 例如: $ git pull origin master
*$ git push    | 上傳本地資料庫到預設的遠端資料庫. 預設遠端資料庫設定請參考 git branch --set-upstream-to
*$ git push -f | 強制上傳(本地資料庫)到(預設的遠端資料庫).
*$ git push <RemoteBranch> <LocalBranch> | 上傳本地資料庫LocalBranch到遠端資料庫RemoteBranch. 
*$ git push origin master                | 上傳本地資料庫master到遠端資料庫origin.
 $ git push origin master:master                | 上傳本地資料庫master:master到遠端資料庫origin. 預設遠端分支名稱與本地資料庫名稱相同.
 $ git push origin master:NewBranchNameInRemote | 上傳本地分支NewBranchNameInRemote到遠端資料庫origin. 同時建立或更新遠端的 NewBranchNameInRemote.
*$ git push --set-upstream origin main          | 上傳本地資料庫到預設的遠端資料庫. 同時指定預設遠端資料庫設定.
*$ git push -u origin master                    | 同 git push --set-upstream origin main, (-u 是 --set-upstream 的簡寫).
*$ git rebase <branch> | 將目前分支改以 <branch> 為準. 這個好用!
*$ git reflog            | 查詢 commit 紀錄. 包含 HEAD 移動紀錄. 例如 切換分支或還原版本). 預設保存90天的歷史紀錄, 不在分支線上的 commit, 則保存30天.
 $ git reflog --date=iso | 查詢 commit 紀錄.
*$ git remote                   | 查詢遠端分支清單. 
*$ git remote -v                | 查詢遠端分支清單, 內容包含(fetch 及 push)的遠端 .git 網址<uri>. 
*$ git remote add <name> <uri>  | 增加遠端分支<uri>. 習慣上命名 origin 為遠端數據庫. upstream 為遠端Forked數據庫.   
 $ git remote prune origin           | 清理無效檔案. 例如 github 已經刪除, 但是本地仍存在的檔案.
 $ git remote prune origin --dry-run | 列出要修剪的無效檔案. 不執行修剪.
*$ git remote update | 下載(全部分支)到本地資料庫, 不會 merge. 遠端資料庫若有多個分支變更檔案, 則應使用這個指令同時下載其他人的變更內容.
*$ git reset         | 還原到前一次的 Commit. 保留工作目錄已變更的檔案. --mixed 為預設的模式可以省略.
*$ git reset --hard  | 還原到前一次的 Commit. 放棄已變更的檔案 並恢復到目前分支的版本. --hard 為 放棄工作目錄已變更的檔案.
 $ git reset --mixed | 還原到前一次的 Commit. 保留工作目錄已變更的檔案. --mixed 為預設的模式可以省略. 
 $ git reset --soft  | 還原到前一次的 Commit. --soft 為 Does not touch the index file or the working tree at all (but resets the head to <commit>, just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.
 $ git reset HEAD    | HEAD 為預設. 同 git reset.
*$ git reset HEAD~   | 取消前一次的 Commit
 $ git reset HEAD^   | 還原工作目錄到目前分支的前1個版本.
 $ git reset HEAD^^  | 還原工作目錄到目前分支的前2個版本.
 $ git reset HEAD~3  | 還原工作目錄到目前分支的前3個版本.
 $ git reset HEAD~n  | 還原工作目錄到目前分支的前n個版本.
*$ git reset <commit id>        | 還原工作目錄到 <commit id> 的版本. 保留工作目錄已變更的檔案. <commit id> 只要輸入前4碼.
*$ git reset <commit id> --hard | 還原工作目錄到 <commit id> 的版本. 放棄工作目錄已變更的檔案. <commit id> 只要輸入前4碼.
 $ git reset <commit id>^       | 還原工作目錄到 <commit id> 前1個版本.
 $ git reset <commit id>^^      | 還原工作目錄到 <commit id> 前2個版本. 
 $ git reset <commit id>~3      | 還原工作目錄到 <commit id> 前3個版本.
 $ git restore <file>          | 取消(工作目錄中)的檔案變更. Restore working tree files
 $ git restore --staged <file> | 取消(暫存區中的)檔案變更.
 $ git rm --cached <file> | 還原(工作目錄)為(暫存區檔案).
 $ git rm <file> |  移除檔案並將變更移到暫存區（工作區域 -> 暫存區. 等於 ($ rm <file> 後再 $ git add <file>).
 $ git stash      | 暫存工作目錄的檔案變更. 不含 untracked 檔案.
 $ git stash -u   | 暫存工作目錄的檔案變更. 包含 untracked 檔案.
 $ git stash clear | 清除暫存變更.
 $ git stash list  | 查詢暫存變更清單.
 $ git stash pop stash@{n}   | 取回(暫存的變更編號n), 到目前的分支上, 並刪除(暫存的變更編號n)
 $ git stash drop stash@{n}  | 刪除(暫存的變更編號n)
 $ git stash apply stash@{n} | 取用(暫存的變更編號n), 到目前的分支上, 並保留(暫存的變更編號n)
*$ git status  | 檢查狀態、本地分支、檢查變更. 若有異動, 則會提示.
 $ git switch <branch> | 同 git checkout <branch> 
*$ git version | 取得版本資訊. 例如: git version 2.31.1.windows.1
*$ winget install --id Git.Git -e --source winget, 更新為最新版本的 git, 包含 git-gui, git bash 工具.
 $ pwd         | 目前工作目錄
 $ gh repo create | CLI. 以詢問方式建立遠端資料庫並 push 目前資料夾已Commit的內容.
 $ gh repo create --source=. --public --push --remote <RepositoryName> | CLI. 建立遠端資料庫並 push 目前資料夾已Commit的內容.

memo:
<file> 例如 LiteDB.Studio/LiteDB.Studio.exe.
<commit id> 只要輸入前4碼.
<branch> 例如 origin/main 或 origin/master 代表 遠端分支為 origin, 本地分支為 main 或 master. (2020-10-01起)響應黑人平權運動, 預設 master branch 改為 main branch.

習慣命名:
  資料庫分支 (資料庫分支名稱可以為任意名稱, 只是習慣上如下命名)
    main: 本地資料庫分支, 本文大多數簡稱為本地資料庫.
    origin: 遠端資料庫分支. 本文大多數簡稱為遠端資料庫.
    master: 舊版的本地資料庫分支. 2020-10-01起, 響應黑人平權運動, 預設 master branch 改為 main branch.
    upstream: 遠端 Forked 分支.

GitMode: (在 $ git ls-files -s 中顯示的第一欄)
  32-bit mode, split into (high to low bits)
    4-bit object type
      valid values in binary are 1000 (regular file), 1010 (symbolic link)
      and 1110 (gitlink)

    3-bit unused

    9-bit unix permission. Only 0755 and 0644 are valid for regular files.
    Symbolic links and gitlinks have value 0 in this field.
Also, a directory object type (binary 0100) and group-writeable (0664 permissions) regular file are allowed as indicated by the fsck.c fsck_tree method. The regular non-executable group-writeable file is a non-standard mode that was supported in earlier versions of Git.

This makes valid modes (as binary and octal):
0100000000000000 (040000): Directory
1000000110100100 (100644): Regular non-executable file
1000000110110100 (100664): Regular non-executable group-writeable file
1000000111101101 (100755): Regular executable file
1010000000000000 (120000): Symbolic link
1110000000000000 (160000): Gitlink


#### SYNOPSIS/Syntax, 2025-04-21
git - the stupid content tracker
git [--version] [--help] [-C <path>] [-c <name>=<value>]
    [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
    [-p|--paginate|-P|--no-pager] [--no-replace-objects] [--bare]
    [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
    [--super-prefix=<path>]
    <command> [<args>]

git-add - Add file contents to the index
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	  [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
	  [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--renormalize]
	  [--chmod=(+|-)x] [--] [<pathspec>…​]

git-blame - Show what revision and author last modified each line of a file
git blame [-c] [-b] [-l] [--root] [-t] [-f] [-n] [-s] [-e] [-p] [-w] [--incremental]
	    [-L <range>] [-S <revs-file>] [-M] [-C] [-C] [-C] [--since=<date>]
	    [--progress] [--abbrev=<n>] [<rev> | --contents <file> | --reverse <rev>..<rev>]
	    [--] <file>


git branch [--color[=<when>] | --no-color] [--show-current]
        [-v [--abbrev=<n> | --no-abbrev]]
        [--column[=<options>] | --no-column] [--sort=<key>]
        [--merged [<commit>]] [--no-merged [<commit>]]
        [--contains [<commit>]] [--no-contains [<commit>]]
        [--points-at <object>] [--format=<format>]
        [(-r | --remotes) | (-a | --all)]
        [--list] [<pattern>…​]
git branch [--track[=(direct|inherit)] | --no-track] [-f]
        [--recurse-submodules] <branchname> [<start-point>]
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
git branch --unset-upstream [<branchname>]
git branch (-m | -M) [<oldbranch>] <newbranch>
git branch (-c | -C) [<oldbranch>] <newbranch>
git branch (-d | -D) [-r] <branchname>…​
git branch --edit-description [<branchname>]

git-commit - Record changes to the repository
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
	   [--dry-run] [(-c | -C | --fixup | --squash) <commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
	   [--date=<date>] [--cleanup=<mode>] [--[no-]status]
	   [-i | -o] [-S[<keyid>]] [--] [<file>…​]
	
git-clone - Clone a repository into a new directory
git clone [--template=<template_directory>]
          [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
          [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
          [--dissociate] [--separate-git-dir <git dir>]
          [--depth <depth>] [--[no-]single-branch] [--no-tags]
          [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
          [--[no-]remote-submodules] [--jobs <n>] [--sparse]
          [--filter=<filter>] [--] <repository>
          [<directory>]
		  
git-config - Get and set repository or global options
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] name [value [value_regex]]
git config [<file-option>] [--type=<type>] --add name value
git config [<file-option>] [--type=<type>] --replace-all name value [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] --get name [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] --get-all name [value_regex]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--name-only] --get-regexp name_regex [value_regex]
git config [<file-option>] [--type=<type>] [-z|--null] --get-urlmatch name URL
git config [<file-option>] --unset name [value_regex]
git config [<file-option>] --unset-all name [value_regex]
git config [<file-option>] --rename-section old_name new_name
git config [<file-option>] --remove-section name
git config [<file-option>] [--show-origin] [--show-scope] [-z|--null] [--name-only] -l | --list
git config [<file-option>] --get-color name [default]
git config [<file-option>] --get-colorbool name [stdout-is-tty]
git config [<file-option>] -e | --edit	   

git-fsck - Verifies the connectivity and validity of the objects in the database
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
	 [--[no-]full] [--strict] [--verbose] [--lost-found]
	 [--[no-]dangling] [--[no-]progress] [--connectivity-only]
	 [--[no-]name-objects] [<object>*]

git-init - Create an empty Git repository or reinitialize an existing one
git init [-q | --quiet] [--bare] [--template=<template_directory>]
	  [--separate-git-dir <git dir>]
	  [--shared[=<permissions>]] [directory]	 

git-log - Show commit logs
git log [<options>] [<revision range>] [[--] <path>…​]

git-prune - Prune all unreachable objects from the object database
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…​]

git-pull - Fetch from and integrate with another repository or a local branch
git pull [<options>] [<repository> [<refspec>…​]]

git-push - Update remote refs along with associated objects
git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	   [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-v | --verbose]
	   [-u | --set-upstream] [-o <string> | --push-option=<string>]
	   [--[no-]signed|--signed=(true|false|if-asked)]
	   [--force-with-lease[=<refname>[:<expect>]]]
	   [--no-verify] [<repository> [<refspec>…​]]

git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>
git remote rename [--[no-]progress] <old> <new>
git remote remove <name>
git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
git remote set-branches [--add] <name> <branch>…​
git remote get-url [--push] [--all] <name>
git remote set-url [--push] <name> <newurl> [<oldurl>]
git remote set-url --add [--push] <name> <newurl>
git remote set-url --delete [--push] <name> <URL>
git remote [-v | --verbose] show [-n] <name>…​
git remote prune [-n | --dry-run] <name>…​
git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)…​]	

git-reset - Reset current HEAD to the specified state   
git reset [-q] [<tree-ish>] [--] <paths>…​
git reset (--patch | -p) [<tree-ish>] [--] [<paths>…​]
EXPERIMENTAL: git reset [-q] [--stdin [-z]] [<tree-ish>]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]

git-restore - Restore working tree files
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…​
git restore [<options>] [--source=<tree>] [--staged] [--worktree] --pathspec-from-file=<file> [--pathspec-file-nul]
git restore (-p|--patch) [<options>] [--source=<tree>] [--staged] [--worktree] [--] [<pathspec>…​]

git-stash - Stash the changes in a dirty working directory away
git stash list [<options>]
git stash show [<options>] [<stash>]
git stash drop [-q|--quiet] [<stash>]
git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
git stash branch <branchname> [<stash>]
git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
	     [-u|--include-untracked] [-a|--all] [-m|--message <message>]
	     [--] [<pathspec>…​]]
git stash clear
git stash create [<message>]
git stash store [-m|--message <message>] [-q|--quiet] <commit>

git switch [<options>] [--no-guess] <branch>
git switch [<options>] --detach [<start-point>]
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
git switch [<options>] --orphan <new-branch>



#### **** 常用(流程、設定、備忘)

**** 常用流程: 複製遠端資料庫 為 本機新子資料夾.  Clone/Fork, 2025-04-21
git clone <url.git> | Clone/Fork 複製遠端資料庫 到 新子目錄(遠端資料庫名稱)中. 
Clone a repository into a new directory. 
同一台電腦可將相同的遠端資料庫, 複製為多份各自獨立的版本, 互不影響.

- 以檔案總管選擇工作目錄後, 按滑鼠右鍵選擇 Git Bash Here, 啟動 Git Bash.

- 輸入指令 git clone <url.git>
  $ git clone <url.git> 
  <url.git> 可從遠端資料庫網站上取得.
  例如: git clone https://github.com/github-honda/MassTransitPratice.git 會建立新子資料夾名稱為 MassTransitPratice 在目前工作目錄下.
  
- 同一台電腦可將相同的遠端資料庫, 複製為多份各自獨立的版本, 互不影響.
  例如: 
  C:\temp\folder1 存放主要版本, 只讀取最新版本, 做為比對差異用途.
  C:\temp\folder2 存放工作版本, 可隨意變更測試.
	a. 工作版本使用後, 若沒有上傳異動的檔案, 則可將整個工作版本的資料夾刪除就好.
	b. 工作版本使用後, 若有上傳異動的檔案, 則再可到主要版本取得更新後, 刪除不再需要的工作版本的資料夾.
	取得工作版本很簡單, 因此不需要在意常常取得工作版本後, 再刪除的問題.

**** 常用流程: Visual Studio 2022 C# 開發環境設定, 2025-04-20
CodeHelper\GitHub\SampleFiles\VisualStudio2022C#
CodeHelper\cs\vs2022\VS2022Pratice, 多專案

**** 常用流程: 建立全新的 Repository, 2025-04-20
1. 在 GitHub.com 網站上新建 repository.
建立時, 請選擇需要加入檔案, 例如 README, license, or gitignore 等檔案, 作為初始版本的檔案.
例如: 
.gitignore template: VisualStudio
License: GNC General Public License v2.0

2. 複製遠端資料庫到新子目錄(專案名稱)中
參考 (常用流程: Clone/Fork 複製遠端資料庫 為 本機新子資料夾)


**** 取得不同版本的檔案變更清單
- 檢視版本清單
$ git log --oneline --graph 

- 取得 最新檔案變更差異清單
$ git diff --name-status HEAD

- 取得 最新 與 指定版本 的檔案變更差異清單
$ git diff --name-status d54a0b4 HEAD > c:\\temp\\ChangeList.txt

**** 常用流程: fix a Git detached head 2023-01-23 
https://stackoverflow.com/questions/10228760/how-do-i-fix-a-git-detached-head
Detached head means you are no longer on a branch, you have checked out a single commit in the history (in this case the commit previous to HEAD, i.e. HEAD^).

□ If you want to delete your changes associated with the detached HEAD
○ You only need to checkout the branch you were on, e.g.
$ git checkout master

Next time you have changed a file and want to restore it to the state it is in the index, don't delete the file first, just do
$ git checkout -- path/to/foo
This will restore the file foo to the state it is in the index.

□ If you want to keep your changes associated with the detached HEAD
○ save your changes in a new branch called tmp
$ git branch tmp 

○ Run 
$ git checkout master
If you would like to incorporate the changes you made into master, run git merge tmp from the master branch. 
You should be on the master branch after running git checkout master.




   

**** 常用設定: 設定 Git Gui Client Encoding UTF-8 on Windows  2022-10-09 
ref: https://support.huaweicloud.com/intl/en-us/usermanual-codehub/devcloud_hlp_0954.html
UTF-8 is the default encoding on Linux and code hosting websites, but not on Windows. Therefore, Chinese characters may become garbled on the Git client on Windows. Set the encoding to UTF-8 to address this problem.
UTF-8 是 Linux 和代碼託管網站上的默認編碼，但在 Windows 上不是。 因此，在 Windows 的 Git 客戶端上，漢字可能會出現亂碼。 將編碼設置為 UTF-8 以解決此問題。

以指令設定的方式:
$ git config --global core.quotepath false # encoding of status output 
$ git config --global gui.encoding utf-8 # GUI encoding
$ git config --global i18n.commit.encoding utf-8 # encoding of commit messages
$ git config --global i18n.logoutputencoding utf-8 # encoding of log outputs
$ export LESSCHARSET=utf-8 # Git uses the less pager by default. This command is to convert the encoding of less commands to UTF-8.

以操作方式同上設定:
注意這兩個檔案(etc\gitconfig, /etc/profile) 都在 Git 安裝目錄下. 
Alternately, you can perform the following operations to convert the encoding:
Add the following lines to etc\gitconfig:
[core]    quotepath = false 
[gui]    encoding = utf-8 
[i18n]    commitencoding = utf-8 
          logoutputencoding = utf-8

Add the following line to /etc/profile:
export LESSCHARSET=utf-8

以下說明相關設定參數:
NOTE:
gui.encoding = utf-8
It addresses the garbled characters in Git GUI and Gitk. If comments in the code contain garbled characters, add [gui] encoding = utf-8 to git/config in the root directory of the project.

i18n.commitencoding = utf-8
It converts commit log messages to the UTF-8 format to avoid garbled characters on the server.

i18n.logoutputencoding = utf-8
It converts git logs to the UTF-8 format.

export LESSCHARSET=utf-8 , together with i18n.logoutputencoding, ensures that Chinese characters are properly displayed in git logs.

Add the following line to etc\git-completion.bash so that Chinese names can be properly displayed:
alias ls="ls --show-control-chars --color

**** 常用設定: 指定程式語言
.gitattributes 設定如下:
* linguist-language=C# 
指定整個 repository 為 C#.
參考檔案: SampleLinguist.gitattributes

**** 常用設定: 選擇 .gitignore
https://github.com/github/gitignore

例如: https://github.com/github/gitignore/blob/main/VisualStudio.gitignore

例如: 參考 VisualStudio.gitignore 中, 忽略 NuGet Packages 的段落如下:
# NuGet Packages
*.nupkg
# NuGet Symbol Packages
*.snupkg
# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*
# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/
# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config
# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets	


**** 常見問題: 檢查 2022-12-30
$ git branch -vv
* master 28b359c1 [origin/master] CodeHelper memo.


**** 常見問題: 檢查遠端是否有新資料 2022-12-30
todo:
檢查遠端是否有新資料待更新?
檢查遠端與本地的差異?


**** 常見問題: git remote update, git fetch, git pull 三者差異 2022-12-30 
git remote update, git fetch, git pull 三者差異:
$ git remote update : 下載全部的分支, 但是不會 merge.
$ git fetch         : 下載指定的分支, 但是不會 merge.
$ git pull          : 下載目前的分支並merge.
What Is The Difference Between Git Remote Update, Git Fetch And Git Pull?
To update your Git remote you can follow the below command:
git remote update can update all of your branches set to track remote ones, however it cannot merge any changes in it.
git fetch can update only the branch you are on, however not merge any changes in.
git pull can update and merge any remote changes of the present branch you are on.
This would be the one you use to update a local branch.

**** 常用流程: 更新本地資料庫, 2024-09-22 
□ pull = fetch + merge 最簡單
從 <RemoteBranch> 下載到 <LocalBranch>, 同時合併分支, git pull = fetch + merge. 
若已設定(預設 upstream)
$ git pull

否則
$ git pull <RemoteBranch> <LocalBranch>  
例如: $ git pull origin main, 或 $ git pull origin master

□ 分解步驟下載全部分支
$ git remote update  <--- 下載全部分支, 無 merge.
$ git merge <branch> <--- 合併分支. 快轉合併 fast-forward 將 <banch>分支併入目前的分支

□ 分解步驟下載指定分支
$ git fetch <RemoteBranch>  <--- 下載指定分支, 無 merge.
$ git merge <branch> <--- 合併分支. 快轉合併 fast-forward 將 <banch>分支併入目前的分支


**** 常用流程: Unable to obtain your identity
(更換電腦, 新安裝 Git Gui, 複製 Local repository 到新電腦使用)時.  

ref:
Picture\UnableToObtainYourIdentity.jpg

Unable to obtain your identity:
  Committer identity unknown
  *** Please tell me who you are.
  Run
    git config --global user.email "you@example.com"
	git config --global user.name "Your Name"
  to set your account's default identity.
  Omit --global to set the identity only in this repository.
  
  fatal: unable to auto-detect email address (got 'honda@GARDEN1.(none)')





**** 常用流程: 恢復到目前分支的原狀 2021-03-17
$ git reset --hard  
還原工作目錄到目前分支的版本, 即放棄已變更的檔案 並恢復到目前分支的版本. --hard 為 放棄工作目錄已變更的檔案.

或
$ git reset <commit id> --hard 
還原工作目錄到 <commit id> 的版本. 放棄工作目錄已變更的檔案. <commit id> 只要輸入前4碼.


**** 常用流程: 查詢本地分支、遠端分支.  2023-01-04 
□ 查詢狀態也可以看到本地分支
$ git status   查詢狀態也可以看到本地分支
On branch master
Your branch is up to date with 'DemoCreateFromGitGui/master'.
Your branch is up to date with 'origin/master'.

□ 查詢本地分支
$ git branch   <--- 查詢本地分支, 標示為綠色*目前本地分支
* ZLib         <--- 目前本地分支
  master


□ 查詢遠端分支
$ git branch -r  查詢遠端分支 
  Sample output 1: 
    2個遠端分支
  origin/ZLib  <---- 目前本地分支
  origin/v3
  origin/v4
  origin/v5
  upstream/master
  upstream/v3
  upstream/v4
  upstream/v5.1

  Sample output 2: 
  origin/1637
  origin/2694
  origin/HEAD -> origin/master            <--- 目前遠端分支  
  origin/anurse/3625-hanging-onconnected
  origin/anurse/4100-try-hard
  : <---- 待輸入 

**** 常用流程: 切換 GitHub 網站上遠端資料庫的預設分支 2023-02-06 
變更GitHub網站上遠端資料庫的預設分支, 可能會有無法預期的結果...
https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/changing-the-default-branch

Changing the default branch
1. On GitHub.com, navigate to the main page of the repository.
2. Under your repository name, click  Settings.
3. In the "Code and automation" section of the sidebar, click  Branches.
4. Under "Default branch", to the right of the default branch name, click Switch icon with two arrows to the right of current default branch name
5. Use the drop-down, then click a branch name.
6. Click Update. "Update" button after choosing a new default branch
7. Read the warning, then click I understand, update the default branch. "I understand, update the default branch." button to perform the update

**** 常用流程: 建立分支 和 切換分支 2023-01-25 
□ 方法1: 2個指令完成.
先建立新分支, 再切換到新分支.
別忘了要切換到哪個分支繼續工作!
*$ git branch <NewBranch>        <--- 建立分支. 
*$ git checkout <NewBranch>      <--- 切換到分支. Switch to a branch. 若分支不存在, 則錯誤訊息.

□ 方法2: 1個指令完成.
切換到新分支, 若新分支不存在, 則建立新分支.
*$ git checkout -b <newBranch>   <--- 切換到新分支, 若新分支不存在, 則建立新分支.

**** 常用流程: 切換到其他 <OtherBranch> 工作後, 再回到自己的 <SelfBranch>. 2023-01-04 
□ 查詢本地分支. 標示為綠色*就是目前的分支.
$ git branch   <---- 查詢本地分支. 標示為綠色*就是目前的分支.
* main

□ 切換到<OtherBranch>工作.
$ git checkout OtherBranch   <--- 切換到<OtherBranch>
Switched to a new branch 'OtherBranch'
Branch 'OtherBranch' set up to track remote branch 'OtherBranch' from 'origin'.

若<OtherBranch>不存在, 要建立的話, 則參考 (常用流程: 建立 <NewBranch>).

□ 查詢本地分支. 標示為綠色*就是目前的分支.
$ git branch   <---- 查詢本地分支. 標示為綠色*就是目前的分支.
* OtherBranch
  main
  
□ 使用後, 切換回到自己的 <SelfBranch>
$ git checkout main   <--- 切換回到自己的 <SelfBranch>



**** 常用流程: 更新 Forked repository 跟上原始來源的最新修改. 2024-09-29
- 在 Forked repository 首頁上, 找到 Sync fork.Update branch 按下去就更新.
  若按下 Sync fork 之後出現 This branch it out-of-date, 才可 Update branch.
  
- 若本地資料庫也需要最新的修改, 則可再更新本地資料庫:
  $ git pull
	
□ 舊方法: 
先在本地資料庫上, 跟上原始來源的最新修改後, 再更新到Forked的遠端資料庫.
○ 確認已增加(遠端原始來源分支) 
  檢查是否已有(遠端原始來源分支)
  $ git remote -v
    習慣上:
      origin = Forked repository. (你自己的遠端分支 origin).
      upstream = Original source repository. (遠端原始來源分支).
	  資料庫分支可以為任意名稱, 可以自訂名稱, 不需要叫做upstream.

  若沒有的話, 則須新增 upstream
  $ git remote add upstream https://github.com/github-honda/LiteDB.git 
 
○ 從(遠端原始來源分支 upstream)下載到(本地資料庫 master).
  $ git pull upstream master 

○ 從(本地資料庫 master) 上傳到 (你自己的遠端分支 origin)
  $ git push origin master 



**** 常用流程: 切換到<commit id>版本. 2020-12-27 
檢查 commit 紀錄
$ git log --oneline --graph

切換到指定的 <commit id>版本
$ git reset <commit id>
<commit id> 只要輸入前4碼就可以.
預設為 --mixed 模式會保留工作目錄已變更的檔案.

或是 切換到指定的 <commit id>版本, 並且放棄工作目錄的檔案變更.
$ git reset <commit id> --hard

切換後檢查 commit 紀錄, 可能會看不到<commit id> 之後的變更紀錄, 必須改用 git reflog 才能看到 
$ get reflog 

再切換為(原先未切換前)的版本
$ git reset <commit id>

切換版本過程中, 可能會多出檔案殘留在工作目錄中. 
例如: 切換到舊版本時, 會把過去已刪除的檔案還原, 殘留在工作目錄中, 形成 untracked file 待 commit.
因此解決方法有
1. 可於切換時加入 --hard 放棄工作目錄的檔案變更, 就不會有殘留於工作目錄的檔案 untracked file.
$ git reset <commit id> --hard

2. 將殘留的檔案 untracked file commit 
3. 修改或刪除殘留的檔案.



**** 常用流程: 暫存目前的變更, 下載最新的遠端資料後, 再繼續暫停的工作. 2020-12-27
$ git stash  | 暫存目前的變更

$ git stash list | 查詢已有的變更
例如:
stash@{0}: WIP on [branch1]: ...
stash@{1}: WIP on [branch2]: ...
stash@{0...n} 為 stash 的編號, WIP=Wrok In Progress 工作進行中.

$ git stash pop stash@{n} | 取回(暫存的變更編號n), 到目前的分支上, 並刪除(暫存的變更編號n). 20201223: ?測試不會刪除?
$ git stash drop stash@{n} | 刪除(暫存的變更編號n)
$ git stash apply stash@{n} | 取用(暫存的變更編號n), 到目前的分支上, 並保留(暫存的變更編號n)

$ git pull origin main
  20201223, 跟Git Gui 操作不一樣: 在 Git Gui 中使用 Remote.Fetch From origin後, 資料會下載, 但是branch卻會保留在目前分支上, 不會跳到到下載後的最新分支上.
            待確認 Git Gui 的正確操作為何? 使用指令 git pull 則會下載新資料, 也會跳到最新下載的分支上.
  20210309, 因為 git pull 比 fetch 多了 fast-forward merge 動作, 若合併分支時沒有衝突, 則將變更併入目前的分支. 

**** 常用流程: 上傳最新的修改 2022-05-02

以下2種方式都可使用, 建議畫面操作方式最簡單:
□ 使用指令: 檔案總管選擇目錄後按滑鼠右鍵.Git Bash Here.
  ○ git status, 檢查檔案狀態. 
    例如: 已變更檔案 Changes not staged for commit, 未納管檔案 Untracked files...等.
    △ git add <file>, 或 git add --all, 將未納管的檔案加入納管. 
	  納管代表(commit 範圍內的檔案清單).
	  
  ○ git commit -a -m "Commit Message". 將已變更的檔案, 存入本地資料庫. 若沒有輸入 Commit Message, 則會要求輸入
  ○ git push, 將(本地資料庫)上傳到(遠端資料庫). 
    △ 或是 git push origin main, 上傳(本地資料庫 main) 到 (遠端資料庫 origin).
	  (資料庫Repository)預設名稱, 習慣為(本地資料庫 main), (遠端資料庫 origin). 舊版的遠端資料庫為 master.

□ 畫面操作: 檔案總管選擇目錄後按滑鼠右鍵.Git GUI Here.
  操作最簡單, 用久了會忘記指令該怎麼敲.
  ○ 啟動畫面後顯示
   上面(已變更檔案清單 Unstaged Changes), 及
   下面(已存入本地資料庫檔案清單(Staged Changes(Will Commit)).
   右上(Portions staged for commit)為選擇(Unstaged Changes檔案)內容變更明細.
    △ 按鍵 Rescan: 重新查詢最新檔案狀態. 若檔案有變更, 就隨時給他來按一下看看最新的狀態.
    △ 按鍵 Stage Changed: 將上面(已變更檔案清單 Unstaged Changes), 存入下面(已存入本地資料庫檔案清單(Staged Changes(Will Commit)).
    △ 按鍵 Sign Off: 不常用. Sign-off is requirement for getting patches into the Linux kernel, but most projects don't actually use it.
    △ 按鍵 Commit: 將下面(已存入本地資料庫檔案清單(Staged Changes(Will Commit)), 存入本地資料庫.
	               若沒有輸入 Commit Message, 則會要求輸入.
    △ 按鍵 Push: 將將(本地資料庫)上傳到(遠端資料庫).
	
**** 常用流程: 上傳最新的修改 及 相關指令. 2020-12-27

$ git status
目前只有未納入管理的檔案.
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        picture/
        readme-GitHub.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add --all
$ git status
將未納入管理的檔案加入後, 現在有可以 commit 的變更檔案了:
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   picture/CreatePublicRepositoryOnGitHubWebSite.jpg
        new file:   readme-GitHub.txt

$ git commit -a -m "Init add"
commit 進本地資料庫:
[main f6225ed] Init add
 2 files changed, 1684 insertions(+)
 create mode 100644 picture/CreatePublicRepositoryOnGitHubWebSite.jpg
 create mode 100644 readme-GitHub.txt

$ git push origin main
推送上傳(本地main)到(遠端origin) 
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 239.76 KiB | 14.10 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
remote: This repository moved. Please use the new location:
remote:   https://github.com/github-honda/GitPratice.git
To https://github.com/github-honda/gitpratice.git
   5327c25..f6225ed  main -> main

$ git status
重新檢查, 現在沒有新的修改了.
On branch main
nothing to commit, working tree clean

同樣的概念, 以下示範不同的情境: 
  修改檔案, 並增加 Untracked files 後上傳推送.
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   picture/CreatePublicRepositoryOnGitHubWebSite.jpg
        modified:   readme-GitHub.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        picture/CreatePublicRepositoryOnGitHubWebSite-Original.jpg

no changes added to commit (use "git add" and/or "git commit -a")

先將 Untracked files 加入管理:
$ git add --all

檢查沒有 Untracked files 了:
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   picture/CreatePublicRepositoryOnGitHubWebSite-Original.jpg
        modified:   picture/CreatePublicRepositoryOnGitHubWebSite.jpg
        modified:   readme-GitHub.txt

commit 進本地資料庫:
$ git commit -a -m "Commit both tracked and untracked files."
[main d54a0b4] Commit both tracked and untracked files.
 3 files changed, 53 insertions(+), 4 deletions(-)
 copy picture/{CreatePublicRepositoryOnGitHubWebSite.jpg => CreatePublicRepositoryOnGitHubWebSite-Original.jpg} (100%)
 rewrite picture/CreatePublicRepositoryOnGitHubWebSite.jpg (86%)

檢查沒有新的變更了:
$ git status
On branch main
nothing to commit, working tree clean

以預設 upstream 名稱推送到遠端資料庫
$ git push
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main
回應錯誤: 尚未設定 upstream.
設定過 upstream, 才能夠執行 "git push", 否則要指定名稱, 例如: "git push origin main"

設定預設 upstream 並 推送到遠端資料庫.
  下次就可以只輸入 "git push".
$ git push --set-upstream origin main
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 227.54 KiB | 16.25 MiB/s, done.
Total 5 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: This repository moved. Please use the new location:
remote:   https://github.com/github-honda/GitPratice.git
To https://github.com/github-honda/gitpratice.git
   f6225ed..d54a0b4  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.


**** 常用流程: 建立本地目錄, 連接到遠端 repository, 下載最新更新資料. 2022-08-27

1. 建立本地工作目錄
例如: E:\CodeHelper\GitHub\GitPratice
到本地工作目錄中, 啟動 git Bash command console.

2. 建立本地 repository 及 branch=main 
$ git init   ----> 新版(2020-10-01起)響應黑人平權運動, 預設已改為 main branch.
$ git init -b main  ----> 舊版建議要指定建立本地 Branch = main.
執行後目前工作目錄中會建立 .git 子目錄, 並且建立本地 branch=main.
指令模式 git bash 可在檔案總管選擇目錄後, 按滑鼠右鍵選單中啟動.
  舊版預設會建立 master branch.
  新版(2020-10-01起)響應黑人平權運動, 預設改為 main branch.
  
  可以將預設建立的名稱改為 "main":
  $ git config --global init.defaultBranch main | 將預設建立本地資料庫分支名稱設為 main.
 
3. 取得(遠端 repository 的 .git 網址).
例如: https://github.com/github-honda/gitpratice.git
.git 位置可從 github 網站的遠端 repository 取得. 

或新建遠端 repository後, 再取得 .git 網址. 
  建立遠端 repository 實例如圖: picture\CreatePublicRepositoryOnGitHubWebSite.jpg

4. 連接到(遠端 repository 的 .git 位置)
$ git remote add origin https://github.com/github-honda/gitpratice.git 
加入遠端的 repository 並指定別名為 origin.
習慣上遠端的 branch 命名為 origin. 

5. 下載最新更新資料.
$ git pull origin/master main
$ git pull origin main
$ git pull
將(遠端的 origin)下載到(本地的 main)

**** 常見問題: 本地branch建立為 main, 遠端 branch 為 master 且 not-for-merge (20210421, v 2.31.1.windows.1 才碰到)
操作過程如下, 最後以 git checkout master 將本地 main 切換到 master 解決.
切換到 master 後, 再切回 main 則已有錯誤, 表示 main 沒有任何版本紀錄可切回.
$ git init
Initialized empty Git repository in E:/CodeHelper/cs/WebSocket/NinjaWebSocketsFork/.git/

$ git remote add origin https://github.com/github-honda/Ninja.WebSockets.git

$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)

$ git remote -v
origin  https://github.com/github-honda/Ninja.WebSockets.git (fetch)
origin  https://github.com/github-honda/Ninja.WebSockets.git (push)

$ git pull
remote: Enumerating objects: 349, done.
remote: Counting objects: 100% (39/39), done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 349 (delta 15), reused 25 (delta 9), pack-reused 310
Receiving objects: 100% (349/349), 124.09 KiB | 1.48 MiB/s, done.
Resolving deltas: 100% (206/206), done.
From https://github.com/github-honda/Ninja.WebSockets
 * [new branch]      master     -> origin/master
 * [new branch]      pr/2       -> origin/pr/2
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> main


$ git branch --set-upstream-to=origin/master main
fatal: branch 'main' does not exist

$ git branch --set-upstream-to=origin/master master
fatal: branch 'master' does not exist

$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)

$ git branch --set-upstream-to=origin/master master
fatal: branch 'master' does not exist

$ git branch --set-upstream-to=origin/master main
fatal: branch 'main' does not exist

$ git branch --set-upstream-to=origin/master main
fatal: branch 'main' does not exist

最後以 git checkout master 將本地 main 切換到 master 解決.
$ git checkout master
Switched to a new branch 'master'
Branch 'master' set up to track remote branch 'master' from 'origin'.

切換到 master 後, 再切回 main 則已有錯誤, 表示 main 沒有任何版本紀錄可切回.
$ git checkout main
error: pathspec 'main' did not match any file(s) known to git


**** 常見問題:  預設Branch關聯未設定
即未設定 (遠端 origin Branch master 到本地 branch main) 的預設 Pull/Push 關聯.
$ git pull
錯誤訊息:
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=master/<branch> main

解決方法: 
  git branch --set-upstream-to=origin/master main


實例如下:
$ git init -b main
Initialized empty Git repository in E:/CodeHelper/GitHub/GitPratice/.git/

$ git remote add origin https://github.com/github-honda/gitpratice.git

$ git remote -v
origin  https://github.com/github-honda/gitpratice.git (fetch)
origin  https://github.com/github-honda/gitpratice.git (push)

$ git pull origin main
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (5/5), 3.88 KiB | 147.00 KiB/s, done.
From https://github.com/github-honda/gitpratice
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main


**** 常用流程: Commit目前的變更, 切換到需要優先處理的分支完成後, 再繼續目前的工作. 2020-12-27
$ git all -all
$ git commit -m "To be continued"
然後切到需要優先處理的分支完成後, 再繼續目前的工作:
$ git reset HEAD^

**** 常用流程: 暫存目前的變更, 切換到需要優先處理的分支完成後, 再繼續目前的工作. 2020-12-27
$ git stash  | 暫存目前的變更

$ git stash list | 查詢已有的變更
例如:
stash@{0}: WIP on [branch1]: ...
stash@{1}: WIP on [branch2]: ...
stash@{0...n} 為 stash 的編號, WIP=Wrok In Progress 工作進行中.

$ git stash pop stash@{n} | 取回(暫存的變更編號n), 到目前的分支上, 並刪除(暫存的變更編號n)
$ git stash drop stash@{n} | 刪除(暫存的變更編號n)
$ git stash apply stash@{n} | 取用(暫存的變更編號n), 到目前的分支上, 並保留(暫存的變更編號n)


**** 常用流程: commit and push 更新變更的檔案到遠端資料庫. 2020-11-29
$ git status
$ git add <file>...               to update what will be commited.
$ git add [subdir]/               新增子目錄.
$ git commit -a                   commit 所有最新變更的檔案, 並使用 vi 介面工具填寫變更說明. (-a = All) 
$ git commit -a -m "Commit Message"  commit 所有最新變更的檔案, 並使用 -m 參數填寫變更說明. (-a = All) 
$ git push                        更新到遠端資料庫.
建議用 Git GUI 比較快.





**** 常用流程: 跟上游同步-將Fork過來的專案, 更新到原作者的修改: 2020-12-27 
  在GitHub網站上跟上游同步-將Fork過來的專案, 更新到原作者的修改:
  參考 (在GitHub網站上跟上游同步.PDF)
第一步：設定原作的遠端節點
舉例來說，這是 Fork 過來的專案：

$ git remote -v
origin	https://github.com/eddiekao/dummy-git.git (fetch)
origin	https://github.com/eddiekao/dummy-git.git (push)
git remote 指令加上 -v 參數後可以看到更完整的資訊。從這裡可以看得出來目前這個專案只有設定一個遠端節點 origin。接下來我要幫它

加上另一個遠端節點，這個遠端節點指的位置就是原作的專案：
$ git remote add dummy-kao https://github.com/kaochenlong/dummy-git.git

其實大部份的資料都會教你使用 upstream 做為原作遠端節點的名字，但為避免大家跟之前在「Push 上傳到 GitHub」章節介紹的 upstream 搞混，所以這裡我故意使用 dummy-kao 做為指向原作的遠端節點。這時候在這個專案應該就有 2 個遠端節點了，一個是原來的 origin，一個是原作的 dummy-kao：
$ git remote -v
dummy-kao	https://github.com/kaochenlong/dummy-git.git (fetch)
dummy-kao	https://github.com/kaochenlong/dummy-git.git (push)
origin	https://github.com/eddiekao/dummy-git.git (fetch)
origin	https://github.com/eddiekao/dummy-git.git (push)

第二步：抓取原作專案的內容
接下來，就是使用 Fetch 指令來取得原作專案最新版的內容：

$ git fetch dummy-kao
如果忘了 Fetch 指令是做什麼的，請參閱「Pull 下載更新」章節介紹。還記得 Fetch 下來之後，在本地的遠端分支會往前移動嗎？如果想要跟上剛抓下來的這些進度的話，便是使用 Merge 指令（或是要用 Rebase 也可）：
$ git merge dummy-kao/master

這樣一來，你本機的進度就跟原作的是一樣了。

第三步：推回自己的專案
這個步驟要不要做就看你自己決定了，畢竟在你電腦上已經是最新版本了，如果你希望你在 GitHub 上那個 Fork 的專案也跟到最新版，只要推上去就行了：
$ git push origin master
這樣一來，你電腦裡的專案，以及在 GitHub 上從原作那邊 Fork 過來的專案都會是最新進度了。

**** 常用流程: 查詢是誰改的? 2020-12-27
$ git blame [檔案名稱], 查詢檔案中每一列的 commit 紀錄.
$ git blame -L 5,10 [檔案名稱], 查詢檔案中第5到10列的 commit 紀錄.
$ git blame -L 40,+1 foo, 查詢檔案 foo 第 40 列的 commit 紀錄.
$ git blame -L 40,+21 foo, 查詢檔案 foo 第 40 列到60列的 commit 紀錄.
$ git blame -L 40,60 foo, 查詢檔案 foo 第 40 列到60列的 commit 紀錄.


**** 常用流程: 合併分支 2020-12-27
檢查目前的分支
$ git branch  查詢本地分支. 標示為綠色*就是目前的分支.
$ git log --oneline --graph 標示為 * 的就是目前的分支.
  標示為 * 的就是目前的分支.
 
切換分支 switch to branch
$ git checkout 分支名稱
$ git checkout master

$ git merge 其他分支
$ git merge main
$ git merge DemoCreateFromGitGui/main (要全名)

若是碰到 "Fatal: Refusing to merge unrelated histories."
表示兩個分支沒有關聯, 無法合併.
則可
$ get merge master --allow-unrelated-histories
$ git merge DemoCreateFromGitGui/main --allow-unrelated-histories (要全名)
$ git push 更新到遠端資料庫

**** 常用流程: 查詢/設定 upstream.  2023-01-04
若設定 upstream後, 則執行 git pull 或 git push 時, 會自動使用預設的 upstream 分支, 不需要指定分支.
□ 查詢 upstream 
*$ git branch -vv     <--- 檢視 upstream 設定, -vv = doubly verbose. 輸出綠色*代表本地分支, 藍色代表遠端分支. 範例: * master 28b359c1 [origin/master] CodeHelper memo. 以上綠色為(* master), 藍色為 origin/master.
○ Sample output:
* master 10e72174 [origin/master] Extend CodeQL3000 in signalr-SignalR-official-build (#4654)

○ Sample output:
* ZLib   7580d066 Correct links.
  master 9843b507 [origin/master] Merge branch 'master' of https://github.com/mbdavid/LiteDB

□ 設定 upstream 
$ git branch --set-upstream-to=DemoCreateFromGitGui/master master  設定 upstream 
Branch 'master' set up to track remote branch 'master' from 'DemoCreateFromGitGui'.

□ 取消 upstream 設定
$ git branch --unset-upstream [<branchname>]  <--- 取消 upstream 設定

  
**** 常用流程: 建立本地新的 Repository, 並將本地 repository 連接到遠端資料庫 2020-12-27
Steps:
A. 建立本地Repository, 新增檔案.
1. 視需求, 先建立根目錄基本控制檔案: 例如 Markdown README.md, .gitignore, .gitattributes. 每一個目錄可以放不同的控制檔案.
2. 以檔案總管選擇目錄後, 按滑鼠右鍵, 選擇 Git Bash Here.
3. 建立本地 repository. $ git init  (執行後可看到子目錄 .git 已建立, branch 預設為 master.)
4. 新增檔案. $ git add .
5. $ git commit

B. 建立遠端 Repository, 連接到本地 Repository.
6. 到 github 網站, 登入帳號後, 選擇右上方的 New repository 按下後, 填寫 Create a new repository 網頁中2個必要欄位後, 按下 Create Repository 按鍵.
6.1 Repository name.
6.2 Public 或 Private repository.
參考 0110-CreateANewRepository.jpg

7. 執行成功後, 會出現 Quick setup 網頁, 提供 HTTPS 及 SSH 的內容, 可製作下方提示的三種建立連結的指令.
   HTTPS連結: https://github.com/github-honda/QTracker.git
   新建的 branch name = main. (預設命名為 main)
   參考 0120-QuickSetup.jpg 中提示三種連結的指令
   
7.1 提示指令1: 
建立全新的本地 Repository 連結. 
create a new repository on the command line
  echo "# QTracker" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main                  強制建立分支 main.
  git remote add origin https://github.com/github-honda/QTracker.git 建立遠端分支 origin.
  git push -u origin main             同時執行 push 及設定 upstream.


7.2 提示指令2:
上傳已存在的 repository 
push an existing repository from the command line
  git remote add origin https://github.com/github-honda/QTracker.git  建立遠端分支 origin.
  git branch -M main        強制建立分支 main.
  git push -u origin main   同時執行 push 及設定 upstream.

7.3 import code from another repository.
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.





#### 以下舊資料, 確認後移到上面, 2025-04-11

#### 遠端操作, 2025-04-11

複製既有的遠端數據庫
$ git clone <url>
執行 clone 命令時，會自動設定遠端數據庫為追踪目標。
這樣在 push 或 fetch/pull 命令時即使省略 repository，也可以正確的顯示/讀取修改內容。

添加一個遠端數據庫
$ git remote add <name> <url>

顯示遠端數據庫清單
$ git remote
加上 -v 後即可顯示遠端數據庫的詳細情況。

取遠端數據庫的分支建立本地端數據庫的分支
$ git checkout <branch>
在最新的Git版本中，chekout 命令的參數下指定遠端數據庫的分支，就可以從遠端數據庫複製分支到本地端數據庫建立分支。
如果因為版本太舊不能建立，請按照下面的方法在 branch 命令下建立分支。
$ git branch <branchname> origin/<branch>

在遠端數據庫建立分支/push修改內容到分支
$ git push <repository> <refspec>
加上 -u ，可以將遠端數據庫的分支設為追蹤目標。這樣，在 push 或 fetch/pull 命令時即使省略 repository，也可以正確的顯示/讀取修改內容。

在 <repository>，除了 remote add 命令所添加的數據庫名稱以外，也可以直接指定 URL，省略 <repository> 也可以成為遠端數據庫指定的追踪對象。
在 <refspec> 可以指定分支名稱。省略 refspec 的話，遠端數據庫和本地端數據庫所存有的分支在預設裡會被列為目標。


查看遠端數據庫分支的修改內容
$ git fetch <repository> <refspec>
要確認遠端數據庫的修改內容，但不想合併內容到本地端數據庫時，可以使用 fetch 命令。fetch 命令不會修改本地端數據庫的分支。

可以省略 repository 或 refspec。省略 repository 時的動作與 push 的時候是相同的。省略 refspec，所有的分支在默認裡會被列為目標。

合併遠端數據庫的分支的修改內容
$ git pull <repository> <refspec>
藉著 pull 命令，可以把遠端數據庫修改的內容合併到本地端數據庫。您只要知道「pull = fetch + merge」就可以了。

可以省略 repository 或 refspec 。省略 repository 名稱時的動作與 push 的時候是相同的。若省略 refspec，會只pull現有的分支。


刪除遠端數據庫的分支
$ git push --delete <repository> <branchname>

在 push 命令加上 --delete 和 <repository> <branchname> ，然後執行。
Git 1.7之前的版本不能使用 --delete ，所以請用以下的指令：
$ git push <repository> :<branchname>

在遠端數據庫建立標籤
$ git push --tags
加上 --tags ，就可以將在本地端數據庫裡所有的標籤添加到遠端數據庫。

刪除在遠端數據庫的標籤
$ git push --delete <repository> <tagname>
在 push 命令加上 --delete 和 <repository> <tagname>，然後執行。
Git 1.7之前的版本不能使用 --delete ，所以請用以下的指令
$ git push <repository> :<tagname>

修改已註冊的遠端數據庫的位址
$ git remote set-url <name> <newurl>
在 <newurl> 內指定遠端數據庫的新地址。

修改已註冊的遠端數據庫名稱
$ git remote rename <old> <new>
將遠端數據庫的名稱從 <old> 改為 <new> 。



#### Sign-Off, 簽名, 2025-04-11

Sign-off 用於 Linux kernel 的 patches, 大多數專案不常用.

Sign-off is a requirement for getting patches into the Linux kernel and a few other projects, but most projects don't actually use it.

It was introduced in the wake of the SCO lawsuit, (and other accusations of copyright infringement from SCO, most of which they never actually took to court), as a Developers Certificate of Origin. It is used to say that you certify that you have created the patch in question, or that you certify that to the best of your knowledge, it was created under an appropriate open-source license, or that it has been provided to you by someone else under those terms. This can help establish a chain of people who take responsibility for the copyright status of the code in question, to help ensure that copyrighted code not released under an appropriate free software (open source) license is not included in the kernel.




#### ToDo

https://stackoverflow.com/questions/58003030/what-is-the-git-restore-command-and-what-is-the-difference-between-git-restor

As reset, restore and revert documentation states:
There are three commands with similar names: git reset, git restore and git revert.
git reset, git restore and git revert 三者的差異
$ git revert 是會從一個(舊的commit版本)取得變更後, 建立(新的commit版本).
  is about making a new commit that reverts the changes made by other commits.
  
$ git restore 是會從(暫存區或其他的commit版本)復原工作目錄檔案, 並不會更新目前的分支.
    白話文簡單如下:
    $ git restore <file>          | 取消(工作目錄中)的檔案變更. Restore working tree files
    $ git restore --staged <file> | 取消(暫存區中的)檔案變更.
  is about restoring files in the working tree from either the index or another commit.
  This command does not update your branch.
  The command can also be used to restore files in the index from another commit.

$ git reset 是會更新目前的分支, 移動tip以便新增或移除目前分支中的commit版本.
  is about updating your branch, moving the tip in order to add or remove commits from the branch. 
  This operation changes the commit history.
  git reset can also be used to restore the index, overlapping with git restore.

So:
To restore a file in the index to match the version in HEAD (this is the same as using git-reset)
  git restore --staged hello.c

or you can restore both the index and the working tree (this the same as using git-checkout)
  git restore --source=HEAD --staged --worktree hello.c

or the short form which is more practical but less readable:
  git restore -s@ -SW hello.c
  
  

----
更新
https://marcus116.blogspot.com/2019/04/git-github-sync-fork-repository.html
在 GitHub 網站上 並未提供功能同步 fork 來源的 repository，因此可以透過以下步驟進行

Step 1 : 查看目前狀態輸入指令  git remote -v  可以看到目前有兩筆資料，內容為自己 GitHub fork 的 repo
$ git remote -v
origin  https://github.com/github-honda/LiteDB (fetch)
origin  https://github.com/github-honda/LiteDB (push)

Step 2 : 加入遠端的 repository 指定別名為 upstream，輸入指令且定義 repository GitHub 位置  
git remote add upstream https://github.com/mbdavid/LiteDB.git 

，執行完畢後再輸入  git remote -v  確認目前狀態，可以發現多了 upstream fetch & push
$ git remote -v
origin  https://github.com/github-honda/LiteDB (fetch)
origin  https://github.com/github-honda/LiteDB (push)
upstream        https://github.com/mbdavid/LiteDB.git (fetch)
upstream        https://github.com/mbdavid/LiteDB.git (push)

Step 3 : 接著把 upstream 更新抓下來，可以透過  git pull upstream master  取得遠端 master 的更新資料
$ git pull upstream master


Step 4 : 此時到 git log 查看發現已取得原本的 repo 更新資料，並與來源 GitHub commit 紀錄與 local 紀錄做比對，確認已更新至最新 commit 無誤
例如以下的 Request #???? 應該一致
master-remotes/upstream/master Merge pull request #1868 from for7raid/issue1865

Step 5 : 接著就可以開始進行修改或是異動的動作，完成後在把更新後的 repo push 即可更新到自己的 GitHub  
$ git push origin master

----------
2020-11-01


https://kbroman.org/github_tutorial/pages/init.html
Start a new git repository

Your first instinct, when you start to do something new, should be git init. You’re starting to write a new paper, you’re writing a bit of code to do a computer simulation, you’re mucking around with some new data … anything: think git init.

A new repo from scratch
完全手動建立 repository.
Say you’ve just got some data from a collaborator and are about to start exploring it.

1. Create a directory to contain the project.
2. Go into the new directory.
3. Type git init.
4. Write some code.
5. Type git add to add the files (see the typical use page).
6. Type git commit.
The first file to create (and add and commit) is probably a ReadMe file, either as plain text or with Markdown, describing the project.

Markdown allows you to add a bit of text markup, like hyperlinks, bold/italics, or to indicate code with a monospace font. Markdown is easily converted to html for viewing in a web browser, and GitHub will do this for you automatically.

A new repo from an existing project
從已經存在的專案建立 repository.
Say you’ve got an existing project that you want to start tracking with git.

1. Go into the directory containing the project.
2. Type git init.
3. Type git add to add all of the relevant files.
4. You’ll probably want to create a .gitignore file right away, to indicate all of the files you don’t want to track. Use git add .gitignore, too.
5. Type git commit.


Connect it to github
將本地 repository 連接到遠端資料庫
You’ve now got a local git repository. You can use git locally, like that, if you want. But if you want the thing to have a home on github, do the following.

1. Go to github.
2. Log in to your account.
3. Click the new repository button in the top-right. You’ll have an option there to initialize the repository with a README file, but I don’t.
4. Click the “Create repository” button.
   在 github 網站上登入後, 找到網頁右上方 "New repository" 按鍵按下後, 可建立新的 repository, 同時可選擇新增一些檔案, 建議不要新增檔案.

5. Now, follow the second set of instructions, “Push an existing repository…”
然後用以下的指令, 將本地的 Repository Push 上來: (ssh 模式)
$ git remote add origin git@github.com:username/new_repo
$ git push -u origin master

Actually, the first line of the instructions will say
實際上, 以上第一列指令可為: (https 模式)
$ git remote add origin https://github.com/username/new_repo

But I use git@github.com:username/new_repo rather than https://github.com/username/new_repo, 
as the former is for use with ssh (if you set up ssh as I mentioned in “Your first time”, 
then you won’t have to type your password every time you push things to github). 
If you use the latter construction, you’ll have to type your github password every time you push to github.



----------
2020-11-02

git mode 請參考 GitMode.txt, 例如以下 git commit 的顯示:
 create mode 100644 QuandicLib/ZLibMySql/Properties/AssemblyInfo.cs
 create mode 100644 QuandicLib/ZLibMySql/ZLibMySql.csproj
 create mode 100644 QuandicLib/ZLibMySql/packages.config
 create mode 100644 README.md



----------
2020-10-25

新建 Repository:
  操作流程畫面在 
 本地目錄為

以下為參考資料:
從 Visual Studio 2015 建立 repository 測試:
  測試流程檔案在 CodeHelper\GitHub\CreateEmptyRepositoryFromVisualStudio\
    目標為建立本機的 repository \CodeHelper\cs\vs2015\FirstPrivate\
  依據這篇: https://github.com/github/VisualStudio/blob/master/docs/using/creating-an-empty-repository-from-visual-studio.md
  PDF 檔案在 VisualStudio_creating-an-empty-repository-from-visual-studio.pdf
  流程文字測試如下:

Creating an empty repository from Visual Studio
1. Sign in to GitHub.
2. Open Team Explorer by clicking on its tab next to Solution Explorer, or via the View menu.
3. Click the Manage Connections toolbar button.
4. The manage connections toolbar button in Team Explorer
5. Click the Create link next to the account you want to create the repository in.

The create link in the Team Explorer pane
In the Create a GitHub Repository dialog, enter a name, description and local path for the repository.
The create a GitHub repository dialog

6. Select a license for the repository.
7. Check the Private Repository box if you want to upload the repository as a private repository on GitHub. You must have a Developer, Team or Business account to create private repositories.
8. Click the Create button to create the repository
9. When the repository is created, click the Create a new Project or Solution link in Team Explorer to create a project or solution in the repository.


----------
2020-11-02


git-reset(1).pdf EXAMPLES.

EXAMPLES
Undo add
$ edit                                     (1)
$ git add frotz.c filfre.c
$ mailx                                    (2)
$ git reset                                (3)
$ git pull git://info.example.com/ nitfol  (4)

(1) You are happily working on something, and find the changes in these files are in good order. You do not want to see them when you run git diff, because you plan to work on other files and changes with these files are distracting.
(2) Somebody asks you to pull, and the changes sound worthy of merging.
(3) However, you already dirtied the index (i.e. your index does not match the HEAD commit). But you know the pull you are going to make does not affect frotz.c or filfre.c, so you revert the index changes for these two files. Your changes in working tree remain there.
(4) Then you can pull and merge, leaving frotz.c and filfre.c changes still in the working tree.


Undo a commit and redo
$ git commit ...
$ git reset --soft HEAD^      (1)
$ edit                        (2)
$ git commit -a -c ORIG_HEAD  (3)
(1) This is most often done when you remembered what you just committed is incomplete, or you misspelled your commit message, or both. Leaves working tree as it was before "reset".
(2) Make corrections to working tree files.
(3) "reset" copies the old head to .git/ORIG_HEAD; redo the commit by starting with its log message. If you do not need to edit the message further, you can give -C option instead.


Undo a commit, making it a topic branch
$ git branch topic/wip     (1)
$ git reset --hard HEAD~3  (2)
$ git checkout topic/wip   (3)
(1) You have made some commits, but realize they were premature to be in the master branch. You want to continue polishing them in a topic branch, so create topic/wip branch off of the current HEAD.
(2) Rewind the master branch to get rid of those three commits.
(3) Switch to topic/wip branch and keep working.

Undo commits permanently
$ git commit ...
$ git reset --hard HEAD~3   (1)
(1) The last three commits (HEAD, HEAD^, and HEAD~2) were bad and you do not want to ever see them again. Do not do this if you have already given these commits to somebody else. (See the "RECOVERING FROM UPSTREAM REBASE" section in git-rebase(1) for the implications of doing so.)

Undo a merge or pull
$ git pull                         (1)
Auto-merging nitfol
CONFLICT (content): Merge conflict in nitfol
Automatic merge failed; fix conflicts and then commit the result.
$ git reset --hard                 (2)
$ git pull . topic/branch          (3)
Updating from 41223... to 13134...
Fast-forward
$ git reset --hard ORIG_HEAD       (4)
(1) Try to update from the upstream resulted in a lot of conflicts; you were not ready to spend a lot of time merging right now, so you decide to do that later.
(2) "pull" has not made merge commit, so git reset --hard which is a synonym for git reset --hard HEAD clears the mess from the index file and the working tree.
(3) Merge a topic branch into the current branch, which resulted in a fast-forward.
(4) But you decided that the topic branch is not ready for public consumption yet. "pull" or "merge" always leaves the original tip of the current branch in ORIG_HEAD, so resetting hard to it brings your index file and the working tree back to that state, and resets the tip of the branch to that commit.

Undo a merge or pull inside a dirty working tree
$ git pull                         (1)
Auto-merging nitfol
Merge made by recursive.
 nitfol                |   20 +++++----
 ...
$ git reset --merge ORIG_HEAD      (2)
(1) Even if you may have local modifications in your working tree, you can safely say git pull when you know that the change in the other branch does not overlap with them.
(2) After inspecting the result of the merge, you may find that the change in the other branch is unsatisfactory. Running git reset --hard ORIG_HEAD will let you go back to where you were, but it will discard your local changes, which you do not want. git reset --merge keeps your local changes.

Interrupted workflow
Suppose you are interrupted by an urgent fix request while you are in the middle of a large change. The files in your working tree are not in any shape to be committed yet, but you need to get to the other branch for a quick bugfix.

$ git checkout feature ;# you were working in "feature" branch and
$ work work work       ;# got interrupted
$ git commit -a -m "snapshot WIP"                 (1)
$ git checkout master
$ fix fix fix
$ git commit ;# commit with real log
$ git checkout feature
$ git reset --soft HEAD^ ;# go back to WIP state  (2)
$ git reset                                       (3)
(1) This commit will get blown away so a throw-away log message is OK.
(2) This removes the WIP commit from the commit history, and sets your working tree to the state just before you made that snapshot.
(3) At this point the index file still has all the WIP changes you committed as snapshot WIP. This updates the index to show your WIP files as uncommitted.

See also git-stash(1).

Reset a single file in the index
Suppose you have added a file to your index, but later decide you do not want to add it to your commit. You can remove the file from the index while keeping your changes with git reset.

$ git reset -- frotz.c                      (1)
$ git commit -m "Commit files in index"     (2)
$ git add frotz.c                           (3)
(1) This removes the file from the index while keeping it in the working directory.
(2) This commits all other changes in the index.
(3) Adds the file to the index again.

Keep changes in working tree while discarding some previous commits
Suppose you are working on something and you commit it, and then you continue working a bit more, but now you think that what you have in your working tree should be in another branch that has nothing to do with what you committed previously. You can start a new branch and reset it while keeping the changes in your working tree.

$ git tag start
$ git checkout -b branch1
$ edit
$ git commit ...                            (1)
$ edit
$ git checkout -b branch2                   (2)
$ git reset --keep start                    (3)
(1) This commits your first edits in branch1.
(2) In the ideal world, you could have realized that the earlier commit did not belong to the new topic when you created and switched to branch2 (i.e. git checkout -b branch2 start), but nobody is perfect.
(3) But you can use reset --keep to remove the unwanted commit after you switched to branch2.


Split a commit apart into a sequence of commits
Suppose that you have created lots of logically separate changes and committed them together. Then, later you decide that it might be better to have each logical chunk associated with its own commit. You can use git reset to rewind history without changing the contents of your local files, and then successively use git add -p to interactively select which hunks to include into each commit, using git commit -c to pre-populate the commit message.

$ git reset -N HEAD^                        (1)
$ git add -p                                (2)
$ git diff --cached                         (3)
$ git commit -c HEAD@{1}                    (4)
...                                         (5)
$ git add ...                               (6)
$ git diff --cached                         (7)
$ git commit ...                            (8)
(1) First, reset the history back one commit so that we remove the original commit, but leave the working tree with all the changes. The -N ensures that any new files added with HEAD are still marked so that git add -p will find them.
(2) Next, we interactively select diff hunks to add using the git add -p facility. This will ask you about each diff hunk in sequence and you can use simple commands such as "yes, include this", "No don’t include this" or even the very powerful "edit" facility.
(3) Once satisfied with the hunks you want to include, you should verify what has been prepared for the first commit by using git diff --cached. This shows all the changes that have been moved into the index and are about to be committed.
(4) Next, commit the changes stored in the index. The -c option specifies to pre-populate the commit message from the original message that you started with in the first commit. This is helpful to avoid retyping it. The HEAD@{1} is a special notation for the commit that HEAD used to be at prior to the original reset commit (1 change ago). See git-reflog(1) for more details. You may also use any other valid commit reference.
(5) You can repeat steps 2-4 multiple times to break the original code into any number of commits.
(6) Now you’ve split out many of the changes into their own commits, and might no longer use the patch mode of git add, in order to select all remaining uncommitted changes.
(7) Once again, check to verify that you’ve included what you want to. You may also wish to verify that git diff doesn’t show any remaining changes to be committed later.
(8) And finally create the final commit.


----------
2020-11-01

首次使用 git 和 github, 設定 SSH Key
https://kbroman.org/github_tutorial/pages/first_time.html

使用 Windows 版本的 Git Gui 可從 選單.Help.Show SSH Key.Generate Key 產生更簡單

Your first time with git and github
If you’ve never used git or github before, there are a bunch of things that you need to do. It’s very well explained on github, but repeated here for completeness.

1. Get a github account.
2. Download and install git.
3. Set up git with your user name and email.

a.Open a terminal/shell and type:

$ git config --global user.name "Your name here"
$ git config --global user.email "your_email@example.com"
(Don’t type the $; that just indicates that you’re doing this at the command line.)

I also do:

$ git config --global color.ui true
$ git config --global core.editor emacs
The first of these will enable colored output in the terminal; the second tells git that you want to use emacs.

4. Set up ssh on your computer. 
建立 ssh Key
I like Roger Peng’s guide to setting up password-less logins. 
Also see github’s guide to generating SSH keys.

Look to see if you have files ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub.
If not, create such public/private keys: Open a terminal/shell and type:

$ ssh-keygen -t rsa -C "your_email@example.com"
Copy your public key (the contents of the newly-created id_rsa.pub file) into your clipboard. On a Mac, in the terminal/shell, type:

$ pbcopy < ~/.ssh/id_rsa.pub


5. Paste your ssh public key into your github account settings.
將 ssh key 貼到 github 網站中你的帳戶設定

Go to your github Account Settings
Click “SSH Keys” on the left.
Click “Add SSH Key” on the right.
Add a label (like “My laptop”) and paste the public key into the big text box.

In a terminal/shell, type the following to test it:
用以下的指令測試 SSH 可連接 github 成功.
$ ssh -T git@github.com

If it says something like the following, it worked:
Hi username! You've successfully authenticated, but Github does
not provide shell access.

----------
2020-11-01

https://blog.darkthread.net/blog/my-git-cheatsheet/

我的 Git 指令小抄
	2019-04-05 08:40 AM	
	
趁著連假啃完龍哥大作「為你自己學 Git」，拖了多年蹲完 Git 馬步，換來了卻一椿心事的輕鬆。

從今天起，我再也不必擔心因「開發老鳥不會 Git Squash 合併 Commit」的祕密敗露被江湖人恥笑了，哈哈哈哈。(謎：擔心半天結果自己說出來?)

(背後有段故事：之前在 Github 送過一個 PR，因 Commit 歷程太雜，原作者請我調一下，結果我瞎搞一陣還愈整愈亂，最後對方搖搖頭說：錯了，你該用 squash 的... 算了，我已經幫你整好了。那時就發誓要學會squash，然後幾年過去了 XD)

讀書筆記做成 Git 常用指令小抄，方便日後查詢：

觀念：
  Git 是 Linus Torvalds 為管理 Linux 原始碼所寫的分散式版控系統，版控資料全部儲存在 .git 目錄下，不需伺服器也能運作。最著名的 Git 伺服器 Github 是全世界開源專案最主要集散地，TFS/Azure DevOps(前身是 VSTS) 也支援 Git 版控，或者自己架設一個 Git 伺服器也是選擇。

觀念：
  Git 有三個區域，採兩段式更新。
  區域包含「工作目錄(Working Directory)」、
  「暫存區(Staging Area)」、
  「儲存庫(Repository)」，
  新增檔案初為 Untracked 狀態，
  加入暫存區後為 New，
  修改後為 Modified，
  刪除後則為 Deleted，
  使用 git add 陸續將檔案更新狀態(新增修改刪除都算)由工作目錄移入暫存區，
  告一段落後再 git commit 將其由暫存區提交到儲存庫。

起手式 git init，
  在該工作目錄建立 .git 資料夾，開始用 Git 做版控

git add .
  將該目錄及其子目錄下所有異動放入暫存區、
  git add --all 將整個 Git 版控範圍異動放入暫存區

git commit -m "Commit Message" 
  將暫存區異動提交到儲存庫

git log --oneline --graph 
  以較清楚易讀的格式顯示簽入歷程

git log 搜尋參數：
  --author="Jefrrey"、
  --grep="wtf"、
  --S "Ruby"、
  --since="9am" 
  --until="5pm" 
  --after="2019-01" 
  --before="2019-05"

git rm filename --cached 將檔案轉為 Untracked，
  在 SourceTreee 中這個動作叫 Stop Tracking

檔案更名對 Git 而言是兩個動作
  (原檔 Deleted + 產生 Untracked 新檔)，
  但 git add . 時若 Git 察覺檔案內容相同(SHA1 相同)，狀態會變成 Renamed。
  要省時可用 git mv hello.html world.html

git commit --amend -m 
  "修改最後的Commit訊息" 
  修改最後一次 Commit 訊息
  (其實是撤掉前一次 Commit 重發一次，SHA1 不同)，若不加 -m 則帶出文字編輯器讓你修改

在最後 Commit 追加檔案：
  先 git add the_file 加入新檔，
  再 git commit --amend --no-edit 
  重發 Commit。
    (--no-edit 表沿用原 Commit 訊息不修改)
  提醒：不要對已 Push 出去的 Commit 做 --amend，以免造成別人困擾

空目錄不會被提交，
  解法為在目錄下放一個 .keep 或 .gitkeep 讓 Git 感應到它

不想版控的項目：
  編輯 .gitignore 檔案列舉排除不要納入版控的路徑(支援萬用字元)，
  常見 .gitignore 設定可參考 https://github.com/github/gitignore
  修改 .gitignore 前就加入的項目可用 git rm --cached 清除，一口氣清理所有應忽略檔：git clean -fx

檢視特定檔案的修改記錄 
  git log -p welcome.html 
  (-p 為顯示修改差異)

git blame index.html 
  列出每一行程式是何時被誰修改的，
    -L n1,n2 參數顯示特定行數區間

救回誤刪檔案或修改後反悔 
  git checkout program.cs

取回兩個版本之前的檔案 
  git checkout HEAD~2 program.cs

取消剛才的簽入 
  git reset HEAD^。
  HEAD 也可用最後一次 Commit SHA1(如 e12d8ef)替代，
  若 HEAD -> master，則寫 master^ 效果相同。
    ^表前一次，^^表前兩次，更多次可寫 ~n。
  或者用 git log 查出某次 Commit 的 SHA1，可直接 git reset SHA1 退至該次 Commit 版本。

Reset 參數：
  拆掉 Commit 後，該次 Commit 內容何去何從？
  --mixed 預設值，只丟棄暫存區內容，工作目錄檔案不動(丟回工作目錄)
  --soft 暫存區跟工作目錄的檔案都不動，只移動 HEAD 位置(丟回暫存區)
  --hard 丟棄暫存區跟工作目錄的檔案

git reflog 
  可查看 Reset 歷程找到被拆掉的 Commit
  (註：reflog 只保留最近 30 天)，用 git reset e12d8ef --hard 把 Commit 再救回來

HEAD 是一個指標指向目前的「分支」。
  .git/HEAD 內容為 refs/heads/master，
  而 .git/refs/heads/master 內容為一段 SHA1 40字元檔
  切換 Branch 時，git checkout branch1 背後是將 HEAD 檔內容為改為 refs/heads/branch1。
    (reflog 會留下所有 HEAD 切換記錄)
	
git add -p somefile 
  只 Commit 檔案部分內容(不常用) 
  SourceTree: Stage Selected Lines

git hash-object 計算 SHA1 值、git cat-file -p SHA1值 印出檔案內容

觀念：
  .git 內的物件有 Blob(檔案內容)、Tree(目錄結構)、Commit(提交資訊)、Tag(標籤) 
  註：書中超冷知識「在 .git 目錄裡有什麼東西」有精彩原理剖析。

觀念：
  Git 儲存資料以 SHA1 為基礎，只要更動一個 Byte 都會重做一個 Blob，比起某些版控用差異備份方式有效率但浪費空間。
  但 Git 會在儲存 Blob 時會壓縮檔案內容，
  當物件過多或 Push 時則會觸發資源回收打包機制，打包時會引用差異備份技巧減少空間，不用太擔心其空間使用效率。

git branch branchName 建立分支，分支耗用成本很低(僅一個 40 Byte 檔案)，請多利用。
  -m 改名、-d 刪除。請想像分支只是一張貼在 Commit 的貼紙，提交時換貼到最新的 Commit 上。

觀念：
  若 master 分支出 cat，Commit 兩次，checkout master 切回主線，
    git merge cat 時只需 Fast-Forward 將 master 貼紙移到 cat 所在 Commit。
    (不想快轉硬要新增一個 Commit 的話，請加 --no-ff 參數)
  若是 master 分支出 cat、dog 各自發展，最後 cat Merge dog 或 dog Merge cat，
    則需要新增一個 Commit，將 cat 或 dog 貼紙放上去。

Rebase 合併。
  master 分支出 cat、dog，二分支各自 Commit 兩次，在 cat 分支 git rebase dog 
    可將 cat 分支接到 dog 分支的後面，cat 的兩次 
	Commit 需要重新計算(Applying)產生兩個新的 Commit，接在 dog 兩次 Commit 後方，而 cat 貼紙移至最後一個 Commit 上。
  Rebase 不會產生合併專用 Commit，看起來較乾淨，但有修改歷史之嫌，Push 前整理 OK，Push 後就不宜再用。

如何取消 Rebase？
  用 reflog 找出 Rebase 前的最後動作 Commit SHA1，git reset b174a5a --hard或git reset ORIG_HEAD --hard
  (Rebase 是危險操作，Git 會留下 ORIG_HEAD 供緊急使用，其他危險動作還有 Merge、Reset)

合併衝突。
  cat 跟 dog 都改了同一個檔案，cat 合併 dog 時會出現 CONFLICT (conent): Merge conflict in ... 字樣，而 Commit 會變成 "Uncomitted changes"，
  衝突檔案(both modified)內容會被 Git 修改成兩邊差異對照並存的版本，務必手動修改決定採用哪邊再重新 git add 及 commit。
  若為 Rebase 合併發生衝突，將處於 rebase is progress 狀態，調整衝突檔案後用 git rebase --continue 繼續。

非文字檔衝突時(例如：圖檔、DLL)，
  git checkout --ours animal.jpg 或 git checkout --theirs animal.jpg 決定使用誰的版本。

在過去某個 Commit 上新增分支 
  git branch bird 657fce7 再 git checkout bird 或是 git checkout -b bird 657fce7 一次搞定。

修改過去歷史 
  git rebase -i bb0c9c2 互動模式修改歷史記錄，以文字編輯器整併 Commit。
    pick 保留 Commit 不做修改
    reword 保留 Commit 但改註解
    edit 保留 Commit 但停止 Amend
    squash 保留 Commit 但併入前一次 Commit
    fixup 類似 squash，但捨棄本次 Commit 的 Log 訊息
    exec 執行 Shell 指令
    drop 移除 Commit

rebase -i 是解決疑難雜症的利器：
  將多個 Commit 合併成一個(squash)、將一個 Commit 拆成多個(edit，到某個 Commit 停下來，此時 reset HEAD^，重新 add 再 commit，拆出兩個 Commit 後再 rebase --continue，頗複雜)、在 Commit 間插入新的 Commit、調整 Commit 順序、刪除 Commit。
  提醒：修改歷史是很危險的事，有可能發生先後順序因果錯亂，請謹慎為之。

git revert HEAD --no-edit 
  相當於 TFS 的 Undo，會新增一個 Commit 記載退回上一個 Commit。
  個人專案 Reset/Rebase 較省事且乾淨俐落，若團隊協作政策不允許，就用 Revert。
  
Tag 標籤有兩種 Lightweight 輕量(只有名稱) vs Annotated 附註(可加入註解文字)，但本質都像貼紙。
  常用於標註里程碑，如 v1.0.0、beta-release。

停掉手上半成品切回問題分支處理 
  - 先 commit，再 reset HEAD^ 或用 git stash (將半成品暫存起來)，
  git stash list 列出暫存項目，git stash pop stash@{2} 取出暫存項目，
  git stash drop stash@{0}、git stash apply stash@{0} 套用但不刪除暫存項目

不小心提交帳密時如何毁屍滅跡？
  git filter-branch --tree-filter "rm -f config/password.file"，
  如果已經 push 出去，就將 filter-branch 過的 Commit 重新 push -f 蓋掉。

  其他善後動作，用 
    filter-branch -f 
  再重來一次，
    rm .git/refs/original/refs/heads/master、
	git reflog expire --all -expire=now、
	git fsck --unreachable、
	git gc --prune=now
git cherry-pick 6a498ec 
  由別的分支撿 Commit 過來用

觀念：Unreachable 
  - 沒物件指向它，Dangling - 沒物件指向它，它也沒指向任何物件
  
設定 GitHub 端點 
  git remote add origin git@github.com:darkthread/practice-git.git，推檔案上去 
  git push -u origin master、取檔案回來 
  git fetch、Pull = Fetch + Merge，git pull --rebase 抓回來並進行 Rebase 手動合併，複製一份 
  git clone git@github.com:darkthead/practice-git.git

FAQ: 
  Fork GitHub 專案開發，如何跟上源頭的進度 
  git remote add src-project httqs://github.com/darkthread/blah.git，抓回更新
  git fetch src-project，合併進自己 Fork 的版本 
  git merge src-project/master

製作更新包 
  git format-patch fdc7cd38..6e6ed76 -o /tmp/patches 產生 *.patch 檔，匯入方式 git am /tmp/patches/*

GitFlow 流程規範：
  Master 分支 - 穩定隨時可上線，多會加上版號
  Develop 分支 - 開發主線，Feature 由此分支出去，改好再合併進來
  Hotfix 分支 - 從 Master 分支出來，改完合併回 Master 及 Develop
  Release 分支 - Dev 成熟時分支到 Release 做上線前最後測試，測試沒問題合併至 Master 及 Develop
  Feature 分支 - 由 Dev 分支出來，寫完再併合 Dev



----------
2020-04-10

HEAD

在 .git 目錄裡有一個檔名為 HEAD 的檔案，就是記錄著 HEAD 的內容
$ cat .git/HEAD
ref: refs/heads/master
  從這個檔案看起來，HEAD 目前正指向著 master 分支
  再看一下 refs/heads/master 的內容就會發現, 其實所謂的 Master 分支也不過就是一個 40 個字元的檔案罷了
  $ cat .git/refs/heads/master
  e12d8ef0e8b9deae8bf115c5ce51dbc2e09c8904

計算 SHA1 = 20 bytes = 40 個十六進位的數字方式呈現
$ printf "honda" | git hash-object --stdin
74fa7dba1df8826f627bf9d344116c1a266da62a
  

----------
2020-04-10

git區域:
工作目錄, Working Directory
暫存區, Staging Area
儲存庫, Repository
  git add    指令把檔案從工作目錄移至暫存區
  git commit 指令把暫存區的內容移至儲存庫

將檔案加入 (Staging Area 暫存區)控管 (即加入 Changes not staged for commit.)
$ git add [file]
$ git add [*.html]
$ git add --all
$ git add .
  沒有加入 Staging Area 的檔案 = Untracked file.
  空目錄是無法被提交的. 空目錄習慣上可以放一個.keep 或 .gitkeep 檔案後進行提交.

若在( add 檔案之後, 又修改的話), 則不會改到 staged 版本.
若需將( add 檔案之後, 又修改的檔案)更新加入到 staged版本, 則重新執行 git add 即可.

將(Staging Area 中檔案)存入本地資料庫
$ git commit -m "Commit Message"
必須提供說明本次commit 的訊息, 才能 commit.
若沒有提供訊息, 則會啟動 Vim 編輯器, 要求輸入.

若沒有檔案變更也要 commit的話:
$ git commit --alow-empty -m "Commit Message"

同時執行2個指令: add 跟 commit.
$ git commit -a -m "Commit Message"
  只對已經存在 repository的檔案有效.
  新加入的檔案(Untracked file)無效.  

$ git log
$ git log [檔案名稱] (找檔案變更紀錄)
$ git log -p [檔案名稱] (找檔案變更內容紀錄)
$ git log --oneline --graph
$ git log --author="Anyone"
$ git log --author="John\|Nacy"
$ git log --grep="AnyWord" (找 Commit 的訊息)
$ git log -S "AnyWord" (找 Commit 的檔案)
$ git log --oneline --since="9am" --until="12am" (今天早上)
$ git log --oneline --since="9am" --until="12am" --after="2017-01" (2017 年 1 月之後，每天早上)
$ git blame [檔案名稱] (檢查檔案中每一列對應的 commit)
$ git blame -L 5,10 [檔案名稱] (檢查檔案中第5到10列對應的 commit)

刪除工作目錄中的檔案, 並加入暫存區
1. 直接刪除[檔案名稱].
2. $ git add [檔案名稱] (將標記狀態=deleted的檔案, 存入暫存區)
或
$ git rm [檔案名稱]

將 tracked file 改成 Untracked file
$ git rm [file] --cached

變更檔名:
$ git mv [原檔名] [新檔名]

復原檔案
$ git checkout [檔案名稱]
$ git checkout HEAD~2 welcome.html (復原 2個版本前的檔案, 並且更新暫存區狀態)
$ git checkout HEAD~2              (復原 2個版本前的全部檔案, 並且更新暫存區狀態)


git reset 
  比較像是「前往」或「變成」，也就是「go to」或「become」的概念
  並沒有真的把這個 Commit「拆掉」

拆掉(前往)最後一次的 commit
$ git reset e12d8ef^
  或
  $ git reset master^
  $ git reset HEAD^
  
拆掉(前往)最後5次的 commit
$ git reset e12d8ef~5

拆掉(前往)到指定的 commit (包含指定的 commit 都拆掉)
$ git reset 85e7e30

$ git reset --mixed
  丟回工作目錄
  reset 的預設參數為 --mixed
  把暫存區的檔案丟掉，但不會動到工作目錄的檔案，也就是說 Commit 拆出來的檔案會留在工作目錄，但不會留在暫存區

$ git reset --soft
  丟回暫存區
  工作目錄跟暫存區的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已。也因此，Commit 拆出來的檔案會直接放在暫存區。
  
$ git reset --hard
  完全丟掉
  不管是工作目錄以及暫存區的檔案都會丟掉


  
----------
2020-04-09

更新 forked repository
https://gitbook.tw/chapters/github/syncing-a-fork.html

方法1: 
刪除舊的, 重新 Fork 新的.

方法2: 
新增(原 repository)為遠端節點, Fetch 最新的變更後, 再合併.

1. git remote add ..., 增設(原 repository)為遠端節點

> git remote add upstream https://github.com/aspnet/Docs.git

>git remote -v  
origin  https://github.com/github-honda/Docs.git (fetch)
origin  https://github.com/github-honda/Docs.git (push)
upstream        https://github.com/aspnet/Docs.git (fetch)
upstream        https://github.com/aspnet/Docs.git (push)
前2個是(自己的 origin), 後2個是(原 repository)為遠端節點

變更 upstream 
git remote set-url [--push] <name> <newurl> [<oldurl>]

2. git fetch [<options>] [<repository> [<refspec>…​]], 取得(原 repository)新資料
> git fetch upstream

Fetch 後, (本地的遠端分支)會往前移動.

3. Merge 或 Rebase 跟上進度
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>] [<commit>…​]
git merge --abort
git merge --continue
> git merge upstream/master
本機的進度已跟(原 repository)相同!

4. push 自己的變更專案.
> git push origin master
若要把本地的變更, 更新到(Fork 回的專案), 則可 push.


----------
2020-04-07
設定 License

參考
https://help.github.com/en/github/building-a-strong-community/adding-a-license-to-a-repository
2020-04-07_License2.jpg

Adding a license to a repository
You can include an open source license in your repository to make it easier for other people to contribute.
In this article
Including an open source license in your repository
Further reading


If you include a detectable license in your repository, people who visit your repository will see it at the top of the repository page. To read the entire license file, click the license name.

Open source licenses enable others to freely use, change, and distribute the project in your repository. For more information on repository licenses, see "Licensing a repository."
Including an open source license in your repository

1. On GitHub, navigate to the main page of the repository.
2. Above the file list, click Create new file. 
3. In the file name field, type LICENSE or LICENSE.md (with all caps).
   在 repository 主頁上, 點選 Create new file, 輸入 LICENSE 檔案名稱全部大寫字母後, 右方會出現 Choose a license template 按鈕
   參考 2020-04-07_AddLicense.jpg
   
4. To the right of the file name field, click Choose a license template. 
5. On the left side of the page, under "Add a license to your project," review the available licenses, then select a license from the list. 
   點選 Choose a license template後, 選擇適合的 license.
   參考 2020-04-07_ChooseLicense.jpg
 
6. Click Review and submit. 
7. At the bottom of the page, type a short, meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message. For more information, see "Creating a commit with multiple co-authors." 

8. Below the commit message fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is master, you should choose to create a new branch for your commit and then create a pull request. For more information, see "Creating a new pull request." 
   選擇要 commit 到目前的 branch 或 新的 branch.

9. Below the commit message fields, click the email address drop-down menu and choose a Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then <username>@users.noreply.github.com is the default commit author email address. For more information, see "Setting your commit email address." 

10. Click Commit new file. 

Further reading
"Setting guidelines for repository contributors"



----------
20190802
本段落 依照 git工作流程編輯摘要, 其餘段落為備忘或測試確認:

https://git-scm.com/docs


## 建立 remote repository
  1. 以 Edge 在 https://github.com/ 上使用自己的帳號建立.
  建議: 一個 repository 可以存放多個 solution. 存放原始碼及相關的文字檔案為主. 不要放文件: 例如 .jpg. 

## 連接 local repository to remote
  1. 先取得 .git 檔案: 在瀏覽repository 主畫面上選擇 "綠色的 Clone or download".
  2. Clone remote repository: 參考 CloneInTeamExplorer.jpg, 填入.git檔案 與 本地目錄位置.

## 取得遠端repository到目前目錄
cd ~/Documents/gitHub/
# example, and again, be careful, it will erase your entire folder
$ rm -rf repositoryA
$ git clone git://github.com/myUser/repositoryA.git
$ rm -rf repositoryB
$ git clone git://github.com/myUser/repositoryB.git 

## 查詢狀態
$ git status
可查詢(已變更、已刪除...)等檔案.

## 把全部的本地異動加到暫存區
$ git add --all

## 刪除檔案
  兩種方式:
  A. $ git rm [檔案名稱]
    透過 git status 可查詢到該檔案暫存區狀態為 deleted, 並且實體檔案已刪除.
	
  B. 分解動作: 先刪除檔案, 再執行 git add 指令:
  1 刪除檔案. (直接透過OS的刪除檔案指令或方式)
    透過 git status 可查詢到該檔案最新狀態為 deleted.
  2. $ git add [已刪除的檔案名稱]
    透過 git status 可查詢到該檔案暫存區狀態為 deleted.

## 加入控管檔案
$ git add [檔案名稱]

## 加入控管目錄
$ git add [目錄名稱]

## 停止控管指定的檔案
$ git rm [檔案名稱] --cached
  該檔案將從 git 目錄中的 tracked 變成 Untracked .
  本地的檔案則不會刪除.
  
## 停止控管本地 repository
  刪除 .git目錄, .gitattributes, .gitignore
  或 刪除本地整個目錄

## 停止控管遠端repository
  On GitHub, navigate to the main page, choose the repository setting, under Danger Zone, click Delete this repository.
  Deleting a private repository will delete all of its forks.
  Deleting a public repository will not delete its forks.
  
## 變更檔名
$ git mv 舊檔名 新檔名

## 只取得檔案, 不會clone, 也不會有本地目錄.git
$ git archive --remote=<repository URL> | tar -t
  只取得第一層 If you need folders and files just from the first level:
$ git archive --remote=<repository URL> | tar -t --exclude="*/*"
  只取得第一層目錄清單 To list only first-level folders of a remote repo:
$ git archive --remote=<repository URL> | tar -t --exclude="*/*" | grep "/"

## 檢查目前的分支
$ git branch
  標示為 * 的就是目前的分支.
 
## 切換分支
$ git checkout 分支名稱
$ git checkout master

## detached HEAD 狀態
  HEAD          = 指向某個分支的指標 或 目前所在的分支.
  detached HEAD = 沒有指向任一分支. 

## 刪除分支
$ git branch -D 分支名稱

## Commit 分支
$ git branch 分支名稱
$ git branch 新分支名稱 commit-SHA-1-編號
$ git brahcn newbranch b6d2111

## 不要版控的檔案或目錄: 
  參考檔案 sample.gitignore.
  
## 變更 repository 的 language
  GitHub 使用 linguist library 自動偵測 repository 中的程式語言. 在 https://github.com/github/linguist 可以找到 linguist完整說明.
    語言清單: languages.yml.txt
    可設定: linguist-documentation, linguist-language, linguist-vendored, linguist-generated and linguist-detectable
  因此可於.gitattributes 設定需要忽略的檔案.
    例如: 
	  *.css linguist-vendored
	  static/* linguist-vendored 代表通知 自動偵測 忽略掉目錄 static 下的所有檔案
      *.js linguist-language=Vue  指定.js 為Vue 語言
	  * linguist-language=C# 指定整個 repository 為 C#, 確認OK! 參考檔案: SampleLinguist.gitattributes

	  參考語法:
	  static/* linguist-vendored 代表通知 自動偵測 忽略掉目錄 static 下的所有檔案
      special-vendored-path/* linguist-vendored
      jquery.js linguist-vendored=false
	  project-docs/* linguist-documentation
      docs/formatter.rb linguist-documentation=false
	  *.kicad_pcb linguist-detectable=true
      *.sch linguist-detectable=true
      tools/export_bom.py linguist-detectable=false
	  *.css linguist-vendored
      *.js linguist-language=Vue  
      modules/* linguist-language=PHP
  
## 取得 Fork 之後的更新版本:
方法1: 刪除舊版, 再重新Fork新版.
方法2: 更新原作者的變更內容.
  主要步驟: 
    1. 將原作者的專案設為上層專案.
	2. Fetch 更新資料.
	3. 手動合併(自己的變更).

1. 將原作者的專案設為上層專案.

先檢查 Fork 的專案的遠端節點, 例如:
$ git remote -v
origin	https://github.com/eddiekao/dummy-git.git (fetch)
origin	https://github.com/eddiekao/dummy-git.git (push)
表示 這個專案只有設定一個遠端節點 origin 

增加遠端節點 = 原作者專案, 例如:
$ git remote add dummy-kao https://github.com/kaochenlong/dummy-git.git

結果例如: (原來的 origin，一個是原作的 dummy-kao)
$ git remote -v
dummy-kao	https://github.com/kaochenlong/dummy-git.git (fetch)
dummy-kao	https://github.com/kaochenlong/dummy-git.git (push)
origin	https://github.com/eddiekao/dummy-git.git (fetch)
origin	https://github.com/eddiekao/dummy-git.git (push)

2. 使用 Fetch 指令來取得原作專案最新版的內容
$ git fetch dummy-kao
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 1), reused 3 (delta 1), pack-reused 1
Unpacking objects: 100% (4/4), done.
From https://github.com/kaochenlong/dummy-git
 * [new branch]      features/mailer      -> dummy-kao/features/mailer
 * [new branch]      features/mailer-plus -> dummy-kao/features/mailer-plus
 * [new branch]      features/mailer_pro  -> dummy-kao/features/mailer_pro
 * [new branch]      features/member      -> dummy-kao/features/member
 * [new branch]      master               -> dummy-kao/master
 
Fetch 下來之後，在本地的遠端分支會往前移動嗎？如果想要跟上剛抓下來的這些進度的話，便是使用 Merge 指令（或是要用 Rebase 也可）
$ git merge dummy-kao/master
Updating ac341ae..689b015
Fast-forward
 contact.html | 2 ++
 1 file changed, 2 insertions(+)
 
這樣一來，你本機的進度就跟原作的是一樣了

3. 手動合併(自己的變更).
這個步驟要不要做就看你自己決定了，畢竟在你電腦上已經是最新版本了，如果你希望你在 GitHub 上那個 Fork 的專案也跟到最新版，只要推上去就行了：
$ git push origin master
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 596 bytes | 596.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/eddiekao/dummy-git.git
   ac341ae..689b015  master -> master
這樣一來，你電腦裡的專案，以及在 GitHub 上從原作那邊 Fork 過來的專案都會是最新進度了
 


----------
Git 是一個分散式版本控制軟體，最初由 Linus Torvalds 創作（也是作業系統 Linux 系統的開發者），其最初目的是為更好地管理 Linux kernel 開發而設計，其具備優秀的 merge tracing 合併程式碼的能力（使用程式碼 snapshot 來比較歷史版本差異）。
Github 則是一個支援 git 程式碼存取和遠端托管的平台服務，有許多的開放原始碼的專案都是使用 Github 進行程式碼的管理。


Git能檢查完整性
在 Git 中所有的物件在儲存前都會被計算查核碼 (checksum) 並以查核碼檢索物件。這意謂著 Git 不可能不清楚任何檔案或目錄的內容已被更動。此功能內建在 Git 底層並整合到它的設計哲學。 Git 能夠馬上察覺傳輸時的遺失或是檔案的毀損。
Git 用來計算查核碼的機制稱為 SHA-1 雜湊法。它由 40 個十六進制的字母 (0–9 and a–f) 組成的字串組成，基於 Git 的檔案內容或者目錄結構計算。 查核碼看起來如下所示：
24b9da6552252987aa493b52f8696cd6d3b00373
讀者會 Git 中到處都看到雜湊值，因為它到處被使用。事實上 Git 以檔案內容的雜湊值定址出檔案在資料庫的位址，而不是以檔案的名稱定址。

Git 是一款版本控制軟體，而 GitHub 是一個商業網站，GitHub 的本體是一個 Git 伺服器

----------
MarkDown

https://github.com/othree/markdown-syntax-zhtw
  MarkdownSyntaxCht.txt
https://daringfireball.net/projects/markdown/syntax
  https://daringfireball.net/projects/markdown/syntax.text
  MarkdownSyntaxEng.txt
  

----------
20190313

FAQ: 
what to do when the current branch does not track a remote branch ? 
M:\CodeHelper\cs\ASPNET\identity\WebAuthMySQL>git branch -u WebAuthMySQL/master
Branch 'master' set up to track remote branch 'master' from 'WebAuthMySQL'.

Given a branch foo and a remote upstream:
As of Git 1.8.0:
git branch -u upstream/foo

Or, if local branch foo is not the current branch:
git branch -u upstream/foo foo

Or, if you like to type longer commands, these are equivalent to the above two:
git branch --set-upstream-to=upstream/foo
git branch --set-upstream-to=upstream/foo foo



----------
20190312

不要版控, 可在.gitignore檔案中加入 regular expression 語法, 例如:
/doc/0230-IdentifyConfig.jpg
doc/ 

# SQL Server files
*.mdf
*.ldf

# Build results
[Dd]ebug/
[Dd]ebugPublic/
[Rr]elease/
[Rr]eleases/
[Xx]64/
[Xx]86/
[Bb]uild/
bld/
[Bb]in/
[Oo]bj/

其餘參考檔案: sample.gitignore



----------
20190311

取得 .git file: 在瀏覽repository 主畫面上選擇 "綠色的 Clone or download"

將本地 Repository 連線到遠端 repository: 
  1. 參考 RemoteEdit-TeamExplorer.jpg, 先在遠端建立, 再填入參數.
  2. 將本地 repository, 新建到遠端尚未建立的 github 資料庫, 可按"IDE 右下角 的 publish"!

----------
20190215

GitHub 

ref:
http://trufflepenne.blogspot.com/2016/09/vs2015git-hub.html


安裝
  Visual Studio 2015
  Tools.Extension and Updates...
  找到 GitHub Extension for Visual Studio 安裝
  
登入
  Team.Manage Connections...
  選擇 Connect, 填入Sign in 畫面的 Username 及 Password
  
建立 Repository
  選擇 Team.Manage Connections...
  選擇 GitHub.Create
  在 Create a GitHub Repository 畫面中填入
    Name:        VS2015TemplateOriginal
	Description: Visual studio 2015 project templates original
	Local path:  C:\Users\[UserName]\Source\Repos (預設路徑) 
	Git ignore:  VisualStudio
	License:     MIT License
	
在 Repository中新建方案 
  一個 repository 可以包含多個 solution.
  選擇 Team Explorer.Solutions.New...
    選擇需要建立的 Visual studio 專案 template
      本例選擇 WebForms with individual user accounts.  
    編譯、測試執行、建立資料庫:
      首頁
      註冊使用者, 建立資料庫. 
        資料庫建立路徑: C:\Users\[UserName]\Source\Repos\VS2015TemplateOriginal\WebAuth1\WebAuth1\App_Data\aspnet-WebAuth1-20190215111250.mdf 及 ldf.
      註冊使用者成功
      登出後再測試登入畫面
  建立完成後, 
    在 Solution Explorer 中可看到 Soluction 已經加上鎖住符號.
    在 Team Explorer中, 可以看到下方 Solutions 已經建立.
	
Commit Changes 確認變更:
  選擇 Team Explorer.Changes.
  Changes畫面下方列出本次本地資料庫已變更的檔案清單, 若需要確認變更, 則必須先填入必要欄位變更訊息.
  填入必要欄位變更訊息後, 才可以下拉確認方式選項:
    1. Commit All. (更新本機資料庫)
	2. Commit All and Push. (更新遠端資料庫)
	3. Commit All and Sync. (更新遠端資料庫 且 取得遠端資料庫的最新變更)
	
----------
2022-05-02

中英對照:
commit | 提交.
fast-forward merge | 快速合併分支.

----------
2022-05-02, todo 待整理

~.ssh/id_rsa.pub 代表在  c:\使用者\[user]\.ssh\ 下. Private key 檔案為 id_rsa, Public key 檔案為 id_rsa.pub.

fast-forward merge 快速合併分支
  若合併分支時沒有衝突, 則將檔案變更直接併入目前的分支.
  否則為 non fast-forward merge.
    若合併分支時產生衝突, 必須修改衝突的內容, 並建立(修改衝突內容後的)新的提交.




