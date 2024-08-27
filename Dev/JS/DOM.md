#JavaScript #web-dev 

`DOMContentLoaded` event fires when the document has been completely loaded and parsed.

-   window.DOMContentLoaded    
-   Document.DOMContentLoaded


innerHTML

Not recommended to use `innerHTML` for ==performance== and ==security== issues.

-   use `document.createDocumentFragment` instead.
-   `innerHTML` can be passed in executable content. Make sure input is fully converted to string, then pass in.


`window.onload` -> open the page

`window.onbeforeunload` -> before close the page

<br/>

### Browser or node.js

https://bobbyhadz.com/blog/javascript-referenceerror-window-is-not-defined

- In browser env window exist, 
- In node.js env, window does not exist

```js
if (typeof window !== 'undefined') {
  console.log('You are on the browser');

  // ✅ Can use window here
  console.log(window.innerWidth);

  window.addEventListener('mousemove', () => {
    console.log('Mouse moved');
  });
} else {
  console.log('You are on the server');
  // ⛔️ Don't use window here
}
```

<br>

### Get Page URL / BaseURL
```js
const base_url = window.location.origin; // http://localhost:3000
const host = window.location.host; // localhost:3000
```


```
function setScrollVar() {

}
```