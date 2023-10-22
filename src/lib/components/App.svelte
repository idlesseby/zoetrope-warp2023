<script>
  import { Canvas } from '@threlte/core'
  import Scene from './Scene.svelte'
  import Overlay from './Overlay.svelte'
  import Renderer from './Renderer.svelte'
</script>

<Canvas>
  <Scene />
  <Renderer/>
</Canvas>

<Overlay />
