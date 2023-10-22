<div class="overlay">
  <div class="instruction">click tree to toggle rotate</div>
  <div class="signature">A digital Zoetrope made by idlesseby</div>
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
  }

  .instruction {
    position: absolute;
    top: 16px;
    left: 16px;
    font-size: 14px;
    font-weight: 100;
  }

  .signature {
    position: absolute;
    bottom: 16px;
    right: 16px;
    font-size: 14px;
  }

  @media (min-width: 480px) {
    .instruction {
      top: 24px;
      left: 24px;
      font-size: 18px;
    }

    .signature {
      bottom: 24px;
      right: 24px;
      font-size: 18px;
    }
  }
</style>
