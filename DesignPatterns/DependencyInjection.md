## Dependency Injection パターン

ものすごく簡単にいうと、  
AクラスがBクラスに依存しているとき、  
`new B();` をせずに、外側から生成したインスタンスを渡すべしということ。  
そうすることで、密結合から疎結合になる。

## わかったらまとめる
http://blog.a-way-out.net/blog/2015/08/31/your-dependency-injection-is-wrong-as-I-expected/
>DIはデザインパターンであり、ツールであるDIコンテナとは別の概念  


デザインパターンがphpで書かれたもの  
https://github.com/domnikl/DesignPatternsPHP
