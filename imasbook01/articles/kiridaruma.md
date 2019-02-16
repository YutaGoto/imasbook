# アイマス楽曲を歌詞解析してみた話<br><span class="subtitle">～輝きの向こう側に見えたもの～</span>
<p class="right">著:きりだるま</p>

## はじめに

同僚の皆さん、また、プロダクションは違えど同じプロデューサーとして日々を過ごしている皆さん、
いつもプロデュースお疲れ様です。
突然ですが、皆さんの担当アイドルの持ち歌についてじっくり考えたことはあるでしょうか？
ほとんどのプロデューサーは担当の持ち歌について様々な思いを巡らせた経験があると思います。
では質問を変えます。
「アイドルマスターシリーズのすべての曲の歌詞についてじっくりと考えたことがあるでしょうか？」

すべてのアイドルマスターシリーズ関連楽曲。
今自分がこの原稿を書いている2018年11月現在、およそ800曲のアイドルマスター関連楽曲があると言われています。(筆者調べ)
中には、その800曲すべてを覚えている方もいると思いますが、10年以上もの歴史の積み重ねを新規のプロデューサーがすぐに全て理解するのは無理と言えるでしょう。
事実、現在プロデューサー歴5年の自分も、1/3程度の曲は聞いたことすらないと思います。
「なんとか、その10年以上もの積み重ねを手軽に感じることはできないか？」
そう考え、自分は歌詞の解析という一つの見方を提案します。


## 目的とその手法

2018年11月現在、800もの楽曲が存在するアイドルマスターシリーズですが、それらから何等かの情報を引き出し、いわゆる「エモさ」を感じることが目的です。

手法として、歌詞データの自然言語解析を用います。
アイドルマスターシリーズ関連楽曲の歌詞データを対象として、特定の品詞に注目して頻度解析を行います。
また、特定の単語に対しては係り受け解析を行い、その単語にさらに詳細に注目して解析を行います。


## 用意

まず、歌詞データが無いと始まりません。
今回、自分はLyrics Master(\*1)というソフトを用いて、2018年現在声優が決まっている全アイドルについてアーティスト検索を行い、該当する曲の歌詞を収集しました。
また、検索ノイズが激しいアイドルや、一部特殊な楽曲やアイドルは特別に下のように検索/整理を行いました。

<footer>\*1 : Lyrics Master http://www.kenichimaehashi.com/lyricsmaster/</footer>

- ロコ
    - `ロコ 中村温姫`として検索
- ジュリア
    - `ジュリア 愛美` として検索
- アナスタシア
    - `アナスタシア 上坂すみれ`として検索
- 宮本フレデリカ
    - `宮本フレデリカ 高野麻美`として検索
- 萩原雪歩
    - 声優交代前後で別アイドルとして扱い整理しました
- アイドルマスター XENOGLOSSIAシリーズ
    - 非常に迷いましたが、同じアイドルマスターシリーズの一つとして、これらも含めました
- TO D@NCE TOやRearrange曲
    - 大幅に歌詞の違うものは別の曲として扱いましたが、基本的にベースとなった曲以外は除外しました

また、各種データの下処理や自然言語処理には、Rubyでプログラムを書いて行っています。
ライブラリはMeCab(\*2)とCaboCha(\*3)を使用し、辞書はIPA辞書をベースにしたものを使用しました。

<footer>\*2 : MeCab: Yet Another Part-of-Speech and Morphological Analyzer http://taku910.github.io/mecab/</footer>
<footer>\*3 : CaboCha: Yet Another Japanese Dependency Structure Analyzer http://taku910.github.io/cabocha/</footer>

詳しいソースコードはGitHub上で公開しています。(\*4)

<footer>\*4 : imas-lyric-analyzer https://github.com/kiridaruma/imas-lyric-analyser</footer>


解析の対象となる楽曲の範囲ですが、これを書いている2018年11月末現在時点で何らかの形で楽曲が公開され、CD販売/楽曲配信が行われている曲が対象となります。
なので、また数年後にもう一度解析を行えばまた違った結果が出てくる可能性があります。

### 歌詞を扱う際の注意事項

歌詞は立派な著作物です。
ですので、これらを権利者に無断で第三者に公開するのはいろいろとアウトです。
Lyrics Masterでは一般社団法人日本音楽著作権協会(JASRAC)から許諾を取っているWebサイトからデータを取得しました。
読者の皆さんも、歌詞の取り扱いには十分お気を付けください。


## 解析結果

### 結果の見方

解析結果ですが、

```
ほげ : 23
```

といったフォーマットで結果を示します。
これは、「ほげ」という単語が全歌詞中23回出現したという意味になります。

### 各品詞ごとの解析

