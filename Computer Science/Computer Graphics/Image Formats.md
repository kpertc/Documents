

| BMP  | lossless + raw data                                                                                                                                            |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TGA  | lossless + raw data + transparency (compression)                                                                                                               |
| PNG  | lossless + raw data + transparency + modern + compression**                                                                                                    |
| JPG  | lossy                                                                                                                                                          |
| WEBP | lossy or lossless, smaller than JPG                                                                                                                            |
| AVIF | use AV1 compression, smaller than JPG, WEBP, adopted by Netflix<br>> safe everywhere now: Chrome and Opera since 2020, Firefox in 2021, Safari in 2022, Edge in 2024; remaining tradeoff is slow encoding, not support |
| KTX  | KTX1: GPU friendly data, no need uncompression for GPU<br>KTX2 + Basis (ETC1S / UASTC): supercompressed, transcoded at load time to the device's native format (BC7 / ASTC / ETC2) — cheap, but needs a transcoder in the runtime<br>Support GPU-specific compression<br>much less GPU memory consumption                                       |


---
Source: 
- https://www.reddit.com/r/explainlikeimfive/comments/yp499/eli5_what_is_the_difference_between_bmp_jpg_png/
- https://web.dev/learn/images/avif

GLTF:
Convert using gltf-transform
https://github.com/KhronosGroup/KTX-Software/releases
```bash
gltf-transform etc1s in.glb out.glb                          # small, lossy, low quality
gltf-transform uastc in.glb out.glb --level 4 --rdo --zstd 18 # larger, higher quality
# both write KHR_texture_basisu (KTX2 + Basis)
```