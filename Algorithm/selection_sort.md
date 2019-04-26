# 選択ソート
![image](https://user-images.githubusercontent.com/38639386/56805417-f603b580-6863-11e9-9b56-81479e52afa1.png)

| A[N] | N個の整数でできた配列 |
| ------------ | ------------- |
| i| 未ソートの部分の先頭を示すループ変数で、配列の先頭から末尾に向かって移動する |
| minj| 各ループの処理でi番目からN-1番目までの要素のうち、最小値の位置 |
|j | 未ソートの部分から最小値の位置(minj)を探すためのループ変数 |

未ソート部分から最小値の位置を探し、その位置の要素と未ソート部分の先頭の要素を交換する。
交換されて先頭にきたものはソート済みとする。
これを繰り返し、配列の先頭から小さい順に決定される。

選択ソートは離れた要素を交換するため安定なソートではない？(ここがちょっとわからない)

### 計算量
未ソート部分の最小値を見つけるため、各ループでN-1回、N-2回、N-3、…、1回の比較が行われる。
よって、常に(N^2 - N) / 2 回の比較が行われる。
N^2に比べてNは十分小さいので無視することができ、定数である1/2も無視することができるので、選択ソートはN^2に比例するといえる。

### 問題
入力は、1行目に数列の長さを表す整数N、2行目にN個の整数が空白区切りで与えられる。
出力は、1行目に整列された数列の要素を空白区切り、2行目に交換回数を出力する。

入力
```
6
5 6 4 2 1 3
```

```php
<?php
$arrayCount = trim(fgets(STDIN));
$array = explode(' ', trim(fgets(STDIN)));

list($sortedArray, $sortedCount) = selectSort($arrayCount, $array);

foreach ($sortedArray as $value) {
    echo $value.' ';
}
echo PHP_EOL, $sortedCount, PHP_EOL;

function selectSort($arrayCount, $array)
{
    $sortedCount = 0;
    for ($i = 0; $i < $arrayCount; $i++) {
        $minj = $i;
        for ($j = $i; $j < $arrayCount; $j++) {
            if ($array[$j] < $array[$minj]) {
                $minj = $j;
            }
        }

        $temporary = $array[$i];
        $array[$i] = $array[$minj];
        $array[$minj] = $temporary;
        if ($minj !== $i) {
            $sortedCount++;
        }
    }

    return [$array, $sortedCount];
}
```
出力
```
1 2 3 4 5 6 
4
```

#### 参考
書籍 プログラミングコンテスト攻略のためのアルゴリズムとデータ構造  

[iOSアプリ アルゴリズム図鑑](  https://itunes.apple.com/jp/app/%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0%E5%9B%B3%E9%91%91/id1047532631?mt=8)
↑動くイメージで解説してくれるのですごく分かりやすい。おすすめ。
360円くらい課金すればすべてのソート、データ構造についての解説が見れる。  


#### 感想
せっかく書いたからesaから移動してきた。
ソートについてまとめてみようとおもったけど全部書くのは挫折しそう。
