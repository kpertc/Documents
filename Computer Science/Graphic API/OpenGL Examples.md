



![[circle.png | 300]]

### Create a circle

```glsl
uniform vec2 u_resolution;

float circleshape(vec2 position, float radius) {
    return step(radius, length(position - vec2(0.5 * u_resolution.x / u_resolution.y, 0.5))); // center follows the aspect fix
}

void main() {

    vec2 position = gl_FragCoord.xy / u_resolution; // x, y normalized to 0 - 1
    position.x *= u_resolution.x / u_resolution.y; // aspect fix, otherwise it draws an ellipse

    vec3 color = vec3(circleshape(position, 0.2));

    gl_FragColor = vec4(color,1);
}
```