## self と static の違い

#### static
staticなメソッドやプロパティとして定義すると、そのクラスをインスタンス化しなくとも呼び出すことができる。  
※staticなプロパティはインスタンス化したオブジェクトからは呼び出すことはできない。staticなメソッドは呼び出せる。  

####  selfとstaticの違い
staticは、staticプロパティを呼び出したクラスのプロパティをみにいく。  
親クラスを継承した子クラスでstaticプロパティを呼んだら、子クラスのプロパティをみにいく。  

selfは、selfプロパティを定義したクラスのプロパティをみにいく。  
継承先でselfプロパティを読んでも、selfプロパティを定義した親クラスのプロパティを見にいく。  

継承を想定する場合は、staticを使うべきなのか、selfを使うべきなのか、意識する必要がある。  


#### 宿題への解答
今回宿題のきっかけとなったEnumでは、  
StudentTypeクラスを継承することは想定していないため、  
定義した時点のプロパティを呼ぶselfも、呼び出したクラスのプロパティを呼ぶstaticも、どちらも使うことができる。  
でも、意味的には「定義した時点のプロパティ」を呼ぶselfを使うべきだったかも？  

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
