---
layout: post
title: "Can a web page contain multiple header elements? What about footer elements?"
description: >
  W3 specification allows multiple header and footer elements in HTML5. Learn when and how to use them correctly.
image: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_1400.jpg
sitemap: true
category: html
tags:
  - html
  - w3c
  - semantics
---

* this ordered seed list will be replaced by the toc
{:toc}

## Answer

Yes to both. The W3 documents state that the tags represent the header(<header>) and footer(<footer>) areas of their nearest ancestor "section". So not only can the page <body> contain a header and a footer, but so can every <article> and <section> element.

W3 recommends having as many as you want, but only 1 of each for each "section" of your page, i.e. body, section etc.

## Additional links

* [StackOverflow - Using header or footer tag twice](https://stackoverflow.com/questions/4837269/html5-using-header-or-footer-tag-twice)