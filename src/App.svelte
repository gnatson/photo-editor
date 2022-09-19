<script>
  // todo: construct custom filter
  // animated transitions with svelte/easing... (bounce effect)
  //  user preferences? (ex. slider step)

  const sample_filters = []
  sample_filters.push('filter: drop-shadow(16px 16px 20px red) invert(75%);')

  let blur = 0
  let contrast = 100
  let grayscale = 0
  let hue = 0

  $: style = `filter: blur(${blur}px) contrast(${contrast}%) grayscale(${grayscale}%) hue-rotate(${hue}deg);`
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
  </div>

</main>
