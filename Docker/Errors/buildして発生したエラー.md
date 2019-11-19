## buildして発生したエラー

https://github.com/AsiaQuestCoLtd/levelup-nagayoshi  
ボーリング問題で使ったDocker環境構築・ユニットテスト環境構築のファイルを  

https://github.com/AsiaQuestCoLtd/levelup-nagayoshi-platform  
基盤問題でそのまま使おうとしたら発生した。

```
$ docker-compose up -d --build
Creating network "levelup-nagayoshi-platform_default" with the default driver
Building php
[WARNING]: Empty continuation line found in:
    RUN apt-get update && apt-get -y install git unzip zlib1g-dev RUN curl -sS https://getcomposer.org/installer | php
[WARNING]: Empty continuation lines will become errors in a future release.
Step 1/3 : FROM php:7.3
 ---> 6a7b60935d73
Step 2/3 : RUN apt-get update && apt-get -y install git unzip zlib1g-dev RUN curl -sS https://getcomposer.org/installer | php
 ---> Running in c5f5a28178f9
Get:1 http://security-cdn.debian.org/debian-security stretch/updates InRelease [94.3 kB]
Get:2 http://security-cdn.debian.org/debian-security buster/updates InRelease [65.4 kB]
Get:3 http://security-cdn.debian.org/debian-security stretch/updates/main amd64 Packages [508 kB]
Get:5 http://security-cdn.debian.org/debian-security buster/updates/main amd64 Packages [158 kB]
Ign:4 http://cdn-fastly.deb.debian.org/debian stretch InRelease
Get:6 http://cdn-fastly.deb.debian.org/debian stretch-updates InRelease [91.0 kB]
Get:8 http://cdn-fastly.deb.debian.org/debian stretch-updates/main amd64 Packages.diff/Index [12.5 kB]
Get:7 http://cdn-fastly.deb.debian.org/debian buster InRelease [122 kB]
Get:9 http://cdn-fastly.deb.debian.org/debian stretch-updates/main amd64 Packages 2019-09-18-2012.01.pdiff [337 B]
Get:11 http://cdn-fastly.deb.debian.org/debian stretch-updates/main amd64 Packages 2019-10-27-2015.53.pdiff [398 B]
Get:12 http://cdn-fastly.deb.debian.org/debian stretch-updates/main amd64 Packages 2019-11-06-2017.59.pdiff [903 B]
Get:12 http://cdn-fastly.deb.debian.org/debian stretch-updates/main amd64 Packages 2019-11-06-2017.59.pdiff [903 B]
Get:10 http://cdn-fastly.deb.debian.org/debian buster-updates InRelease [49.3 kB]
Hit:13 http://cdn-fastly.deb.debian.org/debian stretch Release
Get:14 http://cdn-fastly.deb.debian.org/debian buster/main amd64 Packages [7908 kB]
Get:16 http://cdn-fastly.deb.debian.org/debian buster-updates/main amd64 Packages.diff/Index [1720 B]
Get:16 http://cdn-fastly.deb.debian.org/debian buster-updates/main amd64 Packages.diff/Index [1720 B]
Get:17 http://cdn-fastly.deb.debian.org/debian buster-updates/main amd64 Packages [5792 B]
Reading package lists...
E: Could not open file /var/lib/apt/lists/deb.debian.org_debian_dists_buster-updates_main_binary-amd64_Packages.diff_Index - open (2: No such file or directory)
ERROR: Service 'php' failed to build: The command '/bin/sh -c apt-get update && apt-get -y install git unzip zlib1g-dev RUN curl -sS https://getcomposer.org/installer | php' returned a non-zero code: 100

```

序盤二つは、Dockerfileに空行があると発生するらしい。エラー文もそう言っている。  
2017年のqiitaの記事にも同様のことが書かれていたが、ボーリング問題を解いているときになぜ発生しなかったのかは不明。WARNINGだから無視してたのかも。  

問題は、一番最後のエラー。  
```
RUN rm -rf /var/lib/apt/lists/* && apt update
```
とりあえず上記のようになるようにDockerfileを修正したけど、よくわからない。  
https://github.com/romaricp/kit-starter-symfony-4-docker/issues/10  
https://askubuntu.com/questions/939345/the-package-cache-file-is-corrupted-error  
