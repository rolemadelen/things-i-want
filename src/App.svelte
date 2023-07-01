<script>
  import { onMount } from 'svelte';

  const numberOfitems = 8;
  let content;
  let lastScrollTop;
  let offsetY;
  let offset = 0;

  $: {
    console.log(`lastScrollTop: ${lastScrollTop}`)
    console.log(`${offset}    ${Math.floor(offset)}    ${Math.ceil(offset)}`);
  }
  onMount(() => {
    offsetY = document.body.offsetHeight;
  })

  const items = [
    {
      title: 'Azio Cascade Slim',
      img: '/src/assets/azio-cascade-slim.png'
    },
    {
      title: 'Keychron Q8',
      img: '/src/assets/keychron-q8.png'
    },
    {
      title: 'Kinesis Advantage 2',
      img: '/src/assets/kinesis-advantage-2.png'
    },
    {
      title: 'Ergodox EZ',
      img: '/src/assets/ergodox-ez.png'
    },
    {
      title: 'Nagado Daiko',
      img: '/src/assets/nagado-daiko.png'
    },
    {
      title: 'ROLAND (Taiko-1)',
      img: '/src/assets/roland-taiko-1.png'
    },
    {
      title: 'Rayneo XR Glasses',
      img: '/src/assets/rayneo-xr-glasses.png'
    },
    {
      title: 'Apple Pro Display XDR',
      img: '/src/assets/apple-pro-display-xdr.png'

    },
    {
      title: 'Atmoph Window 2',
      img: '/src/assets/atmoph-window-2.png'
    },
  ];

  const handleScroll = () => {
    offset = numberOfitems - (lastScrollTop / offsetY);
    const main = document.querySelector('.main');

    if(offset > 7.5) {
      main.style.backgroundColor = '#5ca288';
    } else if (offset > 6.5) {
      main.style.backgroundColor = '#819cb5';
    } else if (offset > 5.5) {
      main.style.backgroundColor = '#75bdeb';
   } else if (offset > 4.5) {
      main.style.backgroundColor = '#fff';
    } else if (offset > 3.5) {
      main.style.backgroundColor = '#b64b319e';
    } else if (offset > 2.5) {
      main.style.backgroundColor = '#b865ff9e';
    } else if (offset > 1.5) {
      main.style.backgroundColor = '#fff';
    } else {
      main.style.backgroundColor = '#fff';
    }

    lastScrollTop = content.scrollTop;
  }

</script>

<main>
  <header>
    <div class='logo'>Things I Want</div>
  </header>
  <div class='main' bind:this={content} on:scroll={handleScroll}>
    {#each items as item, i}
      <div class='fullscreen item' id={i+1}>
        <img src="{item.img}"/>
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
      {#each items as item, i}
        <a data-id={i+1} href="#{i+1}"><li>{item.title}</li></a>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .main {
    background-color: #5ca288;
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
    width: 320px;
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
    width: 50%;
    min-width: 400px;
  }

  .fullscreen {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
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
