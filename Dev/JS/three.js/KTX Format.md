
etc1s - lower quality & smaller size
uastc - same quality

files size webp < ktx2 <= png / jpg
vRam ktx2 < webp / png / jpg
[[Image Formats]]

`ktx create` https://github.khronos.org/KTX-Software/ktxtools/ktx_create.html
`toktx` legacy
`ktxsc` legacy

``` bash
# current, one step, upper-left is the default so no orientation flag needed
ktx create --format R8G8B8_SRGB --generate-mipmap --encode basis-lz ${webPublicPath}/cover.jpg ${webPublicPath}/tonscale.ktx2
ktx create --format R8G8B8_SRGB --generate-mipmap --encode uastc --zstd 19 ${webPublicPath}/cover.jpg ${webPublicPath}/tonscaleIIuastc.ktx2

# ktx encode, re-encode an existing ktx2
ktx encode --codec uastc --zstd 19 ${webPublicPath}/tonscale.ktx2 ${webPublicPath}/tonscaleIIuastc.ktx2

# legacy
toktx --t2 --genmipmap --upper_left_maps_to_s0t0 ${webPublicPath}/tonscale.ktx2 ${webPublicPath}/cover.jpg

ktxsc --t2 --encode uastc --zcmp 19 -o ${webPublicPath}/tonscaleIIuastc.ktx2 ${webPublicPath}/tonscale.ktx2
```

load in three.js
``` js
const ktx2 = new KTX2Loader()
	.setTranscoderPath('/basis/') // copy from three/examples/jsm/libs/basis/ into public
	.detectSupport(renderer) // skip it → THREE.KTX2Loader: Missing initialization with detectSupport
gltfLoader.setKTX2Loader(ktx2)
```
