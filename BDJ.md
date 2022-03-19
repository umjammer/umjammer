# BD-J #

System Software Update v2.50 以降 AVCHD がディスク以外から？再生されなくなりました。よって終了〜

  * [MP3 再生のソース](https://github.com/umjammer/vavi-sound-bdj)まで書いたのに...

## PS3 ##

  * ADA
    * 1016832 bytes
## Info ##

### javax.tv ###

  * codec

|type|codec|
|:---|:----|
|audio|ima4, |
|video|cinepak|

  * content

|type|codec|
|:---|:----|
|video|quicktime|

  * protocol

|type|
|:---|
|file|
|http|

## Develop ##

  * [hdcookbook](https://hdcookbook.dev.java.net/)
  * bdj-ps3
  * [xletview](http://xletview.sourceforge.net/)

  * off screen image は Component#createImage を使う
    * new BufferedImage() はダメっぽい
  * Conponent#getToolkit() が NoSuchMethodError
    * xletview ~~だけ？？？~~ → xletview のバグ
  * GZipInputStream でエラーが起きる
    * on PS3
  * String のメソッドのバージョン
    * replace → 自作
    * split → StringTalknizer

  * お約束の LodeRunner

![loderunner](https://lh3.googleusercontent.com/pw/AM-JKLVKI-b4pdQpmiWKGBRW7OSpV7E015pAWJVl1knAoygWs3leXJ1ZPZrKlMH-TYzSRjVtNj6m6tZ66Bc9qCkcFYYaUTfPmsyQ8lhC2WxWU4kD5uOQQzUcGlXs3FPRO1KZHLss7VapoxtUBvhEyBMPiWZ-=w692-h418-no?authuser=0)

  * [Apple II Emulator](https://github.com/umjammer/vavi-apps-appleii-bdj) - [My Blog](http://vavivavi.blogspot.com/2008/09/bd-j-appleii-emulator-bd-j-nes-apple-ii.html) [PS3 NEWS](http://www.ps3news.com/forums/playstation-3-news/playstation-3-bd-j-apple-ii-emulator-released-100986.html)
  * [2ch Browser](https://github.com/umjammer/vavi-apps-mona-bdj) - [My Blog](http://vavivavi.blogspot.com/2008/09/blog-ps3-homebrew-bd-j-2ch-ps3-bd-j-2ch.html)
  * [Tetris](https://github.com/umjammer/vavi-games-tetris-bdj)
  * [PuyoPuyo](https://github.com/umjammer/vavi-games-puyo-bdj)

### xletview ###

  * bugs
    * RandomAccessFile
    * constructor(File,String) not such method
    * user.dir not set like FileInputStream
    * javassist によって xjava.`*` に置換されるクラスのうち自クラスの型もしくは配列を返すメソッドがダメになる
      * File#listFiles() x3
      * Toolkit#getToolkit()

  * differences
    * ColorModel
      * PS3 ではαが効いてる
      * xletview はαなくても OK な場合がある -> BufferedImage#getRGB/setRGB

## Idea ##

  * Virtual Keyboard
    * via network
    * PBP has ServerSocket
    * http://synergy2.sourceforge.net/
