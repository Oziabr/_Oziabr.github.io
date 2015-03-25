---
layout: wirings4book
title: Book Converter
permalink: /bc/
published: true
---

## converter is here

<textarea></textarea>

## here is the code

  /**/
  result = ''
  xml = $('textarea').val()
       .replace(/<empty-line\//g, '<hr/')
  data = $(xml)
  
  // cleaning
  while ($('style', data).length) {
    $('style', data).each(function(n) { $(this).replaceWith($(this).html()) })
  }
  $('a', data).each(function(n) { $(this).replaceWith($(this).html()) })
  $('title', data).each(function(n) { 
    $(this).text(
      $(this).text()
        .replace(/^<p>|<\/p>$/g, '')
        .replace(/<\/p><p>/g, '|')
      + "\n"
    ) 
  })
  
  
  // inline formatting
  $('section p emphasis', data).each(function(n) {
    $(this).replaceWith('*'+$(this).html()+'*') 
  })
  
  // test
  // $('section p', data).each(function(n) { if ($(this).html() !== $(this).text()) console.log(n, $(this).html()) })
  
  // block formatting
  $('title', data).each(function(n) { 
    $(this).text('# '+$(this).text())
  })
  $('section title', data).each(function(n) { 
    $(this).text('#'+$(this).text())
  })
  $('section p', data).each(function(n) { 
    $(this).replaceWith($(this).text()+"\n\n")
  })
  $('section hr', data).each(function(n) { 
    $(this).replaceWith($(this).text()+"---\n")
  })
  
  // composing
  $('>title, >section', data).each(function(n) { 
    result += $(this).text()
  })
  
  console.clear()
  result
  
  
