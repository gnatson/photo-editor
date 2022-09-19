<script>
  export let blur,
    contrast,
    brightness,
    saturate,
    grayscale,
    opacity,
    sepia,
    hue,
    invert
  export let timelineSaveState
</script>

<style>
  #properties {
    position: absolute;
    top: 0px;
    right: 0px;

    background-color: rgba(0, 0, 0, 0.2);
    color: white;
    z-index: 2;
    padding: 2rem;
    margin: 1rem;
    border-top: 0.5rem solid white;
    border-radius: 5px;

    animation: 0.3s scaleUp;
  }
</style>

<div id="properties">
  <p>
    Blur
    <b>{blur}px</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={5}
      step={1}
      bind:value={blur}
      on:change={timelineSaveState} />
  </p>
  <p>
    Contrast
    <b>{contrast}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={300}
      step={10}
      bind:value={contrast}
      on:change={timelineSaveState} />
  </p>
  <p>
    Brightness
    <b>{brightness}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={300}
      step={10}
      bind:value={brightness}
      on:change={timelineSaveState} />
  </p>

  <p>
    Saturate
    <b>{saturate}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={300}
      step={10}
      bind:value={saturate}
      on:change={timelineSaveState} />
  </p>

  <p>
    Grayscale
    <b>{grayscale}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={100}
      step={5}
      bind:value={grayscale}
      on:change={timelineSaveState} />
  </p>

  <p>
    Opacity
    <b>{opacity}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={100}
      step={5}
      bind:value={opacity}
      on:change={timelineSaveState} />
  </p>

  <p>
    Sepia
    <b>{sepia}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={100}
      step={5}
      bind:value={sepia}
      on:change={timelineSaveState} />
  </p>

  <p>
    Hue
    <b>{hue}deg</b>
  </p>
  <p>
    <input
      type="range"
      min={-365}
      max={365}
      step={1}
      bind:value={hue}
      on:change={timelineSaveState} />
  </p>

  <p>
    Invert Colors
    <b>{invert}%</b>
  </p>
  <p>
    <input
      type="range"
      min={0}
      max={100}
      step={10}
      bind:value={invert}
      on:change={timelineSaveState} />
  </p>
</div>
