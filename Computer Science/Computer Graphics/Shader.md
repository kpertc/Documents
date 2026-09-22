
### Blending
> https://youtu.be/AxopC4yW4uY?si=CWtp2Rhf2-KhByYd\

DST - already exist base texture
SRC - new draw
`blendFunction(srcFactor, dstFactor)`
- srcFactor -> Multiplier for SRC
- dstFactor -> Multiplier for DST


Distance vs Length
- `length()` - length of 1 vector
- `distance()` - compare 2 vectors

### Color to Black
Average
```
(R + G + B) / 3
```

Luminosity (better)
```
vec3 luminance = vec3(0.299, 0.587, 0.114);
// (0.2125, 0.7154, 0.0721);

float lum = dot(luminance, color.rgb); // dot() returns float
vec3 gray = vec3(lum);
```

### Normal Map
- Macro detail map
- Micro detail map

##### Blending Normals
- Whiteout - add xy, multiply z
- UDN - cheap, add xy, keep base z
- RNM (Reoriented Normal Mapping) - most correct, rotate detail normal into base normal's frame

### Derivative
dFdx, dFdy | GLSL OpenGL, WebGL
Derivative with respect to Fragment X, Derivative with respect to Fragment Y

ddx, ddy | HLSL
Derivative with respect to X
Derivative with respect to Y

operate on 2×2 pixel blocks

### PBR
> https://www.youtube.com/watch?v=fePsD_8p9vM

- Light Properties (Engine Handle)
- Surface Properties  (User Handle)

Type of Lighting
- Direct Diffuse
- Direct Specular
- Indirect Diffuse
- Indirect Specular  

Diffuse Color
- not darker than 20 or brighter than 240 sRGB
- not darker than 50 if the surface is really rough

Specular
- non-metal surfaces reflect about 4% of light
- 0.5 represent 4 reflection, 1.0 represents 8 reflection
	- surface reflect ==more== on the edge, due to fresnel
	- surface reflect ==less== on crevices

Roughness
 - "focus" of the reflection
 - more of artistic choice

Metallic
- metallic shader and non-metallic shader are two shaders

| Non-Metallic                                         | Metallic                                                                          |
| ---------------------------------------------------- | --------------------------------------------------------------------------------- |
| Base Color → Diffuse<br>Specular → Reflectance 0-8%  | Base Color → Reflectance 0-100%<br>Specular → Not used<br>Diffuse is always black |

- Try to create an either non-metallic or full metallic material, blending in half is weird
- no dark metal, metals are 180 sRGB brighter


`saturate()` | HLSL only, no GLSL equivalent
`saturate()` = `clamp(var, 0.0, 1.0)`
`saturate()` has hardware acceleration, use `saturate()` for clamping value to 0 -1,
use `clamp()` to clamp value other than 0-1
in GLSL write `clamp(x, 0.0, 1.0)` — GLSL ES 1.00 has no implicit int → float, so `clamp(x, 0, 1)` fails


Parallax Shader
- offset UV by heightmap along the tangent-space view direction
