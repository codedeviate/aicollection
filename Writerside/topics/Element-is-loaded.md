# Element is loaded

One of the trickier things to do in JavaScript is to check if an element has been updated with new content. This can be useful when you need to perform some action after the element has been updated, such as animating the new content or updating other parts of the page.

We have an arbitrary element in the DOM:
```html
<div id="element"></div>
```

There are three ways to check if new content is loaded into the element:

## setTimeout

The first way to check if the element has been updated is to use `setTimeout` with a delay of `0` milliseconds. This will execute the callback function after the current script has finished executing and the element has been updated in the DOM:

```javascript
const container = document.getElementById('element');
container.innerHTML = '<div>New content</div>';

setTimeout(() => {
    console.log('Element has been updated!');
}, 0);
```

## requestAnimationFrame

The second way is to use `requestAnimationFrame`, which will execute the callback function before the next repaint of the browser, ensuring that the element has been updated and rendered in the DOM:

```javascript
const container = document.getElementById('element');
container.innerHTML = '<div>New content</div>';

requestAnimationFrame(() => {
    console.log('Element has been updated and rendered!');
});
```

## MutationObserver

The third way is to use a `MutationObserver` to watch for changes in the element's content. This method allows you to observe changes to the DOM and trigger a callback function when the element is updated:

```javascript
const container = document.getElementById('element');
const observer = new MutationObserver(() => {
    console.log('Element has been updated!');
});
observer.observe(container, { childList: true, subtree: true });

container.innerHTML = '<div>New content</div>';
```

## Summary

There is no foolproof way to check if an element has been updated with new content and rendered, but these methods provide different ways to detect changes in the DOM and trigger actions accordingly. Depending on your use case, you can choose the method that best suits your needs.