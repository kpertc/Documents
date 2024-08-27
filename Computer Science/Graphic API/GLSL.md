[[OpenGL]]

OpenGL Shading Language
Syntax similar to C/C++

-   Version Specification
    -   OpenGL version
    -   GLSL version

### Comment
```glsl
/* 
	Multi-line comment
*/

// Single-line comment
```

### Variable

<div style="display: grid; grid-template-columns: repeat(3, 2fr); grid-gap: 10px;">
	<div> 
		<span>float</span><br>
		<span>vec2</span><br>
		<span>vec3</span><br>
		<span>vec4</span><br>
	 </div> 
	 <div> 
		<span></span><br>
		<span>mat2</span><br>
		<span>mat3</span><br>
		<span>mat4</span><br>
	 </div> 
	 <div> 
		<span>int</span><br>
		<span>ivec2</span><br>
		<span>ivec3</span><br>
		<span>ivec4</span><br>
	 </div> 
</div>

bool
sampler2D

### Float

```glsl
vec3 color = vec3(0.0, 0.0 ,0.0);

vec3 color = vec3(1.0); // = vec3(1.0, 1.0, 1.0)

// compose vector
vec4 colorAlpha = vec4(color, 1.0);
```

### Vector 

```glsl
vec3 color = vec3(0.0, 0.0 ,0.0);

vec3 color = vec3(1.0); // = vec3(1.0, 1.0, 1.0)

// compose vector
vec4 colorAlpha = vec4(color, 1.0);
```

##### Swizzling
```glsl
vec3 color = colorAlpha.rgb;
vec3 colorBGR = colorAlpha.bgr;
vec4 grayscale = colorAlpha.rrra; 
```

<div style="display: grid; grid-template-columns: repeat(4, 2fr); grid-gap: 10px;">
	<div> 
		<span>Array-style accessor</span><br>
		<span>[0]</span><br>
		<span>[1]</span><br>
		<span>[2]</span><br>
		<span>[3]</span><br>
	 </div> 
	 <div> 
		<span>Coordinate Dimension</span><br>
		<span>.x</span><br>
		<span>.y</span><br>
		<span>.z</span><br>
		<span>.w</span><br>
	 </div> 
	 <div> 
		<span>Color Channel</span><br>
		<span>.r</span><br>
		<span>.g</span><br>
		<span>.b</span><br>
		<span>.a</span><br>
	 </div> 
	 <div> 
		<span>Texture Dimension</span><br>
		<span>.s</span><br>
		<span>.t</span><br>
		<span>.p</span><br>
		<span>.q</span><br>
	 </div> 
</div>

### Matrix

```glsl
mat3 identityMatrix = mat3(
	1.0, 0.0, 0.0,
	0.0, 1.0, 0.0,
	0.0, 0.0, 1.0
);
```

### Loop
```glsl
for(float i = 1.0; i <= 3.0; i++) // 3 times
{
    ...
}
```

### Function
```glsl
float computeSum(float a, float b) {
	return a + b;
}
```

```glsl
float computeSum(in float a, in float b) {
	return a + b;
}

float computeSum(out float a, out float b) {
	return a + b;
}

float computeSum(inout float a, inout float b) {
	return a + b;
}
```

Let `vec4` interact with `vec3`
``` glsl
vec4Variable.xyz += vec3Variable
```

### if else
``` glsl
vec2 direction;
float angle; 

if (length(uIntersect - uLastPos) > 0.01) 
{ 
	direction = normalize(uIntersect - uLastPos);
	angle = atan(direction.y, direction.x); 
}
else
{ 
	vec2 direction = vec2(1.0, 1.0); 
	float angle = 0.0; 
}
```


```
step()

remap()
smoothstep()
smoothstep(0.4, 1.0) 
// 0-1 clamped value
// let 0.4 → 0.0, 1.0 → 1.0

min()
max()

pow() // let gradient fade faster

abs()
mix()

clamp()

floor()

plot() ?
rect() ?

fract() // 0.xxxxx
mod()
```

### built-in variable

| variable         | type    | usage | website                                                                    |
| ---------------- | ------- | ----- | -------------------------------------------------------------------------- |
| `gl_FrontFacing` | boolean |       | https://registry.khronos.org/OpenGL-Refpages/gl4/html/gl_FrontFacing.xhtml |
|                  |         |       |                                                                            |

