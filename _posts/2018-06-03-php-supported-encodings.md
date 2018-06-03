---
layout: post
title: "PHP supported encodings"
date: "2018-06-03 18:00:00 -0300"
author: "Lemuel Roberto"
meta: "php"
---

**Ordered list of all supported encondings in PHP:**

* 7bit
* 8bit
* ASCII
* ArmSCII-8
* BASE64
* BIG-5
* CP50220
* CP50220raw
* CP50221
* CP50222
* CP51932
* CP850
* CP866
* CP932
* CP936
* CP950
* EUC-CN
* EUC-JP
* EUC-JP-2004
* EUC-KR
* EUC-TW
* GB18030
* HTML-ENTITIES
* HZ
* ISO-2022-JP
* ISO-2022-JP-2004
* ISO-2022-JP-MOBILE#KDDI
* ISO-2022-JP-MS
* ISO-2022-KR
* ISO-8859-1
* ISO-8859-10
* ISO-8859-13
* ISO-8859-14
* ISO-8859-15
* ISO-8859-16
* ISO-8859-2
* ISO-8859-3
* ISO-8859-4
* ISO-8859-5
* ISO-8859-6
* ISO-8859-7
* ISO-8859-8
* ISO-8859-9
* JIS
* JIS-ms
* KOI8-R
* KOI8-U
* Quoted-Printable
* SJIS
* SJIS-2004
* SJIS-Mobile#DOCOMO
* SJIS-Mobile#KDDI
* SJIS-Mobile#SOFTBANK
* SJIS-mac
* SJIS-win
* UCS-2
* UCS-2BE
* UCS-2LE
* UCS-4
* UCS-4BE
* UCS-4LE
* UHC
* UTF-16
* UTF-16BE
* UTF-16LE
* UTF-32
* UTF-32BE
* UTF-32LE
* UTF-7
* UTF-8
* UTF-8-Mobile#DOCOMO
* UTF-8-Mobile#KDDI-A
* UTF-8-Mobile#KDDI-B
* UTF-8-Mobile#SOFTBANK
* UTF7-IMAP
* UUENCODE
* Windows-1251
* Windows-1252
* Windows-1254
* auto
* byte2be
* byte2le
* byte4be
* byte4le
* eucJP-win
* pass
* wchar

You can view this list on your own environment running this:

```php
<?php

$encodings = mb_list_encodings();
asort($encodings);
print_r(array_values($encodings));
```
