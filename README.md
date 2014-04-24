GitHub勉強会 for eeicer
====
Git/Githubについてお勉強しましょう。


目標
----
* よく使うGitのコマンドをなんとなく理解する
* GitHubの機能をなんとなく理解する
* プルリクエストを送るフローを体験する


準備
====

インストール
----
### Windows or Mac
GUIクライアントの Source Tree を使うのがおすすめ。

[http://www.sourcetreeapp.com/](http://www.sourcetreeapp.com/)

#### Source Tree の利点
* 自動的にフェッチしてくれる
* 部分的・一行単位のステージ/アンステージがやりやすい

### Ubuntu
調べた限り使い勝手の良いGUIクライアントはなかったので、コマンドラインから使う。

```sh
$ sudo apt-get install git
```

#### CUIの便利ツール
##### tig
Gitのクライアント。

```sh
$ sudo apt-get install tig
```

##### hub
`git`コマンドを拡張した`hub`コマンド。実行には`Ruby`が必要。

[github/hub](https://github.com/github/hub)


設定
----
### 公開鍵の登録
[https://github.com/settings/ssh](https://github.com/settings/ssh)

右上の`Add SSH key`をクリック。

公開鍵`~/.ssh/id_rsa.pub`の中身を`Key`にコピペする。

### GitHub Educationの申し込み
7ドル/月のディスカウントを2年間受けられるので、Microプラン（プライベートリポジトリ5）が無料で利用できる。

大学ドメインのメールアドレスの登録が必要。

[https://education.github.com/](https://education.github.com/)


GitHubの機能
====

ユーザーに対して
----
### Follow
他のユーザーをフォローできる。
フォロイーが新しくリポジトリを作った・フォークしたなどの情報がNews Feedに流れてくる。

### Public contributions
コミット数を時系列に沿って可視化したもの。
コード書いてるか書いてないかが即わかる。


リポジトリに対して
----
### Watch
リポジトリの更新状況やissueなどの情報がNews Feedに流れてくる。

### Star
いわゆるfav

### Fork
他のユーザーのリポジトリのコピーを作成する。

### Issues
バグ報告・要望・todoなど。
対応が終わったらcloseするかんじ。

### Pull Requests
フォークしたリポジトリの更新を、フォーク元に反映させるためのリクエスト。
フォーク元のユーザーが、更新を取り込むかどうかを決める。


その他の機能
----
### Gist
[https://gist.github.com/](https://gist.github.com/)

スニペットを登録しておける。
ちょっとしたコマンドや設定とかを書いておくと忘れても大丈夫。


Gitのコマンド
====

リポジトリ間の操作
----
### `clone`
リモートリポジトリを、ローカルにコピーする。

リモートリポジトリにはURLごとに名前をつけることができ、メインのものを慣習的に`origin`と名付ける。

```
+ - - - - - -+          + - - - - -+
' remote:    '          ' local:   '
'            '          '          '
' +--------+ '  clone   ' +------+ '
' | origin | ' -------> ' | repo | '
' +--------+ '          ' +------+ '
'            '          '          '
+ - - - - - -+          + - - - - -+
```

### `pull`
リモートリポジトリの更新を、ローカルリポジトリに取り込む。

正確には、更新をダウンロードするだけの`fetch`と、取り込む`merge`もしくは`rebase`の2つのステップが実行される。

```
+ - - - - - -+         +- - - - - +
' remote:    '         ' local:   '
'            '         '          '
' +--------+ '  pull   ' +------+ '
' | origin | ' ------> ' | repo | '
' +--------+ '         ' +------+ '
'            '         '          '
+ - - - - - -+         +- - - - - +
```

### `push`
ローカルリポジトリの更新を、リモートリポジトリに反映させる。

```
+ - - - - - -+         +- - - - - +
' remote:    '         ' local:   '
'            '         '          '
' +--------+ '  push   ' +------+ '
' | origin | ' <------ ' | repo | '
' +--------+ '         ' +------+ '
'            '         '          '
+ - - - - - -+         +- - - - - +
```


ローカルリポジトリ内の操作
----
### 3つの状態
`git`管理下のディレクトリのファイルには3つの状態がある。

#### modified
リポジトリと比べて、ファイルが変更された状態。

#### staged
変更を実際にリポジトリに反映させるために、変更にされたファイルに印をつけた状態。

#### commmited
ファイルの変更が、リポジトリに反映された状態。

```
+----------+  add   +--------+  commit   +----------+
| modified | -----> | staged | --------> | commited |
+----------+        +--------+           +----------+
```

### `add`
変更されたファイルに`staged`の印をつける。

### `commit`
`staged`なファイルの変更を、リポジトリに反映させる。


GitHub上の操作
----
### fork
他のユーザーのリモートリポジトリを、自分のリモートリポジトリとしてコピーする。

```
+ - - - - - - - - - - +         + - - - - - - - -+
' someone's remote:   '         ' your remote:   '
'                     '         '                '
' +-----------------+ '  fork   ' +------------+ '
' |     origin0     | ' ------> ' |  origin1   | '
' +-----------------+ '         ' +------------+ '
'                     '         '                '
+ - - - - - - - - - - +         + - - - - - - - -+
```

### Pull Request
フォークしたリポジトリの更新を、フォーク元に反映させるためのリクエストを送る。

```
+ - - - - - - - - - - +                 + - - - - - - - -+
' someone's remote:   '                 ' your remote:   '
'                     '                 '                '
' +-----------------+ '  pull request   ' +------------+ '
' |     origin0     | ' <-------------  ' |  origin1   | '
' +-----------------+ '                 ' +------------+ '
'                     '                 '                '
+ - - - - - - - - - - +                 + - - - - - - - -+
```
