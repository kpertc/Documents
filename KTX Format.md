
etc1s - lower quality & smaller size
uastc - same quality

files size webp < ktx2 <= png / jpg
vRam ktx2 < webp / png / jpg

`ktx create` https://github.khronos.org/KTX-Software/ktxtools/ktx_create.html
`toktx`
`ktxsc`

``` bash
toktx --t2 --genmipmap --upper_left_maps_to_s0t0 ${webPublicPath}/tonscale.ktx2 ${webPublicPath}/cover.jpg

ktxsc --t2 --encode uastc --zcmp 19 -o ${webPublicPath}/tonscaleIIuastc.ktx2 ${webPublicPath}/tonscale.ktx2
```