Circle
```
float radius = 0.1;
float dist = distance(vUv, uIntersect);
float color = 1.0 - step(radius, dist);
```

##### non-glsl Functions



###### Rotate2D
```glsl
vec2 rotate2D(vec2 value, float angle) {
    float s = sin(angle);
    float c = cos(angle);
    mat2 m = mat2(c, s, -s, c);
    return m * value;
}
```
##### Scale
```glsl
mat2 scale(vec2 scale) {
    return mat2(scale.x, 0.0, 0.0, scale.y);
}
```
##### Remap
``` glsl
float remap(float value, float originMin, float originMax, float destinationMin, float destinationMax) {
    return destinationMin + (value - originMin) * (destinationMax - destinationMin) / (originMax - originMin);
}
```
##### 1d noise
``` gls
float noise1d(float value) {
    return cos(value + cos(value * 90.0) * 100.0) * 0.5 + 0.5;
}
```

Noise Functions
https://gist.github.com/patriciogonzalezvivo/670c22f3966e662d2f83

Simple Noise 4D
``` glsl
//	Simplex 4D Noise 
//	by Ian McEwan, Ashima Arts
//
vec4 permute(vec4 x){return mod(((x*34.0)+1.0)*x, 289.0);}
float permute(float x){return floor(mod(((x*34.0)+1.0)*x, 289.0));}
vec4 taylorInvSqrt(vec4 r){return 1.79284291400159 - 0.85373472095314 * r;}
float taylorInvSqrt(float r){return 1.79284291400159 - 0.85373472095314 * r;}

vec4 grad4(float j, vec4 ip){
  const vec4 ones = vec4(1.0, 1.0, 1.0, -1.0);
  vec4 p,s;

  p.xyz = floor( fract (vec3(j) * ip.xyz) * 7.0) * ip.z - 1.0;
  p.w = 1.5 - dot(abs(p.xyz), ones.xyz);
  s = vec4(lessThan(p, vec4(0.0)));
  p.xyz = p.xyz + (s.xyz*2.0 - 1.0) * s.www; 

  return p;
}

float simplexNoise4d(vec4 v){
  const vec2  C = vec2( 0.138196601125010504,  // (5 - sqrt(5))/20  G4
                        0.309016994374947451); // (sqrt(5) - 1)/4   F4
// First corner
  vec4 i  = floor(v + dot(v, C.yyyy) );
  vec4 x0 = v -   i + dot(i, C.xxxx);

// Other corners

// Rank sorting originally contributed by Bill Licea-Kane, AMD (formerly ATI)
  vec4 i0;

  vec3 isX = step( x0.yzw, x0.xxx );
  vec3 isYZ = step( x0.zww, x0.yyz );
//  i0.x = dot( isX, vec3( 1.0 ) );
  i0.x = isX.x + isX.y + isX.z;
  i0.yzw = 1.0 - isX;

//  i0.y += dot( isYZ.xy, vec2( 1.0 ) );
  i0.y += isYZ.x + isYZ.y;
  i0.zw += 1.0 - isYZ.xy;

  i0.z += isYZ.z;
  i0.w += 1.0 - isYZ.z;

  // i0 now contains the unique values 0,1,2,3 in each channel
  vec4 i3 = clamp( i0, 0.0, 1.0 );
  vec4 i2 = clamp( i0-1.0, 0.0, 1.0 );
  vec4 i1 = clamp( i0-2.0, 0.0, 1.0 );

  //  x0 = x0 - 0.0 + 0.0 * C 
  vec4 x1 = x0 - i1 + 1.0 * C.xxxx;
  vec4 x2 = x0 - i2 + 2.0 * C.xxxx;
  vec4 x3 = x0 - i3 + 3.0 * C.xxxx;
  vec4 x4 = x0 - 1.0 + 4.0 * C.xxxx;

// Permutations
  i = mod(i, 289.0); 
  float j0 = permute( permute( permute( permute(i.w) + i.z) + i.y) + i.x);
  vec4 j1 = permute( permute( permute( permute (
             i.w + vec4(i1.w, i2.w, i3.w, 1.0 ))
           + i.z + vec4(i1.z, i2.z, i3.z, 1.0 ))
           + i.y + vec4(i1.y, i2.y, i3.y, 1.0 ))
           + i.x + vec4(i1.x, i2.x, i3.x, 1.0 ));
// Gradients
// ( 7*7*6 points uniformly over a cube, mapped onto a 4-octahedron.)
// 7*7*6 = 294, which is close to the ring size 17*17 = 289.

  vec4 ip = vec4(1.0/294.0, 1.0/49.0, 1.0/7.0, 0.0) ;

  vec4 p0 = grad4(j0,   ip);
  vec4 p1 = grad4(j1.x, ip);
  vec4 p2 = grad4(j1.y, ip);
  vec4 p3 = grad4(j1.z, ip);
  vec4 p4 = grad4(j1.w, ip);

// Normalise gradients
  vec4 norm = taylorInvSqrt(vec4(dot(p0,p0), dot(p1,p1), dot(p2, p2), dot(p3,p3)));
  p0 *= norm.x;
  p1 *= norm.y;
  p2 *= norm.z;
  p3 *= norm.w;
  p4 *= taylorInvSqrt(dot(p4,p4));

// Mix contributions from the five corners
  vec3 m0 = max(0.6 - vec3(dot(x0,x0), dot(x1,x1), dot(x2,x2)), 0.0);
  vec2 m1 = max(0.6 - vec2(dot(x3,x3), dot(x4,x4)            ), 0.0);
  m0 = m0 * m0;
  m1 = m1 * m1;
  return 49.0 * ( dot(m0*m0, vec3( dot( p0, x0 ), dot( p1, x1 ), dot( p2, x2 )))
               + dot(m1*m1, vec2( dot( p3, x3 ), dot( p4, x4 ) ) ) ) ;

}
```

  Homogeneous translation vs not translation\

