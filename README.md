# 4d-plugin-zint
Barcode generator based on [zint](https://zint.github.io).

* Exports SVG or PNG (compressed bitmap), as picture and text (XML source or base64 encoded data).

**Note:** The original PNG routine is only kept for the sake of completeness. The graphic quality is significantly better if 4D (``CONVERT PICTURE``, ``WRITE PICTURE FILE``) is used to convert SVG to PNG.

### Platform

| carbon | cocoa | win32 | win64 |
|:------:|:-----:|:---------:|:---------:|
||<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|<img src="https://cloud.githubusercontent.com/assets/1725068/22371562/1b091f0a-e4db-11e6-8458-8653954a7cce.png" width="24" height="24" />|

```
spctl -a -vv -t install ZINT.bundle: accepted
source=Notarized Developer ID
origin=Developer ID Application: keisuke miyako (Y69CWUC25B)
```

### Version

<img src="https://cloud.githubusercontent.com/assets/1725068/18940649/21945000-8645-11e6-86ed-4a0f800e5a73.png" width="32" height="32" /> <img src="https://cloud.githubusercontent.com/assets/1725068/18940648/2192ddba-8645-11e6-864d-6d5692d55717.png" width="32" height="32" /> <img src="https://user-images.githubusercontent.com/1725068/41266195-ddf767b2-6e30-11e8-9d6b-2adf6a9f57a5.png" width="32" height="32" />

![preemption xx](https://user-images.githubusercontent.com/1725068/41327179-4e839948-6efd-11e8-982b-a670d511e04f.png)

**Extended for 4D**

* "transparent background" option for both PNG and SVG.
* "rotate (90, 180, 270)" option for both PNG and SVG.
* "DPI" option for both PNG and SVG.
* optimised SVG (~~``cripsEdges`` shape rendering for bars,~~ ``sans-serif`` font).

---

## Syntax

```
barcode:=ZINT (in;format;type;keys;values;out)
```

Parameter|Type|Description
------------|------------|----
in|TEXT|
format|LONGINT|See constants ``ZINT Export Type``
type|LONGINT|See constants ``ZINT Barcode Type``
keys|ARRAY LONGINT|See constants ``ZINT Option Name``
values|ARRAY LONGINT|
out|TEXT|

## Examples

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

### Constants

* ZINT Barcode Type

```
BARCODE_CODE11 1
BARCODE_C25MATRIX 2
BARCODE_C25INTER 3
BARCODE_C25IATA 4
BARCODE_C25LOGIC 6
BARCODE_C25IND 7
BARCODE_CODE39 8
BARCODE_EXCODE39 9
BARCODE_EANX 13
BARCODE_EAN128 16
BARCODE_CODABAR 18
BARCODE_CODE128 20
BARCODE_DPLEIT 21
BARCODE_DPIDENT 22
BARCODE_CODE16K 23
BARCODE_CODE49 24
BARCODE_CODE93 25
BARCODE_FLAT 28
BARCODE_RSS14 29
BARCODE_RSS_LTD 30
BARCODE_RSS_EXP 31
BARCODE_TELEPEN 32
BARCODE_UPCA 34
BARCODE_UPCE 37
BARCODE_POSTNET 40
BARCODE_MSI_PLESSEY 47
BARCODE_FIM 49
BARCODE_LOGMARS 50
BARCODE_PHARMA 51
BARCODE_PZN 52
BARCODE_PHARMA_TWO 53
BARCODE_PDF417 55
BARCODE_PDF417TRUNC 56
BARCODE_MAXICODE 57
BARCODE_QRCODE 58
BARCODE_CODE128B 60
BARCODE_AUSPOST 63
BARCODE_AUSREPLY 66
BARCODE_AUSROUTE 67
BARCODE_AUSREDIRECT 68
BARCODE_ISBNX 69
BARCODE_RM4SCC 70
BARCODE_DATAMATRIX 71
BARCODE_EAN14 72
BARCODE_CODABLOCKF 74
BARCODE_NVE18 75
BARCODE_JAPANPOST 76
BARCODE_KOREAPOST 77
BARCODE_RSS14STACK 79
BARCODE_RSS14STACK_OMNI 80
BARCODE_RSS_EXPSTACK 81
BARCODE_PLANET 82
BARCODE_MICROPDF417 84
BARCODE_ONECODE 85
BARCODE_PLESSEY 86
BARCODE_TELEPEN_NUM 87
BARCODE_ITF14 89
BARCODE_KIX 90
BARCODE_AZTEC 92
BARCODE_DAFT 93
BARCODE_MICROQR 97
BARCODE_HIBC_128 98
BARCODE_HIBC_39 99
BARCODE_HIBC_DM 102
BARCODE_HIBC_QR 104
BARCODE_HIBC_PDF 106
BARCODE_HIBC_MICPDF 108
BARCODE_HIBC_BLOCKF 110
BARCODE_HIBC_AZTEC 112
BARCODE_AZRUNE 128
BARCODE_CODE32 129
BARCODE_EANX_CC 130
BARCODE_EAN128_CC 131
BARCODE_RSS14_CC 132
BARCODE_RSS_LTD_CC 133
BARCODE_RSS_EXP_CC 134
BARCODE_UPCA_CC 135
BARCODE_UPCE_CC 136
BARCODE_RSS14STACK_CC 137
BARCODE_RSS14_OMNI_CC 138
BARCODE_RSS_EXPSTACK_CC 139
BARCODE_CHANNEL 140
BARCODE_CODEONE 141
BARCODE_GRIDMATRIX 142
```

* ZINT Export Type

```
ZINT_Format_SVG 1
ZINT_Format_PNG 2
```

* ZINT Option Name

```
ZINT_HEIGHT 1
ZINT_WHITE_SPACE 2
ZINT_BORDER 3
ZINT_BOX 4
ZINT_BIND 5
ZINT_SCALE 9
ZINT_ROTATE 10
ZINT_COLUMNS 11
ZINT_VERSION 12
ZINT_SECURE 13
ZINT_PRIMARY 14
ZINT_MODE 15
ZINT_GS1 16
ZINT_NO_TEXT 17
ZINT_SQUARE 18
ZINT_KANJI 19
ZINT_SJIS 20
ZINT_SMALL_TEXT 21
ZINT_DPI 22
ZINT_NO_BACKGROUND 23
```

![](https://cloud.githubusercontent.com/assets/1725068/14666616/9294b6a0-0715-11e6-9323-6b1934e37b38.png)

