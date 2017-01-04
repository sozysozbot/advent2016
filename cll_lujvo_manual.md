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
その話は[別記事（未うｐ）](https://sozysozbot.github.io/FIXME)で触れる<sup>[1](#foot1)</sup>として、ここではサラッとrafsiについて解説するのみにしておく。  
rafsiとは、複合語(lujvo)を生み出すための形態素で、その形には8種類ある。
Cが子音、CCが「語頭に立ちうる二重子音」を表す。C/Cは「語中にあり得る二重子音」。

3文字:

形 | 例
--- | ---
Cvv | -bau-
CCV | -jbo-
Cv'v <sup>[2](#foot2)</sup> | -ma'o-
CVC | -sel-

CvvとCv'vを合わせてCVVと呼ぶ。なお、vvとしてはai, ei, au, oiの4通りのみが用いられる。

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

なお、5文字rafsiはlujvo末でのみ使うことができる。  
<br>

結論から言えば、lujvoはこのrafsiをくっつけていけば作れるのだが、そのくっつけるための規則がめんどくさいのである。以下その規則を解説していく。

--------

### 2. rafsiをくっつけるPart1
まず大前提として、lujvoはbrivlaなので、lujvo末には母音で終わるrafsiが来なくてはならない。  
それが済んだら、rafsiをくっつけていけばいいが、諸事情により「ハイフン字」（`y`, `n`, `r`）がrafsi間に挿入されることがある。「諸事情」とは、

* 4文字rafsi  
* 禁則回避  
* 剥がれ落ち防止  

の3パターンである。まずは前2つを解説する。
  
  
  
#### 2-1. 4文字rafsi
4文字rafsiの後ろには必ず`y`が必要である。  

例：  
-plis- + -ladru- → plis**y**ladru

これは、lujvoを一意に分解するのに必要な規則である。この規則と、lujvoの2文字目には絶対にyが来ないということから、先頭を読むだけで {plisyladru} が *[-pli- + syladru] ではなく [-plisy- + ladru] であることを知ることができるのだ。流石LLG、賢い。  
ちなみにこの例でyを抜かすと{plisladru}となるが、これは[-pli- + -sla- + -dru-]である。CVC/C型については{karctadji}を考えてみよう。
  
  
  
#### 2-2. 禁則回避
そのままくっつけると禁則な子音列が発生する場合、2つのrafsiの間には`y`が要求される。  

例：  
-fam- + -ma'o- → fam**y**ma'o （同一子音の連続を回避）  
-fas- + -bau- → fas**y**bau （無声阻害音＋有声阻害音を回避）  
-cen- + -dje- → cen**y**dje （`ndj`を回避）  

この規則はロジバンの音韻構造の制約を直に受けているだけのものであり、それ以上に深い意味は特にない。

--------

### 3. rafsiをくっつけるPart2
さて、「lujvoを作る」というのは、そもそもどういうことだろうか。 <sup>[3](#foot3)</sup>  
私の考えでは、「ハンバーガー🍔をつくること」に例えられると思う。<sup>[4](#foot4)</sup>  
ハンバーガーの内側の具を入れ替えても、それはまだハンバーガーである。 <sup>[5](#foot5)</sup>  
しかし、「一番上に丸くてゴマのついたパン、一番下に平らなパン」という掟を破って層を配置すれば、ハンバーガーではない。  

lujvoにおいても同様のことが言える。  
前述のとおり、lujvo末のrafsiは母音終わりであることが要求されるが、lujvoの語頭に来るrafsiにも面倒な規則が存在するのだ。  

**☆以下の操作は、具を載せ終わって、最後に上の丸いパンを載せるときにのみ、一度だけ、行います☆** （もちろん、具を載せていく過程で2-1と2-2の操作は行うこと）  
- case 1: 丸いパンが4文字rafsiまたはCCV rafsiの場合  
	- 特別な操作は不要
- case 2: [CVV + CCV]で単語が完成する場合（例： {ma'ovla}, {fu'ivla}）
	- 特別な操作は不要
- case 3: 丸いパンがCVVで、case 2以外のとき
	- CVVの後に`r`を挿入（例： {fa'orma'o}, {fu'irvlarafsi}）
	- ただし、直後に既に`r`がある場合は挿入されるのは`n`（例： {ka'enri'u}）
- case 4: 丸いパンがCVCのとき
	- 3-1へ進む

#### 3-1. tosmabruテスト
先頭にCVCを付けたものがαとβのどちらか片方に該当する場合にのみ、α, βの形ではなく、先頭のCVCの後に`y`をねじ込んだ形が採用される。   
 
α [（1個以上のCVC） + CVCCV<sup>[6](#foot6)</sup>] かつ、くっつけた時全ての子音結合がCCである  
β [（2個以上のCVC） + `y` + （1個以上の任意のrafsi）] かつ、y以前の全ての子音結合がCCである  

従って、
- [-cas- -tadji-] → {cas**y**tadji} （全てCC）
- [-kan- -tadji-] → {kantadji} （`nt`はC/C）
- [-cas- -kan- -tadji-] → {caskantadji} （`sk`はCCだけど`nt`はC/C）
- [-pas- -pas- -y- -badna-] → {pas**y**pasybadna} （`dn`はC/Cだが判定にかかるのは`paspasy`の部分まで）

--------
### 4. 以上です
お疲れさまでした。  
本当はlujvoの得点の話とか、この方法で一意に分解できることの証明とかやりたいんですが、それはまたの機会に

--------
### 脚注

<a name="foot1">1</a>: 無駄に長くなりそうなので分離  
<a name="foot2">2</a>: アポストロフィは文字数に入れないので-ma'o-も3文字rafsi  
<a name="foot3">3</a>: なんかポエム始まったぞ  
<a name="foot4">4</a>: 駄目だこいつ…早くなんとかしないと…   
<a name="foot5">5</a>: 「肉が入ってないものは厳密にはハンバーガーとは呼べない」などの指摘は受け付けません。ご了承ください。  
<a name="foot6">6</a>: CVC/CVとは言っていない。ゆえに{mabru}にはマッチするが{mapku}にはマッチしない