さて、まずは自立している名詞、動詞、形容詞、感動詞に注目して頻度解析を行った結果です。
上位で100回以上の出現が見られる単語か、上位30単語のみを示していきます。

まずは名詞です。

```
名詞(全22544単語中)
私 : 877
あなた : 763
君 : 750
今 : 566
みんな : 398
今日 : 367
♪ : 340
好き : 333
いつ : 331
人 : 299
さ : 292
どこ : 292
キミ : 287
それ : 286
何 : 280
明日 : 279
誰 : 274
そう : 247
わたし : 238
一緒 : 226
たち : 216
ここ : 207
いつか : 199
大好き : 186
｢ : 185
夜 : 184
前 : 163
時間 : 160
！) : 154
僕 : 148
幸せ : 145
～ : 140
､ : 139
絶対 : 137
｣ : 137
ひとつ : 130
大切 : 123
ら : 122
瞬間 : 115
いま : 112
素敵 : 111
全部 : 105
度 : 105
```

まず、名詞の解析結果でのトップは「私」。
その次に「あなた」、「君」「みんな」と並びます。
やはり、アイドルとして、自身や曲の中での意中の相手に対する言及が数多くあるのでは？と考えられます。
8番目の「好き」、24番目の「大好き」は、恋愛関連の曲が多いという推測ができます。

次に動詞です。

```
動詞(全28788単語中)
する : 1924
なる : 1047
いる : 656
ある : 450
見る : 400
行く : 314
言う : 274
知る : 263
輝く : 242
笑う : 222
信じる : 220
歌う : 208
変わる : 206
待つ : 205
忘れる : 183
なれる : 183
感じる : 171
歩く : 165
伝える : 159
踊る : 146
泣く : 145
届く : 145
見つめる : 142
抱きしめる : 137
来る : 135
描く : 131
思う : 131
できる : 130
見える : 130
終わる : 125
探す : 123
やる : 120
見つける : 114
会う : 112
止まる : 112
生きる : 109
響く : 109
走る : 109
わかる : 107
聞く : 106
言える : 102
続く : 102
会える : 102
飛ぶ : 101
```

上位7単語は「〇〇する」「〇〇になる」といった形で出てくる単語が並んでいます。
8～13番目には「知る」「輝く」「笑う」「信じる」「歌う」「変わる」といった、
**それまで知らなかった世界へ飛び込んで、今までとは変わり、光り輝くステージで笑顔で歌う**
という、まさにアイドルマスターシリーズを連想させる単語です。
また、16番目「なれる」、19番目「伝える」、20番目「踊る」...と、そのほかにも「まさにアイドルマスター」と言える非常に ~~エモい~~ 興味深い単語が並んでいます。

次に、形容詞の解析結果です。

```
形容詞(全4331単語中)
ない : 476
いい : 234
強い : 194
楽しい : 149
優しい : 138
新しい : 127
遠い : 115
嬉しい : 103
熱い : 85
甘い : 82
眩しい : 79
無い : 76
高い : 76
白い : 70
切ない : 61
恋しい : 60
青い : 59
愛しい : 53
早い : 53
怖い : 51
赤い : 47
欲しい : 47
弱い : 44
可愛い : 43
よい : 42
良い : 42
冷たい : 40
やさしい : 39
寂しい : 38
寒い : 37
```

動詞と同じく、「ない」「いい」とノイズともいえる単語が上位2単語に並んでいます。
3番目には「強い」、4番目には「楽しい」、5番目には「優しい」と、ポジティブでパワフルな単語が数多く見られます。
しかし同時に、15番目「切ない」、16番目「恋しい」といった単語や、20番目「怖い」、23番目「弱い」といった、自分の弱さともいえるネガティブなワードも並んでいます。
アイドルもやはり人であり、内面の弱さや脆さを含んでいるという一つの解釈ができます。

最後に、感動詞の解析結果です。

```
感動詞(全1625単語中)
さあ : 241
ほら : 206
ねぇ : 135
ありがとう : 133
ねえ : 100
さぁ : 91
う : 70
ああ : 61
はい : 34
さよなら : 32
ふふふ : 32
ごめん : 24
オー : 21
嗚呼 : 21
わーい : 20
おはよう : 19
ほんと : 19
あぁ : 19
えっ : 17
おやすみ : 14
おめでとう : 14
サヨナラ : 13
メリークリスマス : 13
アッ : 11
あれ : 11
ゴメン : 10
そら : 10
うん : 10
Kiss : 9
ようこそ : 8
```

感動詞は、その単語だけで独立して、かつ、あまり意味を持たなかったり、その単語だけで独立しているため前後の単語と関わりを持たない単語です。
全体的に解釈しずらい単語が並んでいます。
そのなかで、4番目の「ありがとう」という単語はストレートですが大きな意味を持つ単語です。
感謝を伝える曲は数多くありますが、約800曲の本当に様々な曲がある中で133回という具体的な数字を見ると、「ありがとう」という単語が大きさを実感できます。

