#### 今回のエラー
```
for example_nginx  Cannot start service example_nginx: b'OCI runtime create failed: container_linux.go:344:  
starting container process caused "process_linux.go:424:
```

#### 対処方法
Reset credentialsからいったん認証情報をリセットして、  
PCのアカウント情報を設定しなおせばよいらしい。  [参考](https://seeek.org/)  
Shared drives の部分もチェック付け外ししたからどっちも原因なのか片方が原因なのか不明のまま。  

**追記 認証情報の部分は安易にいじらないほうがいいのかもしれない。**    
1日経ってコンテナ起動しようとしたらCドライブへのマウントが外れていて、  
認証リセットしてカスペルスキーの設定も変更し直したり、WindowsのローカルアカウントのPWを何度も入力したけど、  
チェックが入ることはなかった。  
[参考](https://kantaro-cgi.com/blog/docker/shared-drives-cant-checked.html)  

![image](https://user-images.githubusercontent.com/38639386/55861024-75c92900-5bb0-11e9-8811-512a2a6ee62d.png)
