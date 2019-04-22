## アクセス元IPアドレスの取得方法

通常、AWSのCloudFrontやロードバランサーを経由してWEBサーバにアクセスする場合、  
リクエストからIPアドレスを取得すると、直前のIPアドレスが取得される。
```
Client 150.xx.xx.xx  
↓  
CloudFront 54.xx.xx.xx (Client IP = 150.xx.xx.xx)  
↓  
ELB 172.xx.xx.xx (Client IP = 54.xx.xx.xx)  
↓  
Nginx (Client IP = 172.xx.xx.xx)  
```
そのため、Nginx側で設定を変更する必要がある。  

信頼するIPアドレスとしてCloudFrontのIPアドレス一覧を指定する場合、  
CloudFrontのIPアドレスは増減する恐れがあることを考慮しなければならない。  

#### 参考
https://christina04.hatenablog.com/entry/2016/10/25/190000  
https://int128.hatenablog.com/entry/2017/09/13/143702  
https://blog.manabusakai.com/2016/11/nginx-realip-apache-remoteip/
