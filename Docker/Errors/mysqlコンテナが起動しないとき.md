## 容量不足のためにコンテナが起動できない場合の対処法(このメモすごい役に立った！)

- --initialize specified but the data directory has files in it. Aborting.  
`docker-compose up` (-dなし)で起動したら表示されたエラー。  
「データが空の状態で起動するべきなのに空じゃないからエラーが起きている。データを空にすれば起動する」などの情報を見つけたが、  
もともと空の状態で普段起動しているため、この対策では解決できなさそうと判断した。  
https://qiita.com/n_oshiumi/items/2413665c04ea65904a3c  

- Operating system error number 28.  
前後のエラーはメモし忘れた。  
容量不足のために起動しないことが原因らしい。  
`docker volume prune` で掃除したら正常に起動した。   
https://teratail.com/questions/51944   
https://docs.docker.com/engine/reference/commandline/volume_prune/  

- 2019/10/30 追記

8月に発生したものと同様のエラーが発生した。以前はエラー文を全部貼り忘れていたので掲載しておく。
```
$ docker logs [DBコンテナ名]
Initializing database
2019-10-30T03:46:56.703911Z 0 [Warning] InnoDB: 1048576 bytes should have been written. Only 937984 bytes written. Retrying for the remaining bytes.
2019-10-30T03:46:56.704023Z 0 [Warning] InnoDB: Retry attempts for writing partial data failed.
2019-10-30T03:46:56.704039Z 0 [ERROR] InnoDB: Write to file ./ibdata1failed at offset 8388608, 1048576 bytes should have been written, only 937984 were written. Operating system error number 28. Check that your OS and file system su
pport files of this size. Check also that the disk is not full or a disk quota exceeded.
2019-10-30T03:46:56.704050Z 0 [ERROR] InnoDB: Error number 28 means 'No space left on device'
2019-10-30T03:46:56.704134Z 0 [ERROR] InnoDB: Could not set the file size of './ibdata1'. Probably out of disk space
2019-10-30T03:46:56.704142Z 0 [ERROR] InnoDB: InnoDB Database creation was aborted with error Generic error. You may need to delete the ibdata1 file before trying to start up again.
2019-10-30T03:46:57.305137Z 0 [ERROR] Plugin 'InnoDB' init function returned error.
2019-10-30T03:46:57.305199Z 0 [ERROR] Plugin 'InnoDB' registration as a STORAGE ENGINE failed.
2019-10-30T03:46:57.305210Z 0 [ERROR] Failed to initialize builtin plugins.
2019-10-30T03:46:57.305214Z 0 [ERROR] Aborting

Initializing database
2019-10-30T03:48:16.504674Z 0 [ERROR] --initialize specified but the data directory has files in it. Aborting.
2019-10-30T03:48:16.504791Z 0 [ERROR] Aborting

```

Docker for desctopを再起動したり、コンテナを再起動したりしても解決できなかったので、  
`docker log` コマンドでログを確認したら、どうやら容量が足りていない。  
そんなばかな。2日前はふつうに動いていたのに。  
見覚えがあるなあと思ってTIL確認したら、解決方法があった。

`docker volume ls` コマンドでかなりのdocker volumeがあることがわかった。  
`docker volume prune` でいらないvolumeを削除して、マイグレーション実行して元通り復活！仕事する！
