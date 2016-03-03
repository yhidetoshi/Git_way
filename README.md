## Gitの使い方をまとめる

#### 名前とメールアドレスを設定
```
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
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

