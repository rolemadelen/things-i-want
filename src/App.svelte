<script>
  import Navigation from './Navigation.svelte'
  import Header from './Header.svelte'
  import Image from './Image.svelte'
  import HoverMode from './HoverMode.svelte'
  import { category, hoverMode } from './store.js'
  import { onMount, onDestroy } from 'svelte'
  import { fly } from 'svelte/transition'
  import { cubicOut } from 'svelte/easing'
  import { supabase } from './supabaseClient'
  import { flip } from 'svelte/animate'

  let itemList = [];
  let hoverModeToggle = true;
  let categoryItems = []
  let publicURL = new WeakMap();
  let mouse = {x:0, y:0};

  $: categoryItems = itemList
  $: {
    if(hoverModeToggle) {
      const elems = document.querySelectorAll('.grid-item')
      elems.forEach(elem => {
        elem.classList.add('hover-mode')
      })
    } else {
      const elems = document.querySelectorAll('.grid-item')
      elems.forEach(elem => {
        elem.classList.remove('hover-mode')
      })
    }
  }

  onMount(() => {
    fetchItems() 
    .then(data => {
      itemList = data
      fetchImages(data)
    })
  })

  function fetchImages(items) {
    items.map((item) => {
      const { data } = supabase 
      .storage 
      .from('images')
      .getPublicUrl(item.filename)
      publicURL[item.title] = data.publicUrl
    })
  }

  async function fetchItems() {
    const { data, error } = await supabase 
    .from('Item') 
    .select('id, title, filename, cost, link, tags')
    .order('id')

    if(error) {
      console.error('error fetching images')
    } else { 
      return data
    }
  }

  const unsubscribe = category.subscribe(text => {
    if(text === 'all') {
      categoryItems = itemList
    }
    else {
      categoryItems = itemList.filter(item => item.tags.includes(text))
    }
  })

  const unsubscribe2 = hoverMode.subscribe(mode => {
    hoverModeToggle = mode
  })

  onDestroy(unsubscribe)
  onDestroy(unsubscribe2)

  const handleMouseMove = (e) => {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
    document.querySelector('.cursor').style.top = `${mouse.y-10}px`;
    document.querySelector('.cursor').style.left = `${mouse.x-10}px`;
  }
</script>

<main on:mousemove={handleMouseMove}>
  <div class='cursor'></div>
  <Header />
  {#if itemList.length > 0}
    <Navigation items={itemList} />
  {/if}
  <div class='grid'>
    {#each categoryItems as item (item.title)}
      <div animate:flip={{duration: 500, easing: cubicOut}} class='grid-item' class:hover-mode={hoverModeToggle}>
        {#if Object.keys(publicURL).length > 0}
          <Image src={publicURL[item.title]} alt={item.title} />
        {/if}
        <div class="item-info">
          <div class='item-name'>{item.title}</div>
          <div class='item-cost'>${item.cost}</div>
        </div>
        <a href={item.link} target="_blank" rel="noopener noreferrer">
          <div class="link-arrow" />
        </a>
      </div>
    {/each}
  </div>
  <HoverMode />
</main>

<style>
  main {
    width: fit-content;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-auto-rows: 500px;
    box-sizing: border-box;
  }
  
  .grid-item {
    position: relative;
    border: 1px solid #eee;
    width: 100vw;

    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.2s ease-in-out;
  }

  .item-info {
    position: absolute;
    bottom: 16px;
    left: 16px;
    font-size: 14px;
    color: #333;
  }

  .item-cost {
    font-weight: bold;
  }

  .link-arrow {
    background-image: url('/arrow-black.svg');
    background-size: cover;
    background-repeat: no-repeat;
    position: absolute;
    margin: 0.5rem 0.5rem 0 0;
    top: 3px;
    right: 3px;
    width: 0.8rem;
    height: 0.8rem;
    transition: all 0.2s ease-in-out;
  }

  .link-arrow:hover {
    top: 0px;
    right: 0px;
  }

  .cursor {
    position: fixed;
    top:-10rem;
    left:-10rem;
    width: 18px;
    height: 18px;
    background-color: #000000ccc;
    border-radius: 9999px;
    backdrop-filter: invert(1);
    pointer-events: none;
    z-index: 9999;
    transition: top 0.2s linear, left 0.2s linear;
  }

  @media(min-width: 500px) {
    .grid-item {
      width: auto;
    }
  }
  @media(min-width: 900px) {
    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      grid-auto-rows: 500px;
    }

    .hover-mode .link-arrow {
      background-image: url('/arrow.svg');
      width: 1rem;
      height: 1rem;
    }

    .hover-mode .item-info {
      color: white;
    }

    .hover-mode:hover {
      background-color: #111;
      transition: all 0.2s ease-in-out;
    }
  }

  @media(min-width: 1200px) {
    .grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media(min-width: 1920px) {
    .grid {
      grid-template-columns: repeat(4, 1fr);
    }
  }
</style>
