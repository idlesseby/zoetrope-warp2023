<script>
  import { T, useFrame } from '@threlte/core'
  import { OrbitControls, GLTF, useGltfAnimations, ContactShadows } from '@threlte/extras'
  import { Group } from 'three'

  const { gltf, actions } = useGltfAnimations()

  $: $actions.run?.play()

  const ref = new Group()

  useFrame(() => {
    ref.rotation.y += 0.7892
  })
</script>

<T.PerspectiveCamera
  makeDefault
  position={[-10, 0, 0]}
  fov={15}
>
  <OrbitControls/>
</T.PerspectiveCamera>

<T.DirectionalLight
  intensity={0.8}
/>
<T.AmbientLight intensity={0.5} />

<ContactShadows
  opacity={1}
  scale={10}
  blur={1}
  far={10}
  resolution={256}
  color="#000000"
/>

<GLTF
  bind:gltf={$gltf}
  url="https://threejs.org/examples/models/gltf/Xbot.glb"
/>

<T
  is={ref}
>
  <!-- <T.Mesh scale={2} rotation.x={-Math.PI / 2}>
    <T.PlaneGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh> -->

  <T.Mesh scale={0.1} position={[0.75, 0.2, 0]} >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.11} position={[0.5625, 0.2, 0.5625]} >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.12} position={[0, 0.2, 0.75]}>
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.13} position={[-0.5625, 0.2, 0.5625]} >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.14} position={[-0.75, 0.2, 0]}>
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.13} position={[-0.5625, 0.2, -0.5625]} >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.12} position={[0, 0.2, -0.75]}>
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>

  <T.Mesh scale={0.11} position={[0.5625, 0.2, -0.5625]} >
    <T.SphereGeometry/>
    <T.MeshStandardMaterial color="red"/>
  </T.Mesh>
</T>