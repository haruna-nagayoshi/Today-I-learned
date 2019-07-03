# laravelのalphaバリデーションが日本語でのイメージとは違う
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

(以上[weblio](https://www.weblio.jp/content/%E3%82%A2%E3%83%AB%E3%83%95%E3%82%A1%E3%83%99%E3%83%83%E3%83%88)より)

Laravelの定義済みバリデーション `alpha` ,  `alpha_num` , `alpha_dash` も、恐らくこのような意味で名づけられている。  
もし、「 `[a-zA-Z]` であること」をバリデートするバリデーションが必要な場合は、オーバーライドするか、独自のバリデーションを新たに定義しなければならない。  

####  `alpha` ,  `alpha_num` , `alpha_dash` に共通する、 `[\pL\pM\pN]` とは何か
バリデーションの定義をみると、次のように書いてある。

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
つまり、 `[\pL\pM\pN]` は、以下の文字を含むということになる。
```
L  アルファベット (Letter)	Ll、 Lm、Lo、Lt および Lu を含む
M  記号 (Mark)
N  数字 (Number)
```
Unicode 文字プロパティに含まれる、実際の値はこのサイトに書かれているものだと思われる。
https://www.fileformat.info/info/unicode/category/index.htm


#### 参考
https://blog.tes.co.jp/entry/2018/06/29/145450  
https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/character-classes-in-regular-expressions#unicode-category-or-unicode-block-p  

## 未確認
* 正規表現の中で日本語などのマルチバイトを使ってマッチさせるには、パターン修飾子の u を付けて、  
パターンと対象文字列を UTF-8 として処理するように明示する必要があるらしい（文字コードが UTF-8 であるのが前提）。  

以下参考サイト  
[PHP の preg_replace には u 修飾子をつけた方がいい](https://tinybeans.net/blog/2016/03/14-110954.html)  

[[PHP]preg_matchの正規表現の中で日本語（マルチバイト文字）を使う](http://codaholic.org/?p=1671)  

[私の正規表現におけるポリシー](https://qiita.com/mpyw/items/8dd5378cb01c877e1f7b#pcre%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE%E9%96%A2%E6%95%B0%E3%81%AE%E4%BF%AE%E9%A3%BE%E5%AD%90%E3%82%84%E3%83%A1%E3%82%BF%E6%96%87%E5%AD%97%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%B3%A8%E6%84%8F)  

* [numericは[0-9]であることをバリデートしていない(未確認)](https://hnw.hatenablog.com/entry/20180414)  
→ギリシャ数字だけでなく、ローマ数字なども含むらしい。  

## 疑問
[a-zA-Z0-9_-]は、_以降という表現にならないのか？  
`[-{] ` だと、`{` まで、という意味になるのに・・・？ 
[ASCII](https://ja.wikipedia.org/wiki/ASCII)が基準だから、 `[-{] ` は「最初から{までの文字」ということになるのだろうか...｡
