## 返り値の型 :self
traitや親クラスで `return $this` するとき、  
返り値の型を `self` にしないと継承する側で継承する側のクラスを返すことができない。  
https://asia-quest.slack.com/archives/GRFCKT5KL/p1583308128221500  

プロパティの `self` 定義となんか感覚が違う気がする・・・。  
`self` プロパティは定義時のクラスを指すのに、返り値の型での `self`は実行時のクラスを指すのか・・・・？  

#### 参考
https://qiita.com/niisan-tokyo/items/af3718a6d67d3e29d686#オブジェクトの型   
