#C＃ #Unity  

### Documentations

-   [DoTween Documentation](http://dotween.demigiant.com/documentation.php#editorMethods)
    
-   [DoTween Examples](http://dotween.demigiant.com/examples.php#header)
    
      DOTween example package DOTweenExamples_Unity5.unitypackage
    

### YouTube Tutorial

https://www.youtube.com/watch?v=Y8cv-rF5j6c

  
### Basics

`using DG.Tweening;`

```C#
// move to
.From() // move from the value
.SetRelative() // move relatively
```

**Transform & Rotation & Scaling**

```C#
// Transform (Absolute World Space)
transform.DOMove
transform.DOMoveX

// Relative World Space
transform.DOMove(new Vector3(1,0,0), 1f).SetRelative();

// Move Local (Object) Space
transform.DOLocalMove(new Vector3(1, 0, 0), 1f);


// Rotation below 360
transform.DORotate(new Vector3(0,270,0), 0.5f).SetEase(Ease.InOutSine).SetLoops(3, LoopType.Yoyo);

// Rotation above 360
transform.DORotate(new Vector3(0,360,0), 0.5f, RotateMode.FastBeyond360).SetEase(Ease.InOutSine);
```

**Set Ease & Loop**

```undefined
.SetEase(Ease.InOutSine);

.SetLoops(-1, LoopType.Yoyo); //infinite loop
```

**OnComplete()**

```C#
.OnComplete(() => {
    //do something Here
});
```

**Sequence**

```C#
var sequence = DOTween.Sequence();

sequence.Append(_material.DOFloat(1, "_Alpha", 0.25f)); // Append Seperately
sequence.Append(_material.DOFloat(1, "_Alpha", 3f));

sequence.Play()

mySequence.AppendInterval(float interval)
```