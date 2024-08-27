[Houdini Unified Noise](https://www.sidefx.com/docs/houdini/nodes/vop/unifiednoise.html)


### Tutorial

[[YouTube] [VEX for Algorithmic Design] E19 _ Noise Basics by Junichiro Horikawa](https://youtu.be/Q2OUvq4BcFk)

|![[img/Houdini Noise/unifiednoise_types.jpg \| 400]]|![[img/Houdini Noise/noise in Houdini.png]]|
|-|-|


### Perlin Noise & Simplex Noise

by Ken Perlin

-   `noise()` [Perlin Noise](https://www.sidefx.com/docs/houdini/vex/functions/noise.html)
-   `xnoise()` [Simplex Noise](https://www.sidefx.com/docs/houdini/vex/functions/xnoise.html)

* Scale
+ Offset X / Z -> Shifting; Offset Y -> Waving

```C#
float val = noise(@P * chf("scale") + set(0,0,0)); 
```

  

Noise value will mostly distribute between 0.25 - 0.75.

Remap value to range 0 -1

```C#
clampedNoise = clamp(noiseVal, 0.25, 0.75)
fit(clampedNoise, 0.25, 0.75, 0.0, 1.0) // remap range to 0-1
```


Use Vector4 to "waving" 3D / use as shift vector

```C#
vector4 v = set(pos.x, pos.y, pos.z, chf("shift"));
vector col = noise(v);
```

### Periodic Noise
![[img/Houdini Noise/pnoise.png | 300 ]]

>... repeats itself over a given range of the space. The periodic form can be used to generate patterns which 'tile' over N-dimensional space (i.e. a noise-based texture map which repeats seamlessly).

[pnoise()](https://www.sidefx.com/docs/houdini/vex/functions/pnoise.html)
set 0 non-periodic
set !0 - periodic


Flow Noise
[flownoise()](https://www.sidefx.com/docs/houdini/vex/functions/flownoise.html)

Curl Noise

### Worley Noise

-   Euclidean Distance
-   Manhattan Distance
-   Chebyshev Distance


& -> output variable
[wnoise](https://www.sidefx.com/docs/houdini/vex/functions/wnoise.html)
`wnoise()` both periodic and non-periodic

![[img/Houdini Noise/wnoise.png]]