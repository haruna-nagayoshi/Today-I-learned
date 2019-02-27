# git submodule


## 概要
外部ライブラリの特定のコミットを参照し、自分のリポジトリに含ませることができる。

例えば、bookeリポジトリだったら、laradockの特定のコミットがsubmodule化されている。  
laradockの中身を閲覧しようとすると、コミット番号がディレクトリ名に含まれており、  
githubにpushされたlaradockの特定コミットを参照していることがわかる。    
https://github.com/haruna-nagayoshi/booke
  

## 効果
laradockやbootstrapなどgitの特定コミットをモジュール化することで、  
手元に置かなくても利用することができる。  
そのため、  
・容量が軽くなる  
・開発者間でバージョン管理ができる  

PHPでいうcomposerのような役割を果たす。  
必要なプログラムが動くように必要なものだけ外から持ってきてくれる...イメージ。  

laradockは、中身はカスタマイズせずにgit submoduleで利用し、必要なコンテナを引数で指定して起動する  
という使い方をするようである。  

## 使い方
参考：[Gitのサブモジュール機能を使ってプロジェクトを管理してみよう](http://vdeep.net/git-submodule)  

#### サブモジュールを追加する
①サブモジュールを追加  
`$ git submodule add https://github.com/Laradock/laradock.git`  

②以下の内容の　.gitsubmodule ファイルが生成される。  
```
[submodule "対象ライブラリの名前"]
    path = ローカルのパス
    url = 外部ライブラリのリポジトリURL

(例)
[submodule "laradock"]
    path = laradock
    url = https://github.com/Laradock/laradock.git
```

また、.git/configファイルにも下記のような記述がされる。
```
(中略)
[submodule "laradock"]
	url = https://github.com/Laradock/laradock.git
	active = true
```

③サブモジュールをcommit, push
>サブモジュールは追加をおこなったあと、プロジェクト側でコミットしておく必要があります。次のコマンドでコミットを実行。

`$ git commit -m "add submodule: laradock"`

サブモジュールの状態は、以下のコマンドのいずれかで確認できる。
bookeリポジトリで確認すると、
確かに `876935452ec75fb19f75fef386234dc38e7c78de laradock (v7.5.0-5-g8769354)` のコミットがモジュール化されているとわかる。
```
$ git submodule
 876935452ec75fb19f75fef386234dc38e7c78de laradock (v7.5.0-5-g8769354)

$ git submodule status
 876935452ec75fb19f75fef386234dc38e7c78de laradock (v7.5.0-5-g8769354)
```

最後にpushを行う。
以上の手順でサブモジュール化が完了する。

#### サブモジュールを最新版に更新する
`$ git submodule foreach git pull`
git submodule foreachコマンドを使うと、プロジェクト内の全てのサブモジュールでgit pullを行う。

この場合も、commit・pushが必要。
```
$ git commit -m "update submodule hello: hello2"
$ git push origin master
```

#### サブモジュールが含まれているリポジトリをcloneする
`$ git clone --recursive https://github.com/okutani-t/submodule_test.git`

>もし、すでにクローン済みで、サブモジュールを含んでいない場合、次のコマンドでサブモジュールを落としてくることができます。
```
$ git clone https://github.com/okutani-t/submodule_test.git
$ git submodule update --init --recursive
または
$ git clone https://github.com/okutani-t/submodule_test.git
$ git submodule init
$ git submodule update
```


## おまけ
- githubよりgitlabのMarkdownのほうが書きやすい気がする。ソースを囲った場合の色等がはっきりしているし、画像もすぐにUPできるから。使い方に慣れていないだけかも。  
【追記】①画像はissue上ではリンク生成されるので、適当なissueを作って自動生成する方法がある。他に、画像保存用のブランチやリポジトリを作りそこに保存する方法もある。
②githubでは、gitlabのようにフォントの色を変える方法はないらしい。不便。

- LaravelもLaravel Collectiveも英語であってもレファレンスを読む気になるけど、Gitは読む気になれない・・・。ので、今回参考にしたサイトの存在はありがたいし丁寧で分かりやすかった。
