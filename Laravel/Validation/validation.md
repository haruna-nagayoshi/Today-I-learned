# バリデーション

## laravelのバリデーションがイメージとは違う
#### 結論
[公式](https://laravel.com/)や
[日本語訳](https://readouble.com/laravel/5.5/ja/validation.html#available-validation-rules)
の解説文を読むだけだと誤解を生む可能性があるので、コードもよく読んでおくべき。  
ということを分かっているならこの先は読まなくていい。  

#### 内容

* alpha系はA,B,C,...をバリデートするわけではない
→日本語の日常会話で「アルファベット」というと「A,B,C,...」と英字を指すことが多い。  
が、本来の意味は「文字そのもの」で、海外ではこちらの意味で使われる。
(以下[weblio](https://www.weblio.jp/content/%E3%82%A2%E3%83%AB%E3%83%95%E3%82%A1%E3%83%99%E3%83%83%E3%83%88)より)
>アルファベット（英: alphabet）は、ひとつひとつの文字が原則としてひとつの子音または母音という音素をあらわす表音文字の一種であり、
また、それを伝統的な配列で並べたものをいう。
「アルファベット」という語は、ギリシア文字の最初の2文字 α, β の読み方である「アルファ」（ἄλφα）、「ベータ」（βήτα）に由来する。

Laravelの定義済みバリデーションalpha, alpha_num, alpha_dash もそのような意味で名づけられている。  
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
pL, pM, pNとは、
つづく


* [numericは数字であることをバリデートするわけじゃない(未確認)](https://hnw.hatenablog.com/entry/20180414)  
→ギリシャ数字だけでなく、ローマ数字なども含むらしい。

