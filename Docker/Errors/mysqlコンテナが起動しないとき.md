## Errors

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
