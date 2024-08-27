Install `npm i @tweenjs/tween.js`
npm: https://www.npmjs.com/package/@tweenjs/tween.js

https://tweenjs.github.io/tween.js/docs/user_guide.html

```TypeScript
import * as TWEEN from '@tweenjs/tween.js'

window.addEventListener('mousedown', () => { // mouse down
  console.log("mousedown")

  TWEEN.removeAll()
  new TWEEN.Tween(transitionValue)
    .to({ value: 1 }, 2000)
    .easing(TWEEN.Easing.Quadratic.InOut)
    .start();
})

window.addEventListener('mouseup', () => { // mouse up
  console.log("mouseup")

  TWEEN.removeAll()
  new TWEEN.Tween(transitionValue)
    .to({ value: 0 }, 2000)
    .easing(TWEEN.Easing.Quadratic.InOut)
    .start();
})

function animate() {
  TWEEN.update()
 }
```