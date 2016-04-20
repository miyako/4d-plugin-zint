# 4d-plugin-zint
Barcode generator

##Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
|🆗|🆗|🆗|🆗|

About
---
Barcode generator based on [zint](https://github.com/zint).

* Exports SVG or PNG (compressed bitmap), as picture and text (XML source or base64 encoded data).

**Extended for 4D**

* "transparent background" option for both PNG and SVG.
* "rotate (90, 180, 270)" option for both PNG and SVG.
* "DPI" option for both PNG and SVG.
* optimised SVG (``cripsEdges`` shape rendering for bars, ``sans-serif`` font).

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
