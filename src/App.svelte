<script>
  let blur = 0
  let contrast = 100
  let brightness = 100
  let saturate = 100
  let grayscale = 0
  let opacity = 100
  let sepia = 0
  let hue = 0
  let invert = 0

  let clipSplitPx = 50

  let timeline = []

  const timelineSaveState = () => {
    // const timestamp =
    const state = {
      blur,
      contrast,
      brightness,
      saturate,
      grayscale,
      opacity,
      sepia,
      hue,
      invert,
    }
    timeline.push(state)
    timeline = timeline
  }

  const unsplash = {
    photoId: 'photo-1514888286974-6c03e2ca1dba',
    fit: 'crop',
    width: 1143,
    quality: 80,
  }

  let photo = `https://images.unsplash.com/${unsplash.photoId}?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=${unsplash.fit}&w=${unsplash.width}&q=${unsplash.quality}`

  let splitTextPosition = { x: 0, y: 0 }

  const filtersToCSS = (state) => {
    const {
      blur,
      contrast,
      brightness,
      saturate,
      grayscale,
      opacity,
      sepia,
      hue,
      invert,
    } = state
    return `filter: blur(${blur}px) contrast(${contrast}%) brightness(${brightness}%) saturate(${saturate}%) grayscale(${grayscale}%) opacity(${opacity}%) sepia(${sepia}%) hue-rotate(${hue}deg) invert(${invert}%);`
  }

  $: background = `background-image: url('${photo}');`

  $: style =
    background +
    `filter: blur(${blur}px) contrast(${contrast}%) brightness(${brightness}%) saturate(${saturate}%) grayscale(${grayscale}%) opacity(${opacity}%) sepia(${sepia}%) hue-rotate(${hue}deg) invert(${invert}%);`
  // drop-shadow(16px 16px 20px black)

  $: clip = `clip: rect(0px, ${window.innerWidth * (clipSplitPx / 100)}px, ${
    window.innerHeight
  }px, 0px);`

  const mousedown = (e) => {}

  const mousemove = (e) => {
    const percent = +((e.clientX / window.innerWidth) * 100).toFixed(0)
    clipSplitPx = percent

    splitTextPosition = { x: e.clientX, y: e.clientY }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

  main {
    font-family: 'Poppins', sans-serif;
    user-select: none;
    overflow: hidden;
    padding: 0;
    margin: 0;
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

    /* transform: scale(1.2); */
    /* background-origin: center; */
    /* transform: rotate(5deg); */
  }

  .text {
    position: fixed;
    top: 0px;
    left: 0px;
    color: rgba(0, 0, 0, 0.2);
    font-size: 3rem;
    z-index: 3;
    pointer-events: none;
    padding: 2rem;
  }

  .original.text {
    transform: translateX(-100%) translateY(-50%);
  }

  .altered.text {
    transform: translateY(-50%);
  }

  .photo#splitRight {
    z-index: 2;
    /* transform: translateX(-50%); */
    background-position: center;
    background-size: cover;
    pointer-events: none;
  }

  #timeline {
    position: fixed;
    bottom: 0px;
    left: 0px;
    z-index: 2;
    text-align: center;

    width: 100vw;

    display: flex;
    flex-wrap: wrap;

    background-color: rgba(255, 255, 255, 0.3);
  }

  #timeline > .state {
    width: 80px;
    height: 80px;

    background-image: url();
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;

    display: flex;
    justify-content: center;
    align-items: center;

    opacity: 1;
    margin: 0.3rem;
  }
</style>

<main>
  <div
    class="photo"
    {style}
    on:mousedown={mousedown}
    on:mousemove={mousemove} />
  <div class="photo original" id="splitRight" style={background + clip} />

  <div
    class="original text"
    style="left: {splitTextPosition.x}px; top:{splitTextPosition.y}px;">
    Original
  </div>
  <div
    class="altered text"
    style="left: {splitTextPosition.x}px; top:{splitTextPosition.y}px;">
    Altered
  </div>

  <div id="properties">
    <p>
      Blur:
      <input
        type="range"
        min={0}
        max={5}
        step={1}
        bind:value={blur}
        on:change={timelineSaveState} />
      <b>{blur}px</b>
    </p>

    <p>
      Contrast:
      <input
        type="range"
        min={0}
        max={300}
        step={10}
        bind:value={contrast}
        on:change={timelineSaveState} />
      <b>{contrast}%</b>
    </p>

    <p>
      Brightness:
      <input
        type="range"
        min={0}
        max={300}
        step={10}
        bind:value={brightness}
        on:change={timelineSaveState} />
      <b>{brightness}%</b>
    </p>

    <p>
      Saturate:
      <input
        type="range"
        min={0}
        max={300}
        step={10}
        bind:value={saturate}
        on:change={timelineSaveState} />
      <b>{saturate}%</b>
    </p>

    <p>
      Grayscale:
      <input
        type="range"
        min={0}
        max={100}
        step={5}
        bind:value={grayscale}
        on:change={timelineSaveState} />
      <b>{grayscale}%</b>
    </p>

    <p>
      Opacity:
      <input
        type="range"
        min={0}
        max={100}
        step={5}
        bind:value={opacity}
        on:change={timelineSaveState} />
      <b>{opacity}%</b>
    </p>

    <p>
      Sepia:
      <input
        type="range"
        min={0}
        max={100}
        step={5}
        bind:value={sepia}
        on:change={timelineSaveState} />
      <b>{sepia}%</b>
    </p>

    <p>
      Hue:
      <input
        type="range"
        min={-365}
        max={365}
        step={1}
        bind:value={hue}
        on:change={timelineSaveState} />
      <b>{hue}deg</b>
    </p>

    <p>
      Invert Colors:
      <input
        type="range"
        min={0}
        max={100}
        step={10}
        bind:value={invert}
        on:change={timelineSaveState} />
      <b>{invert}%</b>
    </p>
  </div>

  <div id="timeline">
    {#each timeline as state, id}
      <div
        class="state"
        style={`background-image: url(${photo});` + filtersToCSS(state)}>
        👉
      </div>
    {/each}
  </div>
</main>
