



![[circle.png | 300]]

### Create a circle

```glsl
uniform vec2 u_resolution;

float circleshape(vec2 position, float radius) {
    return step(radius, length(position - vec2(0.5)));
}

void main() {

    vec2 position = gl_FragCoord.xy / u_resolution; // x y 0 -1

    vec3 color = vec3(circleshape(position, 0.2));

    gl_FragColor = vec4(color,1);
}
```