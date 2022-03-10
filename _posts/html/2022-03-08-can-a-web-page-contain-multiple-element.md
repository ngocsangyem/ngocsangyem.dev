---
layout: post
title: "Can a web page contain multiple header elements? What about footer elements?"
description: >
  W3 recommends having as many as you want, but only 1 of each for each "section" of your page, i.e. body, section etc.
image: 
  path: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_1400.jpg
  srcset:
    1400w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_1400.jpg
    1290w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_1290.jpg
    1104w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_1104.jpg
    905w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_905.jpg
    570w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_570.jpg
    406w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_406.jpg
    200w: /assets/img/blog/html/can-a-web-page-contain-multiple-header-elements-what-about-footer-elements_w_200.jpg
sitemap: true
category: html
tags:
- html
---

* this ordered seed list will be replaced by the toc
{:toc}

### Answer

Yes to both. The W3 documents state that the tags represent the header(<header>) and footer(<footer>) areas of their nearest ancestor "section". So not only can the page <body> contain a header and a footer, but so can every <article> and <section> element.

W3 recommends having as many as you want, but only 1 of each for each "section" of your page, i.e. body, section etc.

### Additional links

* [StackOverflow - Using header or footer tag twice](https://stackoverflow.com/questions/4837269/html5-using-header-or-footer-tag-twice)