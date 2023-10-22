<script>
  import { T, useFrame } from '@threlte/core'
  import { OrbitControls, GLTF, interactivity, Environment, useCursor } from '@threlte/extras'
  import { Group } from 'three'
  import { gsap } from "gsap";

  const { onPointerEnter, onPointerLeave } = useCursor()

  const ref = new Group()
  let toggle = false
  let speed = {
    value: 0
  }

  const toggleRotation = () => {
    if(toggle) {
      gsap.to(speed, {value: Math.PI / 6, duration: 5, ease: "power2.in"})
    }
    if(!toggle) {
      gsap.to(speed, {value: 0, duration: 4, ease: "circ.out"})
    }
  }

  useFrame(() => {
    ref.rotation.y -= speed.value
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

<T.PerspectiveCamera
  makeDefault
  position={[15, 3, 0]}
  fov={15}
>
  <OrbitControls
    enablePan={false}
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
  on:pointerenter={onPointerEnter}
  on:pointerleave={onPointerLeave}
  on:click={() => {
    toggle = !toggle
    toggleRotation()
  }}
/>