| translate                          | not translate                      |
| ---------------------------------- | ---------------------------------- |
| ![[glsl-translate-normal.gif.gif]] | ![[glsl-not-translate-normal.gif]] |
| `modelMatrix * vec4(normal, 1.0)`  | `modelMatrix * vec4(normal, 0.0)`  |

### Effects

##### Edge Fade Mask
```glsl
edgeMask = smoothstep(0.0, 0.1, vUv.x)
edgeMask = smoothstep(0.9, 1.0, vUv.x)
```
##### Blink
```glsl
// blink
float blinkValue = step(0.5, fract(u_Time));
// fract() to extract the fractional part (i.e., the 0.xxx part)

// gradient blink
float blinkValue = abs(sin(u_Time));
```

##### Floor
![[glsl-floor.png|300]]
```glsl
// floor the value to the nearest integer value
float value = floor(uv.x * 5.0) / 5.0; 
```

##### Fresnel
![[glsl-fresnel.gif|300]]

varying
```
varying vec3 vWorldNormal;
varying vec3 vWorldPosition;
```

vs
``` glsl
vWorldNormal = (modelMatrix * vec4(normal, 0.0)).xyz; // 0.0 → not translation
vWorldPosition = (modelMatrix * vec4(position, 1.0)).xyz;
```

fs
``` glsl
// normalize
vec3 normalizedWorldNormal = normalize(vWorldNormal); // normal in fs maybe not length of 1, so need to be normalized
vec3 viewDirection = normalize(cameraPosition - vWorldPosition);

float fresnel = dot(viewDirection, normalizedWorldNormal);
fresnel = 1.0 - fresnel;
// fresnel = pow(fresnel, 2.0); // increase contrast
// fresnel = smoothstep(0.2, 0.8, fresnel); // smooth
gl_FragColor = vec4(vec3(1.0), fresnel);
```

``` js
// material
depthWrite: false,
```

