# なんちゃってMVC #

## 概要 ##
### 何？ ###

既存の GUIプログラムを簡単に MVC を適用した構造に書き換える方法

### どこで使うの？ ###

iPhone, android, Kibdle, iPad と次々に発表される新しいプラットフォームに 既存のプログラムを載せたい場合。


## やり方 ##

以下の Applet を題材にします。大昔どこからか拾ってきたものです。

 https://github.com/umjammer/vavi-games-tetris/blob/7194d67aa62d5d6a5c2c67f5a066afb4391d58be/tetris.java

典型的な Applet で一つのファイルになっています。もちろん MVC のカケラもありません。
悪いと言っているのではないですよ。 Applet を作るといえば皆昔はこうしていたんですから。

 ![http://farm3.static.flickr.com/2685/4424024043_48361b691c.jpg](http://farm3.static.flickr.com/2685/4424024043_48361b691c.jpg)

### 1. 固有のプラットフォームを抜く ###

Java 固有の Applet というプラットフォームを抜きます。今回は 3. で行う Controller
もついでに抜いちゃいました。
```
 init(), start(), stop(), destroy(), KeyLitener
```
 https://github.com/umjammer/vavi-games-tetris/commit/4d694246b7c67b6d6bdb67c2c381705d574f71d7?diff=split#diff-f435b399ce7f286aeee6805954eeadc9&diff=split

抜いた Applet は現在こんな感じです。

 https://github.com/umjammer/vavi-games-tetris/blob/4d694246b7c67b6d6bdb67c2c381705d574f71d7/TetrisApp.java

### 2. View を外出しする ###

グラフィック等に関する部分を View というインターフェースで抽象化して外出しします。

今回は
```
repaint(), drawImage(), loopClip(), stopClip() 
```
ですべて外出しすることができます。

 https://github.com/umjammer/vavi-games-tetris/commit/6035a22fb5ee2784e269f2bd5f6111a3f74a7ab7?diff=split#diff-f435b399ce7f286aeee6805954eeadc9&diff=split

外出しした View は Applet 側で実装してやります。

 https://github.com/umjammer/vavi-games-tetris/commit/6035a22fb5ee2784e269f2bd5f6111a3f74a7ab7#diff-9db71d3bd9fbcdb5f207e5f78f9912c4&diff=split

### 3. Controller を外出しする ###

キー操作等に関する部分を Controller というインターフェースで抽象化して外出しします。

今回はそこまですることはないと判断したのでモデルクラスに操作メソッドを追加するにとどめています。
```
 up(), down(), left(), right(), rotate()
```

 https://github.com/umjammer/vavi-games-tetris/commit/fd622e0268b8cce798c0238b18a9044a1e89f0ef#diff-f435b399ce7f286aeee6805954eeadc9&diff=split

この時点で Tetris クラスには import 文がなくなりました。完全なモデルクラスになったわけです。(Thread とか細かいことは言わないw)

### 4. 仕上げ ###

バグを潰して、綺麗にしたら完成です。

モデル

 https://github.com/umjammer/vavi-games-tetris/blob/d748b8a9ba58f5bd53f58da3c9145a66f35e8b42/Tetris.java

Applet

 https://github.com/umjammer/vavi-games-tetris/blob/d748b8a9ba58f5bd53f58da3c9145a66f35e8b42/TetrisApp.java

## ここからどうするの？ ##

Applet を眺めてるとこいつを Kindlet や Midlet, Xlet に置き換えるだけで Tetris じゃんじゃん
移植できると思いません？

### ほれ ###

  * [Android Tetris](https://github.com/umjammer/vavi-games-tetris-android)
  * [Xlet Tetris (BD-J)](https://github.com/umjammer/vavi-games-tetris-bdj)
  * [C# Tetris](https://github.com/umjammer/vavi-games-tetris-winforms)
  * [Kindlet Tetris (KDK)](https://github.com/umjammer/vavi-games-tetris-kdk)

C# ですら楽勝！

<a href='http://www.flickr.com/photos/52807817@N00/4457210112/' title='Android Tetris by umjammer, on Flickr'><img src='http://farm3.static.flickr.com/2708/4457210112_3945fb30d5.jpg' alt='Android Tetris' width='298' height='500' /></a>

![http://farm3.static.flickr.com/2738/4424213858_c7e912be2e.jpg](http://farm3.static.flickr.com/2738/4424213858_c7e912be2e.jpg)

![http://farm3.static.flickr.com/2717/4424213856_aa5e932dd8.jpg](http://farm3.static.flickr.com/2717/4424213856_aa5e932dd8.jpg)

<a href='http://www.flickr.com/photos/52807817@N00/4458856225/' title='Kindle Tetris by umjammer, on Flickr'><img src='http://farm5.static.flickr.com/4025/4458856225_46f0b87fc4.jpg' alt='Kindle Tetris' width='444' height='500' /></a>
