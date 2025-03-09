



### Color to Black
Average
```
(R + G + B) / 3
```

Luminosity (better)
```
vec3 lumiance = vec3(0.299, 0.587, 0.114);
// (0.2125, 0.7154, 0.0721);

vec3 lum = dot(lumiance, color);
```