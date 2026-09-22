#JavaScript #web-dev 

`DOMContentLoaded` event fires when the document has been completely loaded and parsed.

-   `document.addEventListener('DOMContentLoaded', handler)`
-   fired at `document`, bubbles to `window` → a `window` listener works too (no `onDOMContentLoaded` property exists)


innerHTML

Not recommended to use `innerHTML` for ==performance== and ==security== issues.

-   performance: batch with `document.createDocumentFragment`, or build one string and assign once. Reflow only, no security benefit.
-   security: whatever you pass is parsed as HTML — stringifying the input does NOT help. Text → `element.textContent`. Real HTML → sanitize (DOMPurify) / Trusted Types.


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


```js
// drive CSS from scroll position: var(--scroll) in stylesheet
function setScrollVar() {
	const ratio = window.scrollY / (document.documentElement.scrollHeight - window.innerHeight);
	document.documentElement.style.setProperty('--scroll', String(ratio));
}
```