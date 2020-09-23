currently sdl1 doesn't work on macos

# PC

## PC-8801

### quasi88

* https://github.com/barbeque/quasi88-port (40c033b)

### j80 (r6_117)

```
 $ java -jar j80.jar j88.cfg
```
| **j80** | **quasi88** | **m88** |
|:--------|:------------|:--------|
|        R\_80    |N88N.ROM     |N80.ROM    |
|        USR0    |N88N.ROM     |N80.ROM    |
|        R\_88    |N88.ROM      |N88.ROM  |
|        R4E0    |N88EXT0.ROM  |N88\_0.ROM  |
|        R4E1    |N88EXT1.ROM  |N88\_1.ROM  |
|        R4E2    |N88EXT2.ROM  |N88\_2.ROM  |
|        R4E3    |N88EXT3.ROM  |N88\_3.ROM  |
|        FONT    |N88KNJ1.ROM  |KANJI1.ROM |
|        JIS1    |N88KNJ1.ROM  |KANJI1.ROM |
|        JIS2    |N88KNJ2.ROM  |KANJI2.ROM |
|        DISK    |N88SUB.ROM   |DISK.ROM   |

`j88.cfg`
```
	FONT	.../FONT.ROM
//	FONT	.../FONT.ROM		0x1000	// ★	漢字ROMを流用する場合

// use line at last
-D88    disk/Foo.D88       1

```

## PC-9801

### NP2 for OSX

  * ~~HID Utilities 必要~~
  * ~~コンパイルはできたが動かん...orz~~
  * used mac api become obsolated
  * -> NP2Kai

### xnp2

  * ~~素直にこちらを使う~~
  * ~~サウンドとかも OK~~
  * x11 doesn't work on macos
  * sdl1 doesn't work on macos
  * -> NP2kai

### T98next w/ wine

  * ~~サウンドが鳴らない？~~
    * ~~wine のバージョンが悪かったみたい~~
    * now wine64 needs 64bit windows code

### np2 variants

 * https://github.com/AZO234/NP2kai 👑
 * https://github.com/rururutan/np2s (sound library updated)
 
### NP2Kai
 
 * https://github.com/AZO234/NP2kai c38a5b2
 * patch https://gist.github.com/umjammer/c7e8b4ea5a59a40f61b5b8133e27aaa3
 
 ```
 $ uname -a
 Darwin xxxxxxxx 19.6.0 Darwin Kernel Version 19.6.0: Thu Jun 18 20:49:00 PDT 2020; root:xnu-6153.141.1~1/RELEASE_X86_64 x86_64 i386 iMac17,1 Darwin
 $ brew install openssl sdl2 sdl2_ttf sdl2_mixer
 $ git clone ...
 $ cd NP2kai
 $ patch ...
 $ mkdir build
 $ cd build
 $ cmake -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl ..
 $ make
 ```
 
