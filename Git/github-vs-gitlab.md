# gitlabとgithub

## 概要
先日、社内でgithubが利用できるようになった。  
多くの人が喜んでいたようだが、違いや共通点を知らないためになにが便利なのかわからないので調べてまとめる。  

## gitlabとは

## githubとは


#
## 共通点
#### issue board
Trelloのように、カンバン方式でissueを管理できる。
Assigneeに応じてアイコンが表示される機能や、TODOなどのLabel機能がある。  

(githubだと、cardをただのTODOリストとしても使えるし、cardとissueを紐づけることもできる。gitlabでは試したことがないので不明)  



#### 画像の自動生成
画像をコピーしてissue上でペーストすると、自動でリンクが生成され、画像を貼ることができる。  

githubのwikiや.md上では自動生成されないが、issueを適当に作って生成されたリンクを使えば、wiki等でも利用できる。  
画像保存用のリポジトリやブランチを作成する方法もあるが、画像を貼りたいだけならこの方法でいいと思う。  
どこでも自動生成できるようにしてほしい。    

####
####


#
## 相違点
#### PullRequest MergeRequest

#### PullRequestとissueの番号
gitlabでは、MRとissueの番号は生成した順に振られていくので、番号は必ずしも一致しない。  
githubでは、PRとissueの番号が一致するようになっている。(ということは、issueを作らずにPRしたら、issueの番号には空きが発生する？)

#### Shortcut Key
どちらもショートカットキーがあるが、微妙に違うのでややこしい。  
仕事でgitlabを使うときはプロジェクトが複数あるので Shift + P は便利かも。でもどの階層なら使えるのかいまいちわかりにくいので、マウスで十分だと思う。  
gitlabのショートカット一覧(ツールバー→Help→Quick help→Use shortcutsで見れる)  
![image](https://user-images.githubusercontent.com/38639386/53463877-98353600-3a8b-11e9-8d9c-03ca9d7fccb0.png)

githubのショートカット一覧  
?キーを押下するとチートシートが表示される。  
もしくは、詳細な説明付で一覧が見れる。[Using keyboard shortcuts](https://help.github.com/en/articles/using-keyboard-shortcuts)  

####
####
####
#### Markdown
gitlabでは、バッククオートで文字を囲むとフォントが赤色になり、目立たせたい部分を強調できる。  
しかし、githubではフォントの色を変えられない。**不便！**  
slackを見習ってほしい。  


## おまけ
Markdownの書き心地だけ考えると、Qiitaのほうが書きやすい気がする。文字の色や背景がはっきり変わる機能がgithubにはないのが残念・・・・。
