## CLL Version 1.1 におけるlujvo作成アルゴリズム
fi'e [la .sozysozbot.](http://twitter.com/sosobotpi)

---------

### 0. 概要
ロジバンにおいて、lujvo（複合語）を作る規則は意外とめんどくさいし、聖典CLLの説明は分かりにくい。さらに、英語資料は一応あるもののまとまった日本語資料が見当たらない。  
ということで、jvozbaを[再発明](https://sozysozbot.github.io/sozysozbot_jvozba/sozysozbot_jvozba.html)した筆者が実装時のわーきゃーを踏まえながら解説記事を書いてみようと思う。  
なお、筆者が理解していないので、意味論には触れない。

---------

### 1. rafsi
[CLL 4.6](http://lojban.org/publications/cll/cll_v1.1_xhtml-no-chunks/#section-rafsi)に丸投げします  
…  
…  
…  
…  
…  
…  
と、言えたらどんなに嬉しいことか。  
困ったことに、CLLはrafsiに関して自己矛盾を含んでいるのである。  
その話は後で触れるとして、まずはサラッとrafsiについて解説する。そもそも「英語を読まずにlujvoの仕様を理解させる」のがこの記事の目標なので。  
  
rafsiとは、複合語(lujvo)を生み出すための形態素で、その形には8種類ある。

3文字:

形 | 例
--- | ---
Cvv | -bau-
CCV | -jbo-
Cv'v <sup>[1](#foot1)</sup> | -ma'o-
CVC | -sel-

4文字:

形 | 例
--- | ---
CCVC | -plis-
CVC/C | -karc-

5文字:

形 | 例
--- | ---
CCVCV | -plise-
CVC/CV | -karce-


--------

<a name="foot1">1</a>: アポストロフィは文字数に入れないので-ma'o-も3文字rafsi
