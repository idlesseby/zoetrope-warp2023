<script>
  import { T } from '@threlte/core'
	import { ContactShadows, useTexture } from '@threlte/extras';
  import { RepeatWrapping } from 'three'

  const textures = useTexture({
    normal: '/textures/rough_plasterbrick_05_nor_gl_1k.jpg',
    roughness: '/textures/rough_plasterbrick_05_rough_1k.jpg'
  }, {
    transform: (texture) => {
      texture.wrapS = RepeatWrapping
      texture.wrapT = RepeatWrapping
      texture.repeat.set(4, 4)
      return texture
    }
  })
  
</script>
 
{#await textures then textures}
  <T.Mesh
    scale={30}
    rotation.x={-Math.PI * 0.5}
    position.y={-0.1}  
  >
    <T.PlaneGeometry/>
    <T.MeshStandardMaterial 
      roughnessMap={textures.roughness} 
      normalMap={textures.normal}
      normalScale={[0.15, 0.15]}
      color={[0.015, 0.015, 0.015]}
      roughness={0.7}
    />
  </T.Mesh>
{/await}

<ContactShadows
  opacity={1}
  scale={10}
  blur={1}
  far={10}
  resolution={256}
  color="#000000"
/>