<script>
  import { onMount } from 'svelte'
  import { category } from './store.js'
  export let items
  let tags = ['all']

  onMount(() => {
    items.map(item => {
      item.tags.map(it => {
        if(!tags.includes(it))
        tags = [...tags, it]
      })
    })
  })

  function handleClick(e) {
    category.update(text => text = e.currentTarget.innerText.split('\n')[1])
    document.querySelector('nav .active')?.classList.remove('active')
    e.currentTarget.classList.add('active')
  }
</script>

<nav>
  {#each tags as tag, i}
    {#if i === 0}
      <div class='nav-item active' on:click={handleClick}><span class='tag'>#</span>{tag}</div>
    {:else}
      <div class='nav-item' on:click={handleClick}><span class='tag'>#</span>{tag}</div>
    {/if}
  {/each}
</nav>

<style>
nav {
  width: 100vw;
  overflow-x: scroll;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(125px, 1fr));
  grid-auto-columns: minmax(125px, 1fr);
  box-sizing: border-box;
}

.nav-item {
  padding: 1rem 0;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #eee;
  text-transform: lowercase;
  color: #777;
}

.nav-item:hover {
  background-color: #111;
  color: #eee;
  transition: all 0.2s ease-in-out;
}

.nav-item:hover .tag {
  color: #6b96ff;
  transition: all 0.2s ease-in-out;
}

.nav-item.active {
  background-color: #111;
  border-color: #111;
  color: #eee;
}

.nav-item.active .tag {
  color: #6b96ff;
}

.tag {
  font-weight: bold;
  margin-right: 1px;
}

  @media(min-width: 900px) {
    nav {
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      grid-auto-columns: minmax(250px, 1fr);
    }
  }

  @media(min-width: 1200px) {
    nav {
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      grid-auto-columns: minmax(200px, 1fr);
    }
  }

</style>