##### Perlin 3D Noise
Perlin noise is bad for performance ☞ use simple perlin texture instead
```glsl
Classic Perlin 3D Noise 
// by Stefan Gustavson
//
vec4 permute(vec4 x)
{
    return mod(((x*34.0)+1.0)*x, 289.0);
}
vec4 taylorInvSqrt(vec4 r)
{
    return 1.79284291400159 - 0.85373472095314 * r;
}
vec3 fade(vec3 t)
{
    return t*t*t*(t*(t*6.0-15.0)+10.0);
}

float cnoise(vec3 P)
{
    vec3 Pi0 = floor(P); // Integer part for indexing
    vec3 Pi1 = Pi0 + vec3(1.0); // Integer part + 1
    Pi0 = mod(Pi0, 289.0);
    Pi1 = mod(Pi1, 289.0);
    vec3 Pf0 = fract(P); // Fractional part for interpolation
    vec3 Pf1 = Pf0 - vec3(1.0); // Fractional part - 1.0
    vec4 ix = vec4(Pi0.x, Pi1.x, Pi0.x, Pi1.x);
    vec4 iy = vec4(Pi0.yy, Pi1.yy);
    vec4 iz0 = Pi0.zzzz;
    vec4 iz1 = Pi1.zzzz;

    vec4 ixy = permute(permute(ix) + iy);
    vec4 ixy0 = permute(ixy + iz0);
    vec4 ixy1 = permute(ixy + iz1);

    vec4 gx0 = ixy0 / 7.0;
    vec4 gy0 = fract(floor(gx0) / 7.0) - 0.5;
    gx0 = fract(gx0);
    vec4 gz0 = vec4(0.5) - abs(gx0) - abs(gy0);
    vec4 sz0 = step(gz0, vec4(0.0));
    gx0 -= sz0 * (step(0.0, gx0) - 0.5);
    gy0 -= sz0 * (step(0.0, gy0) - 0.5);

    vec4 gx1 = ixy1 / 7.0;
    vec4 gy1 = fract(floor(gx1) / 7.0) - 0.5;
    gx1 = fract(gx1);
    vec4 gz1 = vec4(0.5) - abs(gx1) - abs(gy1);
    vec4 sz1 = step(gz1, vec4(0.0));
    gx1 -= sz1 * (step(0.0, gx1) - 0.5);
    gy1 -= sz1 * (step(0.0, gy1) - 0.5);

    vec3 g000 = vec3(gx0.x,gy0.x,gz0.x);
    vec3 g100 = vec3(gx0.y,gy0.y,gz0.y);
    vec3 g010 = vec3(gx0.z,gy0.z,gz0.z);
    vec3 g110 = vec3(gx0.w,gy0.w,gz0.w);
    vec3 g001 = vec3(gx1.x,gy1.x,gz1.x);
    vec3 g101 = vec3(gx1.y,gy1.y,gz1.y);
    vec3 g011 = vec3(gx1.z,gy1.z,gz1.z);
    vec3 g111 = vec3(gx1.w,gy1.w,gz1.w);

    vec4 norm0 = taylorInvSqrt(vec4(dot(g000, g000), dot(g010, g010), dot(g100, g100), dot(g110, g110)));
    g000 *= norm0.x;
    g010 *= norm0.y;
    g100 *= norm0.z;
    g110 *= norm0.w;
    vec4 norm1 = taylorInvSqrt(vec4(dot(g001, g001), dot(g011, g011), dot(g101, g101), dot(g111, g111)));
    g001 *= norm1.x;
    g011 *= norm1.y;
    g101 *= norm1.z;
    g111 *= norm1.w;

    float n000 = dot(g000, Pf0);
    float n100 = dot(g100, vec3(Pf1.x, Pf0.yz));
    float n010 = dot(g010, vec3(Pf0.x, Pf1.y, Pf0.z));
    float n110 = dot(g110, vec3(Pf1.xy, Pf0.z));
    float n001 = dot(g001, vec3(Pf0.xy, Pf1.z));
    float n101 = dot(g101, vec3(Pf1.x, Pf0.y, Pf1.z));
    float n011 = dot(g011, vec3(Pf0.x, Pf1.yz));
    float n111 = dot(g111, Pf1);

    vec3 fade_xyz = fade(Pf0);
    vec4 n_z = mix(vec4(n000, n100, n010, n110), vec4(n001, n101, n011, n111), fade_xyz.z);
    vec2 n_yz = mix(n_z.xy, n_z.zw, fade_xyz.y);
    float n_xyz = mix(n_yz.x, n_yz.y, fade_xyz.x); 
    return 2.2 * n_xyz;
}
```