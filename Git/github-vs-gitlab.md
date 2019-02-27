# GitlabとGithub

## 概要
先日、社内でGithubが利用できるようになった。違いがわからないので調べてまとめる。  
Gitとは、ソースコードやファイルのバージョン管理のシステムで、  
Gitを使いやすくするツールがGitlabやGithub、Backlogなど。  

## 結論
いろんなところで議論はされているものの大きな違いはないらしい。  
Githubのほうが歴史が古く、サポートが手厚い、というくらい？  
「GitとGithubの関係は、メールとGmailの関係に似ている」という記述を何回か見かけたので、  
個人の好みとか、料金とか、2社間で共有したい場合はGitlabやBacklogを使うなど、それぞれの理由で使い分けをしているのかもしれない。  

#
## 共通点
#### board
Trelloのように、カンバン方式でissueを管理できる。  
Assigneeに応じてアイコンが表示される機能や、Label機能がある。  

(githubだと、cardをただのTODOリストとしても使えるし、cardとissueを紐づけることもできる。gitlabではissueだけのboardのイメージ)  
![image](https://user-images.githubusercontent.com/38639386/53464734-c5cfae80-3a8e-11e9-8ff5-4bcbbdf5a1c3.png)

#### 画像の自動生成
画像をコピーしてissue上でペーストすると、自動でリンクが生成され、画像を貼ることができる。    

Githubのwikiや.md上では自動生成されないが、issueを適当に作って生成されたリンクを使えば、wiki等でも利用できる。  
画像保存用のリポジトリやブランチを作成する方法もあるらしいが、画像を貼りたいだけならこの方法でいいと思う。  
どの方法にしろ面倒なので、どこでも自動生成できるようにしてほしい。  


#
## 相違点
Gitlabのほうが料金が安い。作っているのはGitlab社。  
Githubのほうが歴史が長いので規模も大きいためユーザ数が多く、世界中の人とソースを共有できるので、教え合える可能性が高い。作っているのはMicrosoft。  

#### PullRequestとissueの番号
Gitlabでは、MRとissueの番号は生成した順に振られていくので、番号は必ずしも一致しない。  
GitHubでは、PRとissueの番号が一致するようになっている。(ということは、issueを作らずにPRしたら、issueの番号には空きが発生する？)  

#### Shortcut Key
どちらもショートカットキーがあるが、微妙に違うのでややこしい。  
仕事でGitlabを使っているが、プロジェクトが複数あるので Shift + P は便利かも。でもどの階層なら使えるのかいまいちわかりにくいので、マウスで十分だと思う。    
Gitlabのショートカット一覧(ツールバー→Help→Quick help→Use shortcutsで見れる)    
![image](https://user-images.githubusercontent.com/38639386/53463877-98353600-3a8b-11e9-8d9c-03ca9d7fccb0.png)

Githubのショートカット一覧  
?キーを押下するとチートシートが表示される。    
もしくは、詳細な説明付で一覧が見れる。[Using keyboard shortcuts](https://help.github.com/en/articles/using-keyboard-shortcuts)  

#### Markdown
Gitlabでは、バッククオートで文字を囲むとフォントが赤色になり、目立たせたい部分を強調できる。  
しかし、Githubではフォントの色を変えられない。**不便！**  
slackを見習ってほしい。  


## おまけ
- ディレクトリを好きなように作れるから分類しやすいと思ってGithubを試しに使っているけど、Markdownの書き心地だけ考えるとQiitaのほうが書きやすい。文字の色や背景がはっきり変わる機能がGithubにはないのが残念・・・・。
- [共同編集者は3人までだけど、Githubは無料でプライベートリポジトリを作れるようになった](https://github.blog/2019-01-07-new-year-new-github/)ので、たいした差がないのならサポート面が厚いGithubのほうがよいのかも。
