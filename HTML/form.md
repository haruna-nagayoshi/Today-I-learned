# formタグ

## 経緯
Laravelのソースを読んでいて、  
formタグがフォームのinput要素を囲まずにすぐに閉じタグで閉じている部分があった。  
子要素として囲んでいないとだめんじゃないっけ？と思って調べた。  

## 概要
formタグ同士は、入れ子構造にすることができない。

**NG例**
```php
<form>
    <input type="checkbox">
    <form>
    <input type="text">
    <input type="submit" value="送信">
    </form>
</form>
```
**ではどうするか**  
inputタグのform属性を用いることで、子孫でないinput要素も同じformの要素として扱うことができる。  
たとえば、削除用のフォームに `delete` というid属性をつけ、  
削除用フォームに含みたいinput要素のform属性に `delete` をつけると、formタグの子孫にしなくてもフォームの要素として扱うことができる。  
(LaravelColectiveで書いた)  
```php

<div>
    {{ Form::open([
        'id' => 'delete',
        'route' => 'delete',
        'method' => 'DELETE',
    ]) }}
    {{ Form::close() }}

    {{ Form::checkbox("delete_ids[{$account->id}]", $account->id, false, [
        'form' => 'delete',
        'class' => 'target-checkbox'
    ]) }}
    {{ Form::open([
        'id' => 'store',
        'route' => 'notifications.store',
        'method' => 'POST',
    ]) }}
    {{ Form::close() }}
    {{ Form::text('name', null, [
        'form' => 'store',
    ]) }}
    {{ Form::textarea('email', null, [
        'form' => 'store',
    ]) }}
    {{ Form::submit('登録', [
        'form' => 'store',
        'class' => 'btn btn-danger create',
    ]) }}
    
    {{ Form::submit('削除', [
        'form' => 'delete',
        'class' => 'btn btn-default delete',
        'disabled',
    ]) }}
</div>
```

## 参考
https://qiita.com/k5trismegistus/items/eda92664037f96f40e37


## 追記
調べたことが今日、すごい役に立った。
保守前は<a>タグとJavascriptで書いてあった「フォームの値を渡す」と「値を保持して前のページに戻る」ボタンを素のPHPで実装をしなければならなかった。  
form属性を使えばHTMLの構成をごっそり変えずに済んだ。  
うーん...でも読みやすさからいうと、hiddenが並ぶformとボタンはセットにしたほうがいいのか？  

#### input type="submit" のvalueを改行したいとき
[この記事](https://www.webantena.net/html/input-type-value-new-line/)が役に立った。  
実体参照とやらではうまくいかなかったので、buttonタグで実装した。おかげでcssを書き換える必要があったけど...