### 係り受け解析

さて、次は出現頻度の多い単語に対して、係り受け解析を行った結果を見ていきましょう。
どの単語に対して解析を行うかは
「なんとなくこの単語を解析したら面白い結果が出そうだなぁ」
という完全に筆者の勘頼りで選択しました。

まず、「輝く」という単語に対して係り受け解析を行った結果、以下の通りになりました。
頻度上位30単語を示します。

```
思いっきり : 23
世界 : 15
キラキラ : 8
よう : 6
星 : 6
ため : 4
照らす : 4
私 : 4
なる : 4
歌 : 3
音 : 3
君 : 3
明日 : 3
もっと : 3
未来 : 3
日 : 3
瞳 : 3
見せる : 3
連なる : 3
夜 : 3
色 : 3
たち : 2
空 : 2
月 : 2
だって : 2
!) : 2
いつ : 2
moon : 2
大きい : 2
為 : 2
```

「思いっきり」「世界」「キラキラ」と、非常に ~~エモい~~ アイドルマスターらしい単語が並んでいます。
「思いっきり輝く」「輝く世界」「キラキラ輝く」と、ステージ上で輝くアイドルを連想できます。
8番目の「私」、13番目の「明日」、15番目の「未来」も、「輝く」という単語と繋がると希望に満ちたイメージを連想できる単語です。

次に、「信じる」の係り受け解析を行った結果の頻度上位30単語を示します。

```
! : 12
こと : 10
行く : 8
) : 7
力 : 7
自分 : 6
道 : 5
未来 : 4
瞬間 : 4
ある : 4
届く : 4
絆 : 4
ずっと : 3
ゆける : 3
叶える : 3
恋 : 3
向く : 3
奇跡 : 3
いつ : 3
僕 : 3
明日 : 3
さ : 3
追いかける : 2
大丈夫 : 2
心 : 2
育てる : 2
だから : 2
生まれ変わる : 2
? : 2
ココロ : 2
```

やはり、3番目「行く」、5番目「力」、6番目「自分」、8番目「未来」と、これも
**自分の力を、未来を信じて行く**
という非常に力強くポジティブなイメージを感じます。
また、12番目の「絆」という単語は「絆を信じる」というアイドルマスターにおける一つのキーワードを連想することができます。

最後に「ありがとう」についての係り受け解析結果です。

```
いつも : 4
あいす : 4
もらえる : 4
愛 : 3
大好き : 3
うれしい : 2
言える : 2
出会い : 2
舞台 : 2
時間 : 2
奇跡 : 2
本当に : 2
いる : 2
がんばる : 2
言う : 2
今日 : 2
背中 : 1
あなた : 1
ホッ : 1
気付く : 1
どうも : 1
日 : 1
ボク : 1
覚ます : 1
パパ : 1
繰り返す : 1
つぶやく : 1
心から : 1
交わす : 1
ん : 1
```

この結果に関しては言わずとも伝わると思うので、あえて言及を避けます。


## 最後に ～輝きの向こう側から見えたもの～

さて、ここまで様々な単語について歌詞中での出現頻度と、特定単語に対する係り受け解析を行ってきましたが、いかがでしたでしょうか？
自分としてはもっと深く、もっとたくさんの単語に関して注目して掘り下げていきたいのですが、誌面の都合上、非常に残念ですがここで区切りとさせていただきます。
ここまでお読みくださり、本当にありがとうございました。

アイドルマスターはもう10年を超えて続いているコンテンツです。
その長い積み重ねをすべて追い切ろうというのは非常に難しく、だんだんと現実的ではないというレベルにまでなりつつあると思います。
しかし、その一部だけでも縦断的かつ統計的に感じることができればと思い、このレポートを書くに至りました。

今回の試みからとても深く考えさせられる結果が沢山出てきましたが、自分が特に注目しているのは
**普段、曲を聴いているときに感じる感覚や感情を、明確に数値として示すことができた**
という点です。
人の心というのは数値では測れない面が多いです。
だからこそ「本当にそうなのか」という確証が持てません。
全てを数値化するのは野暮というものですが、我々プロデューサーが普段感じている「エモさ」「尊さ」を少しでも目に見える形として出すことができれば、それはまさに
**アイマスを科学する**と言えるのではないでしょうか。

今回用いたスクリプトは全てGitHub上に公開してあります。(\*4)
さらに詳細な内容について聞きたいという方は、Twitter@kiridarumaまたはwww2480www@gmail.comまでご連絡いただければ出来る範囲内でお手伝い致します。
これを機に、あなたも歌詞解析を通してアイマスを科学してみませんか？