<script>
  // todo: construct custom filter
  // animated transitions with svelte/easing... (bounce effect)
  //  user preferences? (ex. slider step)

  const sample_filters = []
  sample_filters.push('filter: blur(5px);')
  sample_filters.push('filter: contrast(200%);')
  sample_filters.push('filter: grayscale(80%);')
  sample_filters.push('filter: hue-rotate(90deg);')
  sample_filters.push('filter: hue-rotate(90deg);')
  sample_filters.push('filter: drop-shadow(16px 16px 20px red) invert(75%);')

  let blur = 0
  let contrast = 100

  $: style = `filter: blur(${blur}px) contrast(${contrast}%);`
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
  </div>

</main>
