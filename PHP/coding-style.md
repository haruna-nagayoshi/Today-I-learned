## レビューしてもらうときに気をつけること 
PSR‐2とかそうじゃないものもいろいろ。  
コードを書く時のルールが人によってまちまちだと、とても見づらくなるので統一するべき。  

#### 制御構文の括弧
if, for, whileなどの括弧は、
* `{` の前は改行しない。
* `}` の前は改行する。
* `(` の前に空白スペースを空け、後には空けない。
* `)` の後に空白スペースを空け、前には空けない。

```php
if( $age>20 )
{ // 処理 }
```
↓
```php
if ($age > 20) {
    // 処理
}
```

#### クラス、メソッドの括弧
クラス、メソッドの括弧は、
* `{` の前は改行する。
* `}` の前は改行する。
* `(` の前後に空白スペースを空けない。
* `)` の後に空白スペースを空け、前には空けない。

```php
class MessageBag {
    public function __construct( $array = [] ) {
        // 省略
    }
}
```
↓
```php
class MessageBag
{
    public function __construct($array = [])
    {
        // 省略
    }
}
```

#### 引数
引数のカンマの前にはスペースを入れず、後ろには1つのスペースを入れる。
```php
public function __construct($key,$value ,$message) {

}
```
↓
```php
public function __construct($key, $value, $message) {

}
```

#### else ifより、elseifを使う
elseif分岐をあまり書かないから意識してなかったけど、AtCorderで解いた問題を見返したらelse ifって書いてた・・・。  
[マニュアル](https://www.php.net/manual/ja/control-structures.elseif.php)によると、どちらを使っても挙動は全く同じだけど、文法的には異なる。
else if を使った場合、さらにネストが深くなることになるらしい。
参考  
http://piyopiyocs.blog115.fc2.com/blog-entry-937.html  
https://blog-ja.sideci.com/entry/PHP-codingstyles  

#### マジックナンバーを使わない
マジックナンバーとは、　　　あとでかく  
意味のある変数名に変えたり、Enumを利用する。  
```php
$name1 = 'Taro';
$name2 = 'Tanaka';
```
```php
// 青信号ってどれだっけ？
if ($trafficLight === 1) {
    // 処理
} elseif ($trafficLight === 2) {
    // 処理
} elseif ($trafficLight === 3) {
    // 処理
}
```
↓
```php
$firstName = 'Taro';
$lastName = 'Tanaka';
```
```php
// Enumの定義は省略
if ($trafficLight === TrafficLight::bule) {
    // 処理
} elseif ($trafficLight === TrafficLight::yellow) {
    // 処理
} elseif ($trafficLight === TrafficLight::red) {
    // 処理
}
```

#### PHPDocを書く
主にPhpStormによる補完のために書く。
`/** + Enter` で自動入力される。

#### コメントを書かない
クラス名、関数名、変数名でどんな処理なのかを表すことができれば、コメントは必要ない。  
クラス名、関数名、変数名で表せないということは、書く能力がないと言っているようなもの。(みたいなことがClean Codeに書いてあった)  
```php
// 企業ID
$id = 123;
// 企業名
$name = 'ABC';
```
```php
$companyId = 123;
$companyName = 'ABC';
```
コメントを書いてよいのは、特別な理由があって通常とは異なる処理をしているときなどに限る。  
```
// 一般的には処理速度の速い処理Aを実行するべきだが、〇〇のため処理Bを行う。
if ($a > 1000) {
    // 処理B
}
```

#### 無意味な空白スペース、空行を書かない。
たとえば、変数への代入が並ぶとき、=の位置を揃える必要はない。
```php
$id    = 123;
$name  = 'ABC';
$eamil = 'example@example.com';
```
↓
```php
$id = 123;
$name = 'ABC';
$eamil = 'example@example.com';
```

#### Don't Repeat Yourself DRY原則

#### YAGNI原則

## かんそう
書こう書こうと思って数日経過してやっと書けた・・・。ずっとごろごろしてたくもあり出かけたくもあり・・・。  
意外と書くのに時間がかかる。  
