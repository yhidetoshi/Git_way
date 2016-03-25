## Gitの使い方をまとめる

#### 名前とメールアドレスを設定/確認
```
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
$ git config --list
```

  - コミットする
```
git add hello_world.php
git commit -m "add file"
```

  - リポジトリを初期化
```
git init
```

  - リポジトリの状態確認
```
git status
```

#### git log コミットログの確認
  - コミットログの表示
```
git log
```
  
  - ログ表示の要約
```
git log --pretty=short
```

  - 指定したディレクトリ,ファイルのみのログ表示
```
git log <file_name>
```

  - コミットの差分表示
```
git log -p <file_name>
```

#### git diff 変更差分の確認
  - ワークツリーとステージ領域の差分確認
```
git diff
```
  - ワークツリーと最新コミットの差分を確認
```
git diff HEAD
```

#### git branch ブランチ
  - ブランチの一覧表示
```
git branch
```
  - ブランチを作成して切り替える
```
git checkout -b dev-A

(下記の2行と同じ)
→ git branch dev-A
→ git checkout dev-A
```
  - masterブランチへ切り替える
```
git checkout master
```
  - 1つ前のブランチに切り替える
```
git checkout -
```

#### トピックブランチ
  - トピックブランチ
    - 1つのトピック(テーマ)に集中して他の作業は一切行わないブランチのこと
  - masterブランチ
    - いつでもソフトウェアをリリースできるブランチのこと 
  - 統合ブランチ
    - トピックブランチの分岐元で併合する先のブランチのこと
      - 統合先はmasterブランチになる

#### git merge ブランチをマージ
  1. 統合元のブランチからmaster(統合先)ブランチに切り替え
  
  　 ->マージ先のブランチに変更してから  `git merge <hoge-A(マージするブランチ)>`
  
  2. git merge --no-ff dev-A(統合元のブランチ)

#### git log --graph ブランチを視覚的に確認する
  - git log --graph

#### コミット変更する操作
  - git reset 歴史を戻る
```
git reset --hard <id>
→ <id>はgit logで確認
```
  - git reflog Gitコマンドで行われた変更のログを確認(commit, checkout, reset, mergeなど)
  - masterブランチに切り替えてから実施
```
git reset --hard <ref_id>
```
#### コンフリクト(競合)を解消

git merge --no-ff fix-B
```
[コンフリクトエラー]
Auto-merging hello_world.php
CONFLICT (content): Merge conflict in hello_world.php
Automatic merge failed; fix conflicts and then commit the result.
```
→ dev-Aブランチからmasterへコミットし, mergeしてfix-Bブランチしたのでコンフリクが発生
コンフリクが発生したファイルを開くと [=====]で上下に分けられている。
===より上の部分が現在の状態、下のの部分が今回マージしようとしている内容

→ どちらかを削除して git add, git commitするとマージに成功する

  - コミットメッセージを修正(直前のコミットメッセージを修正する)
```
git commit --amend
```

#### git remote add リモートリポジトリを登録
  - リモートリポジトリのmasterブランチへ送信
```
echo "# Git_way_check" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:<user_name>/<repo_name>.git
git push -u origin master
```
  - master以外のブランチ(dev-D)でpush
```
git checkout -b dev-D
git push origin dev-D
```
  
#### git clone リモートリポジトリから取得
```
git clone URL
```
→ git cloneで取得した直後だとブランチはmaster

→ git cloneで取得し, 新たにgit checkoutで新しいブランチをきり,そのブランチで実装してpushするのが
開発の方法。

#### Pull Request
  1. Forkする
  2. git clone <forkした方のURL>
  3. git checkout -b <new_branch>
  4. git push origin <added new branch>


### githubでいつもと違うPCからpushする場合
```
# git remote set-url origin https://<account_name>@github.com/<account_name>/<repo_name>.git
# git push -u origin master
-> パスワードを入力
```

### rejected/non-fast-forwardが出た場合
(error_message)! [rejected]        master -> master (non-fast-forward)
```
[対策1]
# git pull
 -> (pull コマンドによって、リモートリポジトリの変更内容がローカルリポジトリのブランチに反映)

[対策2]
# git fetch
# git merge origin/master
```

### Gtk-WARNING **: cannot open display:とエラーの時
```
# git pull
(gnome-ssh-askpass:11826): Gtk-WARNING **: cannot open display: 

# echo $SSH_ASKPASS
/usr/libexec/openssh/gnome-ssh-askpass

# unset SSH_ASKPASS
# git pull
```
#### error: The requested URL returned error: 403 Forbidden while accessing と怒られた時
```
$ git remote set-url origin https://<user_name>@github.com/<user_name>/<repo_name>.git
$ git config --list
-> 再度、git pushする
```


### git fetchとpullについて
- feth
  - リモートリポジトリの最新の履歴の取得だけを行う。取得したコミットは、名前の無いブランチとして取り込まれる
  - このブランチはFETCH_HEADという名前でチェックアウトすることができる
```
# git branch                           
* master

# git checkout FETCH_HEAD
-> リモートの変更分がこの(FETCH_HEAD)ブランチで変更されている

# git branch                           
* (HEAD detached at FETCH_HEAD)
  master

->次にmasterブランチにmergeする

# git checkout master

git branch                           
* master

# git merge FETCH_HEAD                 
Updating 7a0a6e2..3921d78
Fast-forward
 CentOS6_x/Command/README.md | 1 +
 1 file changed, 1 insertion(+)

 -> リモートリポジトリで変更されたリポジトリがローカルにも反映された
```

- pull
  - `git fetch` と `git merge`を一気にやるもの  
