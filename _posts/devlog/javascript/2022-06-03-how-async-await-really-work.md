---
layout: post
title: "How async/await really work"
description: >
  "An async function is a function declared with the async keyword, and the await keyword is permitted within it. The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains." - MDN
img: assets/img/blog/javascript/jun_2022/async_dog.webp
sitemap: true
category: devlog
tags:
- javascript
---

* this ordered seed list will be replaced by the toc
{:toc}

### Explanation

To simplify how async/await work, we'll use the `fetch` function from the `window` object.

```javascript
const getTodo = async () => {
  console.log('Log me first');
  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
  const todo = await response.json();
  console.log(todo);
};

getTodo();

console.log('Log me second');
```

Let's explain what's happening here.

* In line 1, we declare a function called `getTodo` that returns a promise.
* Next, we invoke the `getTodo` and immediately create a new execution context. At this time, assume in 1ms, we are going to get the message `Log me first`.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step1.webp alt: 'async/await'%}

* In next line, we define a variable called `response`. For now, it is `undefined`.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step2.webp alt: 'async/await'%}

`response` is going to be the evaluated result of the `fetch` function on the right-hand side. So it will get a Promise object. In this object, we have two important properties: `onFullfilled` and `value`. The `value` is gonna be auto-filled in with whatever comes back from the `web browser`. The `onFullfilled` is an array of functions, this array will be filled when we use the `then` method of Promise. We hold this object just for now.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step3.webp alt: 'async/await'%}

In this time, let's look at the web browser. We see we are spinning up the background feature [XHR] request by running the `fetch` function with an URL.

[XHR] requests have done many things, one of them is to send a request to the server. It sends an HTTP message to the server. At 1ms, in the complete phase, it not complete yet.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step4.webp alt: 'async/await'%}

On completion, we want to update the `value` property.

> Take a note: we have not assigned the Promise object to any particular place. It's just a position in memory.

So the `value` here is the `value` of the Promise object.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step5.webp alt: 'async/await'%}

And now the powerful `await` keyword is going to throw us out of the `getTodo` execution context. Where we are going to encounter the next line of code.

* At the next line, we declare a variable called `todo`. And at this time it is also undefined. We run the right-hand side and we met the `await` keyword. This also throws us out of the `getTodo` execution context to run the next line - console.log('Log me second').

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step6.webp alt: 'async/await'%}

The important we want to do is set up an asynchronous task that takes a bunch of time to complete - That is a web browser feature task, for example, to speak to the internet and take about 1s to complete but we want able to continue running our synchronous code afterward. You can see to do it, we are stepping out of our function.

But it would be wonderful if we could step back into our function when we get the value from the request back as a response. Hopefully, it's gonna be stored in the `response` variable. And we can continue running our code and log that data.

After log `'Log me second`, we don't have much stuff to do. But assume after 200ms, we get the value back from the request. That going to update the value property of the promise object that is being stored in memory and referred to its position.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step7.webp alt: 'async/await'%}

At this point, we are going to trigger at that moment the continuation of our `getTodo` function. make the `getTodo` back on the call stack and come back in.

The `await` keyword was super powerful, it threw us straight out of the execution context that we never got to assign anything to the data. But it's not a bad thing, we are hoping that data is going to be filled in with whatever the right-hand side evaluates to. And the value we get here is the response from the server.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step8.webp alt: 'async/await'%}

And we assign this value to the `response` variable.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step9.webp alt: 'async/await'%}

After that, the `todo` variable also gets the evaluated value of the `response` variable.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step10.webp alt: 'async/await'%}

So that we can hit our next line - `console.log(todo)`.

{% responsive_image path: assets/img/blog/javascript/jun_2022/async_step11.webp alt: 'async/await'%}

### Summary

All works return a value or the response object into the promise object we stored in future data. Then we use the `then` method to trigger the callback function to receive the data. All of that is automated. The `async` function will handle that for us. The `await` still behaves similar to a `yield` keyword.

### Additional links

* [JavaScript the Hard Parts: Asynchronous JavaScript]
* [Difference between async/await and ES6 yield with generators]

[XHR]: https://en.wikipedia.org/wiki/XMLHttpRequest
[JavaScript the Hard Parts: Asynchronous JavaScript]: https://www.youtube.com/watch?v=xTjx3q2Nm1w
[Difference between async/await and ES6 yield with generators]: https://stackoverflow.com/questions/36196608/difference-between-async-await-and-es6-yield-with-generators