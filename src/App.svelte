<script>
  import Properties from './Components/Properties.svelte'

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

  let showTextOriginalAltered = false

  const timelineSaveState = () => {
    // const timestamp =
    const MEMORY_LIMIT = 5

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

    if (timeline.length > MEMORY_LIMIT) {
      // timeline = timeline.slice(0, MEMORY_LIMIT)
      timeline.shift()
    }
    timeline = timeline
  }

  const recoverState = (savedState) => {
    ;({
      blur,
      contrast,
      brightness,
      saturate,
      grayscale,
      opacity,
      sepia,
      hue,
      invert,
    } = savedState)
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

  const mouseenter = () => {
    showTextOriginalAltered = true
  }

  const mousemove = (e) => {
    const percent = +((e.clientX / window.innerWidth) * 100).toFixed(0)
    clipSplitPx = percent

    splitTextPosition = { x: e.clientX, y: e.clientY }
  }

  const mouseleave = () => {
    showTextOriginalAltered = false
    clipSplitPx = 0
  }

  const UI = { showMenu: true, showTimeline: true, showProperties: true }

  const windowMouseMove = (e) => {
    const mouseOnRigthHalfOfWindow = e.clientX > window.innerWidth / 2
    const mouseOnBottomHalfOfWindow = e.clientY > window.innerHeight / 2

    UI.showProperties = mouseOnRigthHalfOfWindow
    UI.showMenu = !mouseOnRigthHalfOfWindow
    UI.showTimeline = mouseOnBottomHalfOfWindow
  }

  const windowMouseLeave = () => {
    // UI.showMenu = false
    // UI.showProperties = false
    // UI.showTimeline = false
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

  #menu {
    position: absolute;
    top: 0px;
    left: 0px;

    background-color: rgba(0, 0, 0, 0.2);
    color: white;
    z-index: 2;
    padding: 2rem;
    margin: 1rem;
    border-top: 0.5rem solid white;
    border-radius: 5px;

    animation: 0.3s scaleUp;
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
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;

    /* background-color: rgba(255, 255, 255, 0.3); */
    background: transparent;
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

    transition: 0.3s;

    animation: 0.3s scaleUp;

    border-radius: 5px;
  }

  #timeline > .state:hover {
    transform: translateY(-10px);
  }

  @keyframes scaleUp {
    from {
      transform: scale(0.5);
    }
  }
</style>

<svelte:window on:mousemove={windowMouseMove} on:mouseout={windowMouseLeave} />

<main>
  <div
    class="photo"
    {style}
    on:mouseenter={mouseenter}
    on:mouseleave={mouseleave}
    on:mousemove={mousemove} />
  <div class="photo original" id="splitRight" style={background + clip} />

  {#if showTextOriginalAltered}
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
  {/if}

  {#if UI.showProperties}
    <Properties
      bind:blur
      bind:contrast
      bind:brightness
      bind:saturate
      bind:grayscale
      bind:opacity
      bind:sepia
      bind:hue
      bind:invert
      {timelineSaveState} />
  {/if}

  {#if UI.showTimeline}
    <div id="timeline">
      {#each timeline as state, id}
        <div
          on:click={() => recoverState(state)}
          class="state"
          style={`background-image: url(${photo});` + filtersToCSS(state)} />
      {/each}
    </div>
  {/if}

  {#if UI.showMenu}
    <div id="menu">
      <button>upload</button>
    </div>
  {/if}
</main>
