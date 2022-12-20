<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
</script>

<h1>juhuuu</h1>
<button on:click={() => dispatch("reset")}>reset</button>
<div>
  <video autoplay><source src="/cool.mp4" type="video/mp4" /></video>
</div>

<style>
  div {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    z-index: -1;
  }
  video {
    min-width: 100%;
  }
</style>
