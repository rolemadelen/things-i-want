<script>
  import { supabase } from './supabaseClient';
  import { onMount } from 'svelte';

  let itemList = [];
  let content;
  let clientHeight = 1;

  onMount(() => {
    fetchItems().then(res => itemList = Array.from(res));
    clientHeight = document.body.clientHeight;
  })

  async function fetchItems() {
    const { data, error } = await supabase
      .from('Item')
      .select('id, title, img_src, bg_color, cost')
      .order('title');

    if(error) {
      console.error('error')
    } else {
      return data;
    }
  }

  const handleScroll = (e) => {
    let itemPosition = Math.round(content.scrollTop / clientHeight) + 1;
    const prev = document.querySelector(`[data-id="${itemPosition - 1}"]`);
    const curr = document.querySelector(`[data-id="${itemPosition}"]`);
    const next = document.querySelector(`[data-id="${itemPosition + 1}"]`);

    document.querySelector('.main').style.backgroundColor = `${itemList[itemPosition-1].bg_color}`;

    if(itemPosition == 1) {
      curr.classList.add('active');
      next.classList.remove('active');
    } else if(itemPosition > 1 && itemPosition < itemList.length) {
      prev.classList.remove('active');
      curr.classList.add('active');
      next.classList.remove('active');
    } else if(itemPosition === itemList.length){
      prev.classList.remove('active');
      curr.classList.add('active');
    }
  }

  const displayCost = (cost) => {
    return cost.toLocaleString('en-us');
  }
</script>

<main>
  <header>
    <div class='logo'>Things I Want</div>
  </header>
  <div class='main' bind:this={content} on:scroll={handleScroll}>
    {#each itemList as item, i}
      <div class='fullscreen item' id={i+1}>
        <img src="{item.img_src}" alt={item.title}/>
        <div class='cost'>${displayCost(item.cost)}</div>
      </div>
    {/each}
  </div>
  <footer>
      <div class="contact"><a href='mailto:hello@jiieu.com'>hello@jiieu.com</a></div>
      <div class="copyright">@ 2023 Jii Eu</div>
  </footer>
  <nav>
    <ul>
      {#each itemList as item, i}
        <a data-id={i+1} href="#{i+1}"><li>{item.title}</li></a>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .main {
    z-index: -100;
    height: 100vh;
    overflow: auto;
    scroll-behavior: smooth;
    scroll-snap-type: y mandatory;
    transition: background-color 0.3s ease-in-out;
  }

  .item {
    scroll-snap-align: start;
    position: relative;
  }

  header {
    position: fixed;
    left: 10px;
    top: 20px;
    width: 100%;
    font-size: 2rem;
  }

  .logo {
    margin-left: 15px;
    text-transform: uppercase;
    font-weight: 600;
  }

  footer {
    position: fixed;
    bottom: 20px;
    left: 10px;
    width: clamp(200px, 40vw, 320px);
    margin-left: 15px;
    line-height: 1.35;
  }

  .contact,
  .copyright {
    font-size: 0.8rem;
    font-weight: light;
    margin: 0.25rem auto;
  }

  nav {
    position: fixed;
    right: 15px;
    bottom: 20px;
    font-size: 1rem;
    font-weight: 500;
    margin-right: 15px;
  }

  nav li {
    margin-bottom: 0.5rem;
  }

  nav li:hover {
    text-decoration: underline;
  }

  img {
    width: 100%;
    transition: all 0.2s ease-in-out;
  }

  img:hover {
    transform: scale(1.1);
  }

  .fullscreen {
    min-width: 400px;
    max-width: 35vw;
    margin: 0 auto;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .cost {
    position: absolute;
    left: -70%;
    font-size: 5rem;
    font-weight: bold;
    opacity: 0.25;
  }

  a {
    color: inherit;
    text-decoration: none;
  }

  footer a {
    text-decoration: underline;
  }

  li {
    list-style: none;
  }

  :global(.active) {
    color: #4949CF !important;
    font-weight: bold;
    transition: all 0.1s ease-in-out;
  }

  :global(.active::before) {
    content: "⇢";
    position: absolute;
    left: -1.5rem;
  }


</style>
