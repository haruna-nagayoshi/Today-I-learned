## セッション
異なるリクエスト間で同じ値を利用したい場合に使う。  
たとえば、ログイン情報とか、何回アクセスしたかとか？  

#### なぜセッションが必要か
Webはステートレス＝状態を持たないべきである。  
1回目のリクエストでも、n回目のリクエストでも、同じ値でリクエストしたなら常に同じレスポンスが返ってくることを保証されていなければならない。  

しかし、それだけではWebアプリケーションは成り立たない。そこで活躍するのがセッションである。  
セッションはサーバー側で状態を保持していて、ログイン情報や買い物かごの情報などが含まれている。  

つづく　たぶん