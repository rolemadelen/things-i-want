<script>
  import { hoverMode } from './store.js'

  let isRectangle = false;

  function handleClick(e) {
    isRectangle = !isRectangle
    hoverMode.update(mode => !mode)
  }

</script>

<div class='hoverModeToggle' on:mouseover on:mouseleave class:rectangle={isRectangle} on:click={handleClick}></div>

<style>
  @media (min-width: 900px) {
    .hoverModeToggle {
      position: fixed;
      bottom: 1rem;
      right: 1rem;
      border-radius: 2px;
      border: 1px solid #111;
      width: 25px;
      height: 25px;
      backdrop-filter: blur(5px);
      transition: all 0.5s ease-in-out;
    }

    .hoverModeToggle:hover {
      cursor: pointer;
      background-color: #111;
    }

    .rectangle {
      border-radius: 50px;
      transform: rotate(45deg);
    }
  }
</style>
