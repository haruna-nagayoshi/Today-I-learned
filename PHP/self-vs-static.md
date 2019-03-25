## self と static の違い

#### static
staticなメソッドやプロパティとして定義すると、そのクラスをインスタンス化しなくとも呼び出すことができる。  
※staticなプロパティはインスタンス化したオブジェクトからは呼び出すことはできない。staticなメソッドは呼び出せる。  

####  selfとstaticの違い
staticは、プロパティを呼び出したクラスで定義されているプロパティをみにいく。
例) 親クラスを継承した子クラスでプロパティを呼んだら、子クラスのプロパティをみにいく。

selfは、プロパティを定義したクラスのプロパティをみにいく。
例) 子クラスでプロパティを呼び出しても、プロパティを定義した親クラスのプロパティを見にいく。

継承を想定する場合は、staticを使うべきなのか、selfを使うべきなのか、意識する必要がある。  


#### 宿題への解答
今回宿題のきっかけとなったEnumでは、  
StudentTypeクラスを継承することは想定していないため、  
定義した時点のプロパティを呼ぶselfも、呼び出したクラスのプロパティを呼ぶstaticも、どちらも使うことができる。  
でも、意味的には「定義した時点のプロパティ」を呼ぶselfを使うべきだったかも？ → (追記)そうするべきだった。

```
<?php

namespace App\Enums;

use MabeEnum\Enum;

class StudentType extends Enum
{
    const PRIMARY_SCHOOL = 1;
    const JUNIOR_HIGH_SCHOOL = 2;
    const HIGH_SCHOOL = 3;
    const UNIVERSITY = 4;

    /**
     * @return array
     */
    public static function asList(): array
    {
        return [
            // selfでもstaticでも呼べる
            self::PRIMARY_SCHOOL => '小学校',
            self::JUNIOR_HIGH_SCHOOL => '中学校',
            static::HIGH_SCHOOL => '高校',
            static::UNIVERSITY => '大学',
        ];
    }
}
```

#### 参考
[PHP の static と self の違い](https://gotohayato.com/content/488)
[PHPのself::とstatic::の違い](https://tohokuaiki.hateblo.jp/entry/2016/12/16/PHP%E3%81%AEself%3A%3A%E3%81%A8static%3A%3A%E3%81%AE%E9%81%95%E3%81%84)
[PHPで「self::」と「$this」の違いを理解する。](http://note.onichannn.net/archives/648)
