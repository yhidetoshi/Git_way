## Gitの使い方をまとめる

  - 名前とメールアドレスを設定
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

##### コミットログ 
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

    
