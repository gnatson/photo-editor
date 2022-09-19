<script>
  // todo: construct custom filter
  // animated transitions with svelte/easing... (bounce effect)
  //  user preferences? (ex. slider step)
  // animated preview

  let blur = 0
  let contrast = 100
  let grayscale = 0
  let hue = 0
  let invert = 0

  $: style = `filter: blur(${blur}px) contrast(${contrast}%) grayscale(${grayscale}%) hue-rotate(${hue}deg) drop-shadow(16px 16px 20px black) invert(${invert}%);`
</script>

<style>
  main {
    user-select: none;
  }
</style>

<main>
  <div id="photo">
    <img src="photos/geran-de-klerk-bKhETeDV1WM-unsplash.jpg" alt="" {style} />
    <!-- maybe div.background? -->
  </div>

  <div id="properties">

    <p>
      Blur:
      <input type="range" min={0} max={5} step={1} bind:value={blur} />
      <b>{blur}px</b>
    </p>
    
    <p>
      Contrast:
      <input type="range" min={0} max={300} step={10} bind:value={contrast} />
      <b>{contrast}%</b>
    </p>
    
    <p>
      Grayscale:
      <input type="range" min={0} max={100} step={5} bind:value={grayscale} />
      <b>{grayscale}%</b>
    </p>

    <p>
      Hue:
      <input type="range" min={-365} max={365} step={1} bind:value={hue} />
      <b>{hue}deg</b>
    </p>

    <p>
      Invert Colors:
      <input type="range" min={0} max={100} step={10} bind:value={invert} />
      <b>{invert}%</b>
    </p>
  </div>

</main>
