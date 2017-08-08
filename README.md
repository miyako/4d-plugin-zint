# 4d-plugin-zint
Barcode generator

### Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|

### Version

<img src="https://cloud.githubusercontent.com/assets/1725068/18940649/21945000-8645-11e6-86ed-4a0f800e5a73.png" width="32" height="32" /> <img src="https://cloud.githubusercontent.com/assets/1725068/18940648/2192ddba-8645-11e6-864d-6d5692d55717.png" width="32" height="32" />


![](https://cloud.githubusercontent.com/assets/1725068/14666616/9294b6a0-0715-11e6-9323-6b1934e37b38.png)

About
---
Barcode generator based on [zint](https://github.com/zint).

* Exports SVG or PNG (compressed bitmap), as picture and text (XML source or base64 encoded data).

**Extended for 4D**

* "transparent background" option for both PNG and SVG.
* "rotate (90, 180, 270)" option for both PNG and SVG.
* "DPI" option for both PNG and SVG.
* optimised SVG (~~``cripsEdges`` shape rendering for bars,~~ ``sans-serif`` font).

Commands
---
```c
ZINT
```

Examples
---
```
ARRAY LONGINT($optionNames;0)
ARRAY TEXT($optionValues;0)

APPEND TO ARRAY($optionNames;ZINT_SMALL_TEXT)
APPEND TO ARRAY($optionValues;"0")

APPEND TO ARRAY($optionNames;ZINT_BOX)
APPEND TO ARRAY($optionValues;"0")

APPEND TO ARRAY($optionNames;ZINT_BORDER)
APPEND TO ARRAY($optionValues;"0")

APPEND TO ARRAY($optionNames;ZINT_DPI) 
APPEND TO ARRAY($optionValues;"96")

APPEND TO ARRAY($optionNames;ZINT_ROTATE)  
APPEND TO ARRAY($optionValues;"0")  //90, 180, 270

APPEND TO ARRAY($optionNames;ZINT_NO_BACKGROUND)
APPEND TO ARRAY($optionValues;"1")

$bar:=ZINT ("abcde";ZINT_Format_SVG;BARCODE_CODE39;$optionNames;$optionValues;$textData)
$bar:=ZINT ("abcde";ZINT_Format_SVG;BARCODE_CODE93;$optionNames;$optionValues;$textData)
$bar:=ZINT ("abcde";ZINT_Format_SVG;BARCODE_EXCODE39;$optionNames;$optionValues;$textData)
$bar:=ZINT ("http://www.4d.com/";ZINT_Format_SVG;BARCODE_QRCODE;$optionNames;$optionValues;$textData)
$bar:=ZINT ("http://www.4d.com/";ZINT_Format_SVG;BARCODE_AZTEC;$optionNames;$optionValues;$textData)
$bar:=ZINT ("http://www.4d.com/";ZINT_Format_SVG;BARCODE_CODE128;$optionNames;$optionValues;$textData)
$bar:=ZINT ("http://www.4d.com/";ZINT_Format_PNG;BARCODE_QRCODE;$optionNames;$optionValues;$textData)
$bar:=ZINT ("Wikipedia, the free encyclopedia";ZINT_Format_PNG;BARCODE_MAXICODE;$optionNames;$optionValues;$textData)
$bar:=ZINT ("164626565111";ZINT_Format_PNG;BARCODE_EANX;$optionNames;$optionValues;$textData)
$bar:=ZINT ("Wikipedia, the free encyclopedia";ZINT_Format_SVG;BARCODE_MAXICODE;$optionNames;$optionValues;$textData)

SET TEXT TO PASTEBOARD($textData)
  //WRITE PICTURE FILE(System folder(Desktop)+"test.svg";$bar)
  //SET PICTURE TO PASTEBOARD($bar)
```
