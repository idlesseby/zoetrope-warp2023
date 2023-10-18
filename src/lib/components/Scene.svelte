<script>
  import { T, useFrame } from '@threlte/core'
  import { OrbitControls, GLTF, interactivity } from '@threlte/extras'
  import { Group } from 'three'
  import { gsap } from "gsap";
	import Ground from './Ground.svelte';

  interactivity()

  const ref = new Group()
  let speed = {
    value: 0
  }

  function start() {
    gsap.to(speed, {value: Math.PI / 4, duration: 8, ease: "power2.in"})
  }

  useFrame((state) => {
    //const time = state.clock.getElapsedTime()
    ref.rotation.y -= speed.value
  })
</script>

<T.PerspectiveCamera
  makeDefault
  position={[-25, 5, 0]}
  fov={15}
>
  <OrbitControls/>
</T.PerspectiveCamera>

<T.DirectionalLight
  intensity={1.2}
/>

<Ground/>

<T
  is={ref}
>
  <GLTF
    url={'./model/Zoetrope.glb'}
    scale={1}
    useDraco
  />

  <T.Mesh 
    scale={0.1} 
    on:click={() => {
      start()
    }}
  >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>
</T>