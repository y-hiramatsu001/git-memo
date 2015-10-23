# git-memo
個人的によく使うgitコマンドです

###公式サイト
[https://git-scm.com/](https://git-scm.com/)


###git log

1行で表示
```
git log --oneline
```

1行で5件表示
```
git log --oneline -5
```


###git add

追加したファイルを全部追加
```
git add .
```


###git checkout

ブランチ作成と切り替え
```
git checkout -b ブランチ名
```

ブランチ切り替え
```
git checkout ブランチ名
```

リモートブランチをローカルにチェックアウト
```
git checkout -b ブランチ名 origin/ブランチ名
```


