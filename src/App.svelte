<script>
  // todo: construct custom filter
  // animated transitions with svelte/easing... (bounce effect)
  //  user preferences? (ex. slider step)
  // animated preview
  // split view

  let photo = 'photos/geran-de-klerk-bKhETeDV1WM-unsplash.jpg'

  let blur = 0
  let contrast = 100
  let brightness = 100
  let saturate = 100
  let grayscale = 0
  let opacity = 100
  let sepia = 0
  let hue = 0
  let invert = 0

  $: style = `filter: blur(${blur}px) contrast(${contrast}%) brightness(${brightness}%) saturate(${saturate}%) grayscale(${grayscale}%) opacity(${opacity}%) sepia(${sepia}%) hue-rotate(${hue}deg) drop-shadow(16px 16px 20px black) invert(${invert}%);`
</script>

<style>
  main {
    user-select: none;
  }

  img {
    transition: 0.5s;
    z-index: 1;
  }

  #properties {
    z-index: 2;
  }
</style>

<main>
  <div id="photo">
    <img src={photo} alt="" {style} />
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
      Brightness:
      <input type="range" min={0} max={300} step={10} bind:value={brightness} />
      <b>{brightness}%</b>
    </p>

    <p>
      Saturate:
      <input type="range" min={0} max={300} step={10} bind:value={saturate} />
      <b>{saturate}%</b>
    </p>

    <p>
      Grayscale:
      <input type="range" min={0} max={100} step={5} bind:value={grayscale} />
      <b>{grayscale}%</b>
    </p>

    <p>
      Opacity:
      <input type="range" min={0} max={100} step={5} bind:value={opacity} />
      <b>{opacity}%</b>
    </p>

    <p>
      Sepia:
      <input type="range" min={0} max={100} step={5} bind:value={sepia} />
      <b>{sepia}%</b>
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
