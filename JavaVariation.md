# Java Variation #

### Doja to MIDP2.0 ###

|javax.microedition.midlet.Midlet|com.nttdocomo.ui.IApplication|
|:-------------------------------|:----------------------------|
|Choice                          |ListBox(ListBox.CHECK\_BOX | ListBox.MULTI\_SELECTION)|
|TextField                       |TextBox                      |
|TextField#set/getString         |TextBox#set/getText          |
|STAR                            |Display.KEY\_ASTERISK        |
|NUM#                            |Display.KEY_#_|
|searviceRepaint                 |                             |
|Alart                           |Dialog                       |
|Display.getDispaly(this).setCurrent|Display.setCurrent           |
|Timer                           |com.nttdocomo.util.Timer     |
|TimerTask                       |com.nttdocomo.util.TimerListener|
|Midlet#getGameAction            |Canvas#getKeypadState        |

## android ##

### Info ###

|Java|android|
|:---|:------|
|java.awt.Image|Bitmap |
|Graphics|Canvas |
|Graphics#drawImage|Canvas#drawBitmap|

  * MediaPlayer

|type|status|
|:---|:-----|
|.au |NG    |
|.wav|OK    |
|.mid|OK    |

### はまったところ ###

  * Rect は (x, y, w, h) じゃなくて (l, t, r, b)
  * キー入力のおまじない setFocusable(true);

### はじめてのあんどろいど ###

  * [LodeRunner (オリジナル右)](http://umjammer.googlecode.com/svn/trunk/x-lr/index.html)を移植してみた(左下)
  * ついでに iαppli にも移植してみた(左上)
    * DOJA は android に比べると J2SE に近いね

![](https://camo.githubusercontent.com/fbf1639a015277084756e3c4cc1fd0143fbe26e1/687474703a2f2f6c68352e67677068742e636f6d2f5f4a636855486645335746342f536e41466170334b4563492f41414141414141414147512f6654444e7a3555775f4c6f2f733238382f616e64726f69642e6c722e706e67)
