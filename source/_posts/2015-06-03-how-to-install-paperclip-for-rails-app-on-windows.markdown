---
layout: post
title: "how to install paperclip for rails app on windows"
date: 2015-06-03 22:34:43 +0800
comments: true
categories: rails, paperclip, windows
---

- If we want to run rails app with paperclip in windows environment, we need to install two package for it.

1. GnuWin32 - http://gnuwin32.sourceforge.net/packages/file.htm
2. ImageMagick binary-  http://www.imagemagick.org/download/binaries/

- Next, we should install the correct static version for your OS (32-bit vs 64-bit) (not dll version)

- Finnally, we need to add the bin directory to your environment path (in config/environment/development.rb or production.rb) as following lines:

``` ruby
...
Paperclip.options[:command_path] = 'C:\Program Files (x86)\GnuWin32\bin; C:\Program Files\ImageMagick-6.7.6-3-Q16' 
Paperclip.options[:swallow_stderr] = false
...
```