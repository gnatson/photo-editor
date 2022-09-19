<script>
  const unsplash = {
    photoId: 'photo-1514888286974-6c03e2ca1dba',
    fit: 'crop',
    width: 1143,
    quality: 80,
  }

  let photo = `https://images.unsplash.com/${unsplash.photoId}?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=${unsplash.fit}&w=${unsplash.width}&q=${unsplash.quality}`

  let blur = 0
  let contrast = 100
  let brightness = 100
  let saturate = 100
  let grayscale = 0
  let opacity = 100
  let sepia = 0
  let hue = 0
  let invert = 0

  let clipSplitPx = 150

  $: background = `background-image: url('${photo}');`

  $: style =
    background +
    `filter: blur(${blur}px) contrast(${contrast}%) brightness(${brightness}%) saturate(${saturate}%) grayscale(${grayscale}%) opacity(${opacity}%) sepia(${sepia}%) hue-rotate(${hue}deg) invert(${invert}%);`
  // drop-shadow(16px 16px 20px black)

  $: clip = `clip: rect(0px, ${clipSplitPx}px, 300px, 0px);`
</script>

<style>
  main {
    user-select: none;
  }

  #properties {
    position: absolute;
    background-color: rgba(0, 0, 0, 0.367);
    color: white;
    z-index: 2;
  }

  .photo {
    /* transition: 0.1s; */
    z-index: 1;

    position: absolute;
    top: 0px;
    right: 0px;

    width: 100%;
    height: 100%;

    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    /* background-origin: center; */
  }

  .photo#splitRight {
    z-index: 2;
    /* transform: translateX(-50%); */
    background-position: center;
    background-size: cover;
  }

  #timeline {
    position: fixed;
    bottom: 0px;
    z-index: 2;
  }
</style>

<main>
  <div class="photo" {style} />
  <div class="photo" id="splitRight" style={background + clip} />

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

    <p>
      clipSplitPx
      <input type="range" min={0} max={300} step={1} bind:value={clipSplitPx} />
    </p>

  </div>

  <div id="timeline">--[edit.1]--->[edit.2]--></div>
</main>
