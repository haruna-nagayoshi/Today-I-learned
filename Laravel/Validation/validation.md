# laravelのバリデーションが日本語でのイメージとは違う
## 結論
* [公式](https://laravel.com/)や
[日本語訳](https://readouble.com/laravel/5.5/ja/validation.html#available-validation-rules)の解説文を読むだけではだめで、コードを読むべき。  
* Laravelの `alpha` バリデーションは正規表現でいう `[a-zA-Z]` ではない。  
ということを分かっているならこの先は読む必要はない。  

## 内容
#### `alpha` はA,B,C,...をバリデートするわけではない
→日本語の日常会話で「アルファベット」というと「A,B,C,...」と英字を指すことが多い。  
が、本来の意味は「文字そのもの」で、海外ではこちらの意味で使われる。
>アルファベット（英: alphabet）は、ひとつひとつの文字が原則としてひとつの子音または母音という音素をあらわす表音文字の一種であり、
また、それを伝統的な配列で並べたものをいう。
「アルファベット」という語は、ギリシア文字の最初の2文字 α, β の読み方である「アルファ」（ἄλφα）、「ベータ」（βήτα）に由来する。

([weblio](https://www.weblio.jp/content/%E3%82%A2%E3%83%AB%E3%83%95%E3%82%A1%E3%83%99%E3%83%83%E3%83%88)より)

Laravelの定義済みバリデーション `alpha` ,  `alpha_num` , `alpha_dash` もこのような意味で名づけられていると思われる。  
もし、「 `[a-zA-Z]` であること」をバリデートするバリデーションが必要な場合は、オーバーライドするか、独自のバリデーションを新たに定義しなければならない。  

####  `alpha` ,  `alpha_num` , `alpha_dash` に共通する、 `[\pL\pM\pN]` について
バリデーションの定義の中身をみると、 `preg_match('/^[\pL\pM\pN_-]+$/u', $value)` と書いてある。

```php
    /**
     * Validate that an attribute contains only alpha-numeric characters, dashes, and underscores.
     *
     * @param  string  $attribute
     * @param  mixed   $value
     * @return bool
     */
    public function validateAlphaDash($attribute, $value)
    {
        if (! is_string($value) && ! is_numeric($value)) {
            return false;
        }

        return preg_match('/^[\pL\pM\pN_-]+$/u', $value) > 0;
    }
```
pL, pM, pNとは、[PHPマニュアル](http://php.net/manual/ja/regexp.reference.unicode.php)によるとUnicode 文字プロパティのこと。  
つまり、 `[\pL\pM\pN]` と定義すると、以下の文字を含むということになる。
```
L  アルファベット (Letter)	Ll、 Lm、Lo、Lt および Lu を含む
M  記号 (Mark)
N  数字 (Number)
```

https://en.wikipedia.org/wiki/Template:General_Category_(Unicode)
Letter Mark Numberが指定されるということ。
https://www.fileformat.info/info/unicode/category/index.htm

でもMarkに該当すると思われるものをPOSTMANで投げてみてもバリデーションエラーになる

他参考
https://blog.tes.co.jp/entry/2018/06/29/145450
https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/character-classes-in-regular-expressions#unicode-category-or-unicode-block-p (edited)

【やったこと】
①Markに当てはまるのは、
濁点やアクセント記号のような
文字に添えられる記号(例：Ã)らしいが、
~やÃを入れても弾かれる。なぜだ。

②
しかも、ひらがなでも、「あ」は通過するが、「ほ」は通らない。
これは境目があるのでは？と思い、試しにあいうえお順に「ほ～ん」で入れてみると弾かれる。濁点をつけても同様。
「あ～へ」を全て試すのはしんどいので、いくつかランダムに入れてみたけど、「あ」「う」「こ」「て」「ぎ」「べ」「ぺ」などは通る。
しかし「ぜ」は入らなかった　？？？
https://www.fileformat.info/info/unicode/category/Lo/list.htm
このリストを信じてよいのであれば、「ぺ」と「ほ」が境界になっているのか？
記号とは文字に結合されているものを指し単体の「゛」「゜」は含まないということか？
と思ったけど、どうも違うらしい。
「さ」「ざ」は通るのに「そ」「ぞ」「せ」「ぜ」は通らない。
「て」「で」は通るのに「だ」「た」は通らない。
カタカナは恐らく全滅。
漢字は、漢数字の「一」はBadRequestになる。なんでだ。「二」はバリデーションエラーとして弾かれる。

結局alphaはどういうバリデーションなんだ？？？
Unicodeで指定されているLMNなんだから、同じはずなんだけど・・・

【やったこと2】
↑で試したことは、GETパラメータで試していたから発生していたことがわかった。
URLに書いたひらがなは別の文字に変換されていた。
例) 000ざ　→　000V

JSONで渡したら平仮名も片仮名もOKだった。
でも、濁点や鍵括弧などは通らない・・・ (edited)

haruna nagayoshi パ [1 month ago]
alpha /^[pLpMpN]+$/u
custom_alpha_num /^[pLpMpN]+$/
二つの違いは、最後にuがつくかつかないか。
このuは、パターンと対象文字列をUTF-8として扱うためのものらしい。

https://tinybeans.net/blog/2016/03/14-110954.html

これを回避するには、正規表現にパターン修飾子の u を付けて、パターンと対象文字列を UTF-8 として処理するように明示します（文字コードが UTF-8 であるのが前提）。

マルチバイト対応、にするためのもの？
http://okumocchi.jp/php/re.php (edited)

haruna nagayoshi パ [1 month ago]
http://d.hatena.ne.jp/sutara_lumpur/20100904/1283565264
検索対象の中にある日本語が合っても、
正規表現のなかに日本語がなければu修飾子はつけなくてもいいらしい？？？

絵文字バリデーションとかも、/uつけないとだめ？
つけなくてもよい？
はてなダイアリー
【PHP】preg系で日本語を使う場合、パターン修飾子『u』は不可欠 - すたら日記
結論 (2018年8月2日現在) 検索対象にマルチバイト文字が含まれていても、抽出したい文字に含まれていなけれ..


http://codaholic.org/?p=1671
やっぱ正規表現のなかに日本語があるときuが必要？
Codaholic
[PHP]preg_matchの正規表現の中で日本語（マルチバイト文字）を使う
正規表現の中で日本語（マルチバイト文字）を使ってマッチさせるには、パターン修飾子というものを使う必要がありまし…



https://qiita.com/mpyw/items/8dd5378cb01c877e1f7b#pcre%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE%E9%96%A2%E6%95%B0%E3%81%AE%E4%BF%AE%E9%A3%BE%E5%AD%90%E3%82%84%E3%83%A1%E3%82%BF%E6%96%87%E5%AD%97%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%B3%A8%E6%84%8F
そうっぽい 

#### 疑問
[a-zA-Z0-9_-]は、_以降という表現にならないのか？
[-{] だと、　{まで、という意味になるのに・・・？


#### いつか調べる
* [numericは[0-9]であることをバリデートしていない(未確認)](https://hnw.hatenablog.com/entry/20180414)  
→ギリシャ数字だけでなく、ローマ数字なども含むらしい。

