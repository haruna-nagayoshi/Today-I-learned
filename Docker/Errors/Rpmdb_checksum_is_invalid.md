## Rpmdb checksum is invalidというエラーでコンテナが起動しない
PC移行に伴い、今まで使っていた環境をもう一度構築していたら、  
次のようなエラーメッセージが出てDockerコンテナが立ち上がらなくなった。  
`Rpmdb checksum is invalid: dCDPT(pkg checksums): sudo.x86_64 0:1.8.23-3.el7 - u`


### 回避方法
このエラーに対して  
いろんなひとが対応策を考えたけど、本来必要なものではない  
・yum install -y <パッケージ> をするたびに RUN rpm --rebuilddb  
・RUN yum ..... | true としてエラーコードを無理やり true にする  

そこでつくられたのがこのパッチ  
https://github.com/CentOS/sig-cloud-instance-images/issues/15#issuecomment-252563831

```
# yum-plugin-ovlプラグインをインストール
RUN yum install -y yum-plugin-ovl
```

OverlayFSが問題の原因らしいけどよくわからない  
わかったら追記する。  
https://qiita.com/skame/items/f1c755d66256b750b3e8  
https://eidera.com/blog/2017/08/29/docker_to_old_amazon_linux/  
https://medium.com/@fkei/docker-rpmdb-checksum-is-invalid-dcdpt-pkg-checksums-xxxx-amzn1-u-%E5%AF%BE%E5%87%A6%E6%B3%95-289b8c58d4a3  
https://github.com/moby/moby/issues/10180  
