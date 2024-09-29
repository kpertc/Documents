#JavaScript #web-dev 

[[API]]

### Math
##### Get Random number to Integer 
``` js
const range = 10000;
const randomInteger = Math.floor(range * Math.random())
```

##### DataURL

Typically for transferring image

"data:image/jpeg;base64,I9J14RW..."

Type Encode actual content

##### Base64 Encoding

将任何二进制数据编码为ASCII的纯文本字符

64 -> 2^6

Because American Standard Code for Information Interchange (ASCII) only supports 2^7
-   Sending binary data over text-based protocol (such as HTTP)
-   Ensures text not get corrupted
-   Does not conceal data
  

```JavaScript
btoa() // Encode to Base64
atob() // decode
```

### URL Decode

```js
// 当不想网站自动转换成ASCII `%D1%88%D0%B5%D0%BB%D0%BB%D1%8B` 时用
decodeURIComponent(document.URL)

// 
encodeURIComponent(document.URL)
```

### Calculate percentage of scrolling of element 
```js
const scrollTop = parentElement.scrollTop; 
const scrollHeight = parentElement.scrollHeight - parentElement.clientHeight; 
if (scrollHeight === 0) return 0; 
const scrollPercentage = (scrollTop / scrollHeight) * 100;
```