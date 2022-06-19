---
layout: post
title: "setup-script is the cool feature of vue but..."
category: devlog
description: script setup is the cool feature that Vue team introduced. But in some cases, normal script is the better choice.
tags: vue
image:
  path: assets/img/blog/vue/jun_2022/vue_cover.webp
---

* this ordered seed list will be replaced by the toc
{:toc}

`<script setup>` block is compiled into the `setup()` function for the component.

### Why?

##### Use the options API

Not everything has an equivalent in the composition API, like `inheritAttrs`.

##### Run setup code one time

Because `setup()` is run for *every* component, if you have code that should only be executed once you can't include it in `<script setup>`.

You can put it inside of the regular `<script>` block though.

##### Named exports

Sometimes it's nice to be able to export multiple things from one file, but you can only do that with the regular `<script>` block.

### Additional links

* [Vue SFC](https://vuejs.org/api/sfc-script-setup.html#script-setup)
* [@MichaelThiessen](https://twitter.com/MichaelThiessen)
