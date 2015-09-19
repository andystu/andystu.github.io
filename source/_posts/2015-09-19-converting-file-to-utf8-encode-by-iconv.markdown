---
layout: post
title: "Converting file to utf8 encode by iconv"
date: 2015-09-19 22:47:20 +0800
comments: true
categories:
---
- Sometimes, we need to convert file from different encode to utf8 before we may open and edit it. **iconv** command make it easy.
```
# convert input_file from big5 encode to utf8 encode
$ iconv -f BIG5 -t UTF8 input_file > output_file
```
- done.
