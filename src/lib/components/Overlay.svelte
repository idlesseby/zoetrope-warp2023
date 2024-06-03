<script>
  import { dragStrength } from "../stores"

  let exclamationDiv
  let exclamationText = ""
  let isVisible = false

  const updateExclamation = () => {
    if(Math.abs($dragStrength) < 0.075) {
      exclamationText = ""
      isVisible = false
    }

    if(Math.abs($dragStrength) > 0.075 && Math.abs($dragStrength) < 0.125) {
      exclamationText = "Spin harder!"
      isVisible = true
    }

    if(Math.abs($dragStrength) > 0.125 && Math.abs($dragStrength) < 0.15) {
      exclamationText = "Almost!"
      isVisible = true
    }

    if(Math.abs($dragStrength) >= 0.15) {
      exclamationText = "Awesome!"
      isVisible = true
    }
  }

</script>

<svelte:window 
  on:mouseup={updateExclamation}
/>

<div class="overlay">
  <div class="instruction">
    <div class="instruction-header">Instructions:</div>
    <ul class="instruction-points">
      <li>Drag/swipe horizontally over screen to spin the zoetrope</li>
      <li>Drag/swipe far enough to make the illusion appear</li>
    </ul>
  </div>
  <div 
    bind:this={exclamationDiv} 
    style="transition: all 0.3s; opacity: {isVisible ? 1 : 0}; transform: scale({isVisible ? 1 : 0.25}); translateY({isVisible ? '-100%' : '0%'})"
    class="exclamation"
  >
    <p>{exclamationText}</p>
  </div>
  <div class="signature">A digital Zoetrope made by Sebastian Mödritzer</div>
  <div class="mobile-warning">
    <p>Mobile version under construction</p>
  </div>
</div>

<style>
  .overlay {
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    pointer-events: none;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .instruction {
    position: absolute;
    bottom: 12px;
    left: 16px;
    display: none;
  }

  .instruction-header {
    font-weight: 500;
    font-size: 16px;
  }

  .instruction-points {
    font-weight: 100;
    margin-top: 4px;
    font-size: 14px;
    padding-left: 24px;
  }

  .exclamation {
    position: absolute;
    font-size: 36px;
    width: 100%;
    text-align: center;
    bottom: 160px;
    display: none;
  }

  .signature {
    position: absolute;
    top: 16px;
    right: 16px;
    font-size: 14px;
    display: none;
  }

  .mobile-warning {
    display: block;
    font-size: 28px;
    text-align: center;
  }

  @media (min-width: 480px) {
    .instruction {
      bottom: 12px;
      left: 24px;
      display: block;
    }

    .instruction-header {
      font-size: 18px;
    }

    .instruction-points {
      margin-top: 8px;
      font-size: 18px;
      padding-left: 30px;
    }

    .exclamation {
      font-size: 66px;
      display: block;
    }

    .signature {
      top: 24px;
      right: 24px;
      font-size: 18px;
      display: block;
    }

    .mobile-warning {
      display: none;
    }
  }
</style>
