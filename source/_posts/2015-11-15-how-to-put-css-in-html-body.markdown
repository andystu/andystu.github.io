---
layout: post
title: "how to put css in html body?"
date: 2015-11-15 23:49:47 +0800
comments: true
categories: css, html5, style, javascript, jquery
---
- There are two ways to set css file into our html documents.
- first way: using pure javascript to append css file into head part of html.

``` html
<script type="text/javascript">

   function loadCSS(filename){

      var file = document.createElement("link")
      file.setAttribute("rel", "stylesheet")
      file.setAttribute("type", "text/css")
      file.setAttribute("href", filename)

      if (typeof file !== "undefined")
         document.getElementsByTagName("head")[0].appendChild(file)
   }


  //just call a function to load a new CSS:
  loadCSS("path_to_css/file.css")

</script>
```

<!--more-->

- Or we can simply use jquery.

``` html
$('head').append('<link rel="stylesheet" type="text/css" href="{yoururl}">');
```

- Fashion way is to use style tag in body. (notice: some old browsers would not support this.)

``` html
<!DOCTYPE html>
<html>
<head></head>
<body>

<div id = "scoped-content">
    <style type = "text/css" scoped>
    h1 { color: red; }
    </style>

    <h1>Hello</h1>
</div>

<h1>World</h1>

</body>
</html>
```

references:
- http://stackoverflow.com/questions/11833325/css-hack-adding-css-in-the-body-of-a-website
- http://stackoverflow.com/questions/2830296/using-style-tags-in-the-body-with-other-html
- http://html5doctor.com/the-scoped-attribute/
