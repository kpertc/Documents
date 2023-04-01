#JavaScript #web-dev 

`DOMContentLoaded` event fires when the document has been completely loaded and parsed.

-   window.DOMContentLoaded    
-   Document.DOMContentLoaded


innerHTML

Not recommended to use `innerHTML` for ==performance== and ==security== issues.

-   use `document.createDocumentFragment` instead.
-   `innerHTML` can be passed in executable content. Make sure input is fully converted to string, then pass in.