<script>
  import { T, useFrame } from '@threlte/core'
  import { OrbitControls, GLTF, interactivity, Environment } from '@threlte/extras'
  import { Group } from 'three'
  import { gsap } from "gsap";

  const ref = new Group()

  $: innerWidth = 0
	$: innerHeight = 0

  let mouseStartPos = 0
  let mouseCurrPos = 0
  let dragStrength = 0
  let rotationSpeed = 0
  let isDragActive = false

  const startDrag = (event) => {
    isDragActive = true
    mouseStartPos = event.clientX - innerWidth / 2
  }

  const getMouseCurrPos = (event) => {
    mouseCurrPos = event.clientX - innerWidth / 2
  }

  const stopDrag = () => {
    isDragActive = false
  }

  useFrame(() => {
    if(isDragActive) {
      dragStrength = (mouseCurrPos - mouseStartPos) / 10000
    }

    if(Math.abs(dragStrength) > 0.2) {
      dragStrength = Math.PI / 6
    }

    if(dragStrength > 0) {
      dragStrength -= 0.0005
    }

    if(dragStrength < 0) {
      dragStrength += 0.0005
    }

    rotationSpeed += (dragStrength - rotationSpeed) * 0.2

    ref.rotation.y += rotationSpeed
  })

  interactivity()
</script>

<!-- 3D-Models:
  Fall Tree V1 by Danni Bittman [CC-BY] via Poly Pizza - https://poly.pizza/m/0rx_H4qbwBp
  Husky by Quaternius via Poly Pizza - https://poly.pizza/m/wcWiuEqwzq
  Ghost Skull by Quaternius via Poly Pizza - https://poly.pizza/m/TX8r9WBXpe
  basic stone 3 by felix stief [CC-BY] via Poly Pizza - https://poly.pizza/m/3a0ubCurnwU
  Halloween Pumpkin by Neil Realubit [CC-BY] via Poly Pizza - https://poly.pizza/m/2Z1UzUc0No4
-->

<svelte:window on:mousedown={startDrag} on:mousemove={getMouseCurrPos} on:mouseup={stopDrag} bind:innerWidth bind:innerHeight/>

<T.PerspectiveCamera
  makeDefault
  position={[15, 1, 0]}
  fov={15}
>
  <OrbitControls
    enablePan={false}
    enableRotate={false}
    minDistance={8}
    maxDistance={25}
    maxPolarAngle={1.5}
  />
</T.PerspectiveCamera>

<Environment
  path="/envmap/"
  files={'autumn_meadow_1k.hdr'} 
/>

<T
  is={ref}
>
  <GLTF
    url={'./model/Zoetrope.glb'}
    scale={1}
    useDraco
    position={[0, -0.5, 0]}
  />
</T>

<GLTF
  url={'./model/Fall Tree V1.glb'}
  scale={0.6}
  useDraco
  position={[0, 0.75, 0]}
/>