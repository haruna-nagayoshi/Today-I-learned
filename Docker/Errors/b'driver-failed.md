
```
ERROR: for db2_1  Cannot start service db2:
b'driver failed programming external connectivity on endpoint db2_1 (62809bcaf63a7273eaaf7db800e639c47e7f811d6332875c9036fc9cb74f0619):
Error starting userland proxy: mkdir /port/tcp:0.0.0.0:33306:tcp:172.18.0.3:3306: input/output error'
```

こういうエラーが出たら、Docker DesctopをQuitして再起動する必要があるらしい。  
Quitがいつまでたっても終わらないから、タスクマネージャから強制終了させたことが原因かも。  
[Docker コンテナー起動エラー：driver failed programming external connectivity](https://sqlazure.jp/r/tips/1546/)
