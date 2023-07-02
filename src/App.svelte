<script>
  import { supabase } from '/src/supabaseClient';
  import { onMount } from 'svelte';

  let itemList = [];

  onMount(() => {
    fetchItems().then(res => itemList = Array.from(res));
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

</script>

<main>
  <header>
    <div class='logo'>Things I Want</div>
  </header>
  <div class='main'>
    {#each itemList as item}
      <div class='fullscreen item' id={item.id}>
        <img src="{item.img_src}"/>
        <div class='cost'>${item.cost}</div>
      </div>
    {/each}
  </div>
  <footer>
      <div class='description'>
      Welcome to my curated collection of Things I Want. 
      Whether it's an item that satisfies my intellectual curiosity or a cherished dream 
      I've nurtured for years, each selection holds a special place in this collection.
    </div>
      <div class="contact"><a href='mailto:hello@jiieu.com'>hello@jiieu.com</a></div>
      <div class="copyright">@ 2023 Jii Eu</div>
  </footer>
  <nav>
    <ul>
      {#each itemList as item}
        <a data-id={item.id} href="#{item.id}"><li>{item.title}</li></a>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .main {
    z-index: -1;
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
    left: 0;
    width: clamp(200px, 40vw, 320px);
    margin-left: 15px;
    line-height: 1.35;
  }

  .description {
    font-size: 1.1rem;
    font-weight: 500;
    margin-bottom: 0.5rem;
  }

  .contact,
  .copyright {
    font-size: 0.8rem;
    font-weight: light;
    margin: 0.25rem auto;
  }

  .privacy-policy {
    font-size: 1.1rem;
    font-weight: 600;
    margin-top: 2rem;
  }

  nav {
    position: fixed;
    right: 0;
    bottom: 20px;
    font-size: 1.1rem;
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

  .active {
    font-weight: bold;
  }

</style>
