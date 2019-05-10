## レビューしてもらうときに気をつけること 
PSR‐2とかそうじゃないものもいろいろ。  
コードを書く時のルールが人によってまちまちだと、見づらくなるので統一するべき。  

[PHP 公式マニュアル](https://www.php.net/manual/ja/index.php)  
[PSR-2](https://www.php-fig.org/psr/psr-2/)  

#### returnの前は改行する
たまに忘れる。  
コードは処理のまとまりごと・意味ごとに書いたほうが分かりやすい。処理内容と結果は分けてかく。
```php
if ($age > 20) {
    return 'お酒が飲めるよ';
}
return 'お酒はダメ';
```
↓
```php
if ($age > 20) {
    return 'お酒が飲めるよ'; // return1行だけの場合は改行しなくてよい
}

return 'お酒はダメ';
```

#### 制御構文の括弧
if, for, whileなどの括弧は、
* `{` の前は改行しない。
* `}` の前は改行する。
* `(` の前に空白スペースを空け、後には空けない。
* `)` の後に空白スペースを空け、前には空けない。

```php
if( $age>20 )
{ // 処理 }

↓

if ($age > 20) {
    // 処理
}
```

```php
for ( $i=1;$i<$n;$i++ ) {
    // くっついてると、ぱっと見分かりにくい。
}

↓

for ($i = 1; $i < $n; $i++) {
    // 四則演算、等号、不等号などの記号の前後は半角スペースを空ける。  
    // ;の後に空白スペースを空ける。
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

↓

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

↓

public function __construct($key, $value, $message) {

}
```

#### else ifより、elseifを使う
elseif分岐をあまり書かないから意識してなかったけど、AtCorderで解いた問題を見返したらelse ifって書いてた・・・。   
[マニュアル](https://www.php.net/manual/ja/control-structures.elseif.php)によると、どちらを使っても挙動は全く同じだけど、文法的には異なる。  
else if を使った場合、一段階ネストが深いif ~ else ~ になるらしい。  
参考  
http://piyopiyocs.blog115.fc2.com/blog-entry-937.html  
https://blog-ja.sideci.com/entry/PHP-codingstyles  

#### マジックナンバーを使わない
マジックナンバーとは、　　　あとでかく  
意味のある変数名に変えたり、Enumを利用する。  
```php
$name1 = 'Taro';
$name2 = 'Tanaka';

↓

$firstName = 'Taro';
$lastName = 'Tanaka';
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

↓

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
主にPhpStormによる補完のために、メソッドの前に書く。  
`/** + Enter` で自動入力される。  
PHPDoc内でも、returnの前は1行空ける。  

#### コメントを書かない
クラス名、関数名、変数名でどんな処理なのかを表すことができれば、コメントは必要ない。  
クラス名、関数名、変数名で表せないということは、書く能力がないと言っているようなもの。(みたいなことがClean Codeに書いてあった)  
```php
// 企業ID
$id = 123;
// 企業名
$name = 'ABC';

↓

$companyId = 123;
$companyName = 'ABC';
```

コメントを書いてよいのは、特別な理由があって通常とは異なる処理をしているときなどに限る。  
```php
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

#### 否定の!は後ろに空白スペースを入れる。
```php
if (!$this->messages->has($attribute)) {
    // ...
}

↓

if (! $this->messages->has($attribute)) {
    // こっちのほうが見やすい
}
```

#### ファイルの末尾には空白を1行入れる。  
gitで管理する場合？

#### Don't Repeat Yourself DRY原則
あとでかく  
※必ずしもこの原則が正しいわけではない。  

#### YAGNI原則
"You ain't gonna need it"  
YAGNI とは、実際に必要となるまでは機能を追加しないのがよいとする原則。  
コードを書くときは、必要なものを必要になったときに書けばよく、先回りして「必要になりそうなもの」を書くことはしない。  
※必ずしもこの原則が正しいわけではない。  

## かんそう
書こう書こうと思って数日経過してやっと書けた・・・。ずっとごろごろしてたくもあり出かけたくもあり・・・。  
意外と書くのに時間がかかる。  
