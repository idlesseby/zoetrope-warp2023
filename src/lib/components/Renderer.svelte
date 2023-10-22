<script>
  import { useThrelte, useRender } from '@threlte/core'
  import {
    EffectComposer,
    EffectPass,
    RenderPass,
    SMAAEffect,
    SMAAPreset,
    BloomEffect,
    KernelSize
  } from 'postprocessing'
  const { scene, renderer, camera, size } = useThrelte()
  // To use the EffectComposer we need to pass arguments to the
  // default WebGLRenderer: https://github.com/pmndrs/postprocessing#usage
  const composer = new EffectComposer(renderer)
  const setupEffectComposer = (camera) => {
    composer.removeAllPasses()
    composer.addPass(new RenderPass(scene, camera))
    composer.addPass(
      new EffectPass(
        camera,
        new BloomEffect({
          intensity: 0.35,
          luminanceThreshold: 0.15,
          height: 512,
          width: 512,
          luminanceSmoothing: 0.08,
          mipmapBlur: true,
          kernelSize: KernelSize.MEDIUM
        })
      )
    )
    composer.addPass(
      new EffectPass(
        camera,
        new SMAAEffect({
          preset: SMAAPreset.LOW
        })
      )
    )
  }
  // We need to set up the passes according to the camera in use
  $: setupEffectComposer($camera)
  $: composer.setSize($size.width, $size.height)
  useRender((_, delta) => {
    composer.render(delta)
  })
</script>