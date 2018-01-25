# git-memo
個人的によく使うgitコマンドです

## 公式サイト
[https://git-scm.com/](https://git-scm.com/)


## git log

1行で表示
```
git log --oneline
```

1行で5件表示
```
git log --oneline -5
```


## git add

追加したファイルを全部追加
```
git add .
```


## git checkout

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


## git branch

ブランチ表示
```
git branch
git branch origin/master
git branch origin/dev
git branch -a
```

ローカルブランチ削除
```
git branch -D ブランチ名
```

リモートブランチ削除
```
git branch -D ブランチ名
git push origin :ブランチ名
git push --delete origin ブランチ名　←これでも行けるかも
```


## git reset

指定したリビジョンまで戻す（リビジョンを指定することで操作履歴も戻すことができる）
```
git reset --hard リビジョン
```

コンフリクトが起きて解消しようとしたけどこんがらがって中止したくなった場合の対処法
```
git reset --hard ORIG_HEAD
```


## git reflog

操作履歴を1行で4件表示する
```
git reflog -n 4
```


## git diff

指定した範囲のリビジョンの差分ファイルを出力する
```
git diff 開始リビジョン..終了リビジョン --name-only | git checkout-index --prefix=./sabun/ --stdin
```


## git tag


タグを付ける
```
git tag タグ名(v1.0.0とか)
```

タグを付ける（過去のコミットに）
```
git tag タグ名 リビジョン名
```

リモートのタグを削除する
```
git push --delete origin refs/tags/タグ名
```


## git stash

変更を退避させる
```
git stash
```

退避させた変更を見る
```
git stash list
```

退避させた変更を復活させる
```
git stash pop
git stash pop stash@{0}
```


## git rebase

マージ元のブランチへ移動
```
git checkout ブランチ名
```

マージ先(この例だとmaster)を指定してリベースする
```
git rebase master

	→コンフリクトしたら

		リベースの取り消しをする場合
		git rebase --abort

		コンフリクトを解決した場合（これをやるとリベースが続行する。更にコンフリクトしたら解決してから再度このコマンドで続行する）
		git rebase --continue

	コンフリクトしなかったら（コンフリクトを解決したら）マージ先のブランチへ移動
	git checkout master

	マージ元（ブランチ名）→マージ先（master）へ、マージコマンドでfast-forwardマージする
	git merge ブランチ名
```


## 無視するファイル指定
```
# シャープで始めるとコメント行になる

# tmp フォルダまるごと無視したい
tmp/

# 下階層全てのフォルダ内で ".DS_Store" ファイルを無視したい
*/.DS_Store

# 下階層全てのフォルダ内で拡張子が .psd のファイルを無視したい
*/*.psd

# トップ階層の .exe ファイルのみを無視したい
# ただしサブフォルダ内の .exe ファイルは無視しない
/*.exe

# img フォルダをまるごと無視したい
# だけど .png だけは無視したくない
img/*.*
!.png
```


## git skip-worktree

ファイルを無視したいとき
```
git update-index --skip-worktree [ファイル名]
```
ファイル無視の設定を元に戻したい時
```
git update-index --no-skip-worktree [ファイル名]
```

## .gitkeepファイルをからディレクトリに作成
```
find . -type d -empty -not -path './.git*' -exec touch {}\/.gitkeep \;
```

## コミットをまとめる(これでHEADから4つ分のコミットをまとめられます)
```
git rebase -i HEAD~4
```

## コミット間の変更ファイル一覧を出力
```
git diff --stat --name-only コミット1 コミット2
```

## 作業ディレクトリから追跡対象外のファイル（Untracked files）を削除
```
// 削除実行(-f：強制削除、-d：ディレクトリを対象にする)
git clean -fd

// 削除実行せずに削除予定のファイル一覧を表示
git clean -n
```

## ファイル単位でリセット
```
git checkout HEAD -- hoge.txt
```

## tigでコミット間の差分を見たい時
```
tig <コミットID>..<コミットID>
```

## 空コミット
```
git commit --allow-empty -m "コメント"
```

## git stashを復活させる方法
```
// 候補の sha1 がいくつか出てくる(長く開発していると、結構多く候補が出てきます)
git fsck | awk '/dangling commit/ {print $3}'

// 一つ一つの sha1 の内容を確認
git show --summary 候補のsha1

// 復活させる
git cherry-pick -n -m1 見つけたsha1
```
