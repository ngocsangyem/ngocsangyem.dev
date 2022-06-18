---
layout: post
title: "Object dot notation"
description: >
  "Property accessors provide access to an object's properties by using the dot notation or the bracket notation." - MDN
image:
  path: assets/img/blog/javascript/object-dot-notation_w_1280.webp
sitemap: true
category: devlog
tags:
- javascript
---

* this ordered seed list will be replaced by the toc
{:toc}

### What is object dot notation?

Let's say we have an application storing each user's name and score in a single objec`t. An the functionality we need to have for each user just the ability to increase their score by one.

```javascript
const user1 = {
  name: 'John',
  score: 0,
};
```

In our ideal world, wherever user is in the application, we would be able to access their score and increase it by one. So how we could bundle up in one package in one kind of organizing data structures? That data with the functionality so we know that they're right there next to each other. And we can even use a special "dot". That "dot" is a special character that we can use the functionality on that data. So how can we bundle functionality and data in one place? That's where `Object dot notation` comes in.

```javascript
const user1 = {
  name: 'John',
  score: 0,
  increment: function() {
    user1.score++;
  },
};

user1.increment(); // user1.score = 1
```

### Additional links

[Property accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors)