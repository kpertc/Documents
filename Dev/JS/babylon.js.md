

```

```


``` js
scene.debugLayer.show();
```

Particle System
``` js
// Create a particle system
const particleSystem = new ParticleSystem("particles", 2000, scene);

//Texture of each particle
particleSystem.particleTexture = new Texture("textures/flare.png");

// Position where the particles are emiited from
particleSystem.emitter = new Vector3(0, 0.5, 0);
particleSystem.start();
```