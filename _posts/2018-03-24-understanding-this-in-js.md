---
layout: post
title: Understanding this in JS
---

- function 中的 `this` 是运行的环境决定，这个  function 被谁调用, this 指向谁。
- `() => {}` 箭头函数本身没有 `this`, 也无法用 `bind`, `apply`,`call` 来改变  `this` 的指向。箭头函数的 `this` 为定义处上下文环境中的`this`
- `'use strict'`, 严格模式下，window 中调用的 function 的 `this` 为 `undefined`

举个🌰

```html
<button id="test">this is a button</button>
```
``` javascript
const button = document.getElementById('test');
button.addEventListener('click', ajaxRequest, true);

function ajaxRequest() {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://localhost:3000/static/text.txt', true);
    xhr.onload = function () {
        console.log('normal function this', this); // what's the output
    };
    xhr.onreadyStateChange = () => {
        console.log('arrow function this', this); // what's the output
    }
    xhr.send();
}
```
---
---
<br>
onload 内的 function 是 xhr 实例出的对象方法调用的，`this` 指向 xhr 这个 object

`onreadyStateChange` 定义在 ajaxRequest 这个 function 内。ajaxRequest 这个 function 被 button 调用，那么应该指向 button 这个元素



