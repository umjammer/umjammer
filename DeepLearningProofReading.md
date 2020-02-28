# ディープラーニングで校正

と言っても Web の API 使うんだけどね。
Recruit の [a3rt](https://a3rt.recruit-tech.co.jp/product/proofreadingAPI/) の Proofreading API です。

## いままで

 1. キャプチャ
 2. Google Docs OCR ほんの基本的な校正も行える (赤の波線がつく)
     * ドキュメントからプレーンテキストを取り出す[スクリプト](https://gist.github.com/umjammer/30b1977bfaa0c36241261016052669ae#file-docxview-sh)
 3. 手動校正
     * "「"がダメだったような気が
     * カタカナの"ニ"と数字の"二"とか
     * "パ"と"バ"とか
 4. Web サービス [たぶんこれ](http://enno.jp/)使ったはず（覚えていないw）
     * "洒落"を見つけてくれた (酒になってた)
 5. 何回も間を空けて読み返す
     * たまに見つかる
 5. a3rt を試してみたがダメだった...
     * https://twitter.com/umjammer/status/972039212236095490

(3.) と (5.) がやっぱり大変なんだよね。
(3.) は気が狂いそうだし、 (5.) は何回読んでも出てくるし...
(2.) は当時 Google のくせに全然ダメだった。今はどうなんだろう？
(4.) は機械学習系じゃないのが多いからやっぱり限界があるし。
 
## 使えるようになった？ 2019-05-15

久しぶりに起動してみたら指摘してくれた。 Twitter で呟いたから学習させた？
それとも一年以上の学習の結果なのか？

```json
{
   "normalizedSentence" : "薄茶色のシミがあちこちについた掛け布団。座ったら、五分でお尻が序くなってきそうだ。",
   "message" : "pointed out",
   "checkedSentence" : "薄茶色のシミがあちこちについた掛け布団。座ったら、五分でお尻が <<序>> くなってきそうだ。",
   "status" : 1,
   "resultID" : "1e908391e3bd",
   "alerts" : [
      {
         "pos" : 31,
         "suggestions" : [
            "な",
            "き",
            "し"
         ],
         "word" : "序",
         "score" : 0.809495427479827
      }
   ],
   "inputSentence" : "薄茶色のシミがあちこちについた掛け布団。座ったら、五分でお尻が序くなってきそうだ。"
}
```

サジェスチョンは適当だがそこは別に手動でいいのだ。修正箇所は少ないんだからそこは人力で OK。
広大な文字の海から変なのを見つける作業が大変なのであって、そこを AI に任せたいのだ。

さて全行やってみるか。制限かかりませんように...

https://github.com/umjammer/vavi-util-screenscraping/blob/master/src/test/java/RecruitProofreadingV2.java

## 結果 2019-05-15

うーん... 今度は要らん指摘しすぎだ。 1317/5245 行に指摘が入った。1000 件とか確認無理なんですけど。
まぁぱっと見新たに3件見つけたんで一応役には立つな。それも1行目からw
もう少し頑張って指摘減らしてくれ。

```
本作品の全部または一部を無断で複製、転載、 <<改>>  <<賞>> 、公衆送信すること
```

改竄ですね

## 追記 2019-05-16

1000 件確認してみた。
あってても指摘入ってるやんけ！まったく...

```
薄茶色のシミがあちこちについた掛け布団。座ったら、五分でお尻が <<痒>> くなってきそうだ。
```

指摘し過ぎを減らしてハイライト

```regex
<<[^\W^\p{Hiragana}^\p{Katakana}^〇^一^二^三^四^五^六^七^八^九^十]+>>
```

昨日の分を含めて、更に 10 件見つけた。固有名詞をもっと頑張って学習して省いてくれればすごい有用なツールになりそう。

## 追記 2020-02-29

[Sudachi](https://github.com/WorksApplications/Sudachi) を調べていたら oov という単語が出てきた。 out of vocabulary の略だそうだ。
これってまさに校正対象のことじゃないの？と思って試してみた。

青空文庫表記のタグやルビが鬱陶しいので先に除いておいて、漢字のみの oov を表示させてやる。

[Program](TBD)

### 結果

めっちゃうまくいく!!!

![image](https://lh3.googleusercontent.com/BWtEQrYSyjIpdw6iRyXR3FD7803bZwGPLxiNsJ_bx3IJeQr8lDSfJKzIappdKvq2Az4hkqHgQattDhsoZqQpsP3MLXN5rX3BByq6H2aMW3mmOMFPwEWx4Z49DZjMW_3l8tDcbm43Hw=w2400)

ものすごい精度だ。完璧なんじゃなかろうか？ディープラーニングいらんやんｗ
