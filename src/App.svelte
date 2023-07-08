<script>
  import Navigation from './Navigation.svelte'
  import Header from './Header.svelte'
  import { category } from './store.js'
  import { onDestroy } from 'svelte'
  import { fly } from 'svelte/transition'

  const items = [
    {
      title: 'Apple Pro Display XDR | Nano-texture glass',
      cost: '5,999.00',
      src: '/assets/apple-pro-display-xdr.png',
      tags: ['monitor', 'display']
    },
    {
      title: 'Nagado Daiko',
      cost: '926.75',
      src: '/assets/nagado-daiko.png',
      tags: ['taiko']
    },
    {
      title: 'Azio Cascade Slim',
      cost: '99.99',
      src: '/assets/azio-cascade-slim.png',
      tags: ['keyboard']
    },
    {
      title: 'Atomph Window 2',
      cost: '499.00',
      src: '/assets/atmoph-window-2.png',
      tags: ['electronic', 'display']
    }, 
    {
      title: 'Bolt Jime Shime Daiko',
      cost: '1,081.21',
      src: '/assets/bolt-jime-shime-daiko.png',
      tags: ['taiko']
    },
    {
      title: 'Ergodox EZ',
      cost: '295.00',
      src: '/assets/ergodox-ez.png',
      tags: ['keyboard']
    },
    {
      title: 'Flexispot EC1 Standing Desk',
      cost: '239.00',
      src: '/assets/flexispot-ec1.png',
      tags: ['electronic', 'desk']
    },
    {
      title: 'Kensington iPad Docking',
      cost: '199.99',
      src: '/assets/kensington-ipad-docking.png',
      tags: ['electronic']
    },
    {
      title: 'Keychron Q8',
      cost: '195.00',
      src: '/assets/keychron-q8.png',
      tags: ['keyboard']
    }, 
    {
      title: 'Kinesis Advantage 2',
      cost: '1,484.99',
      src: '/assets/kinesis-advantage-2.png',
      tags: ['keyboard']
    },
    {
      title: 'Lukcy Cat Artisan Keycap',
      cost: '59.00',
      src: '/assets/lucky-cat-artisan-keycap.png',
      tags: ['keycap']
    },
    {
      title: 'Rayneo XR Glasses',
      cost: '399.00',
      src: '/assets/rayneo-xr-glasses.png',
      tags: ['electronic']
    },
    {
      title: 'ROLAND Taiko-1',
      cost: '1,499.00',
      src: '/assets/roland-taiko-1.png',
      tags: ['electronic', 'taiko']
    },
    {
      title: 'Ultimate Hacking Keyboard',
      cost: '320.00',
      src: '/assets/ultimate-hacking-keyboard.png',
      tags: ['keyboard']
    }
  ]

  let categoryItems = [];

  const unsubscribe = category.subscribe(text => {
    if(text === 'all') categoryItems = items;
    else {
      categoryItems = [];
      items.map(item => {
        if(item.tags.includes(text)) {
          categoryItems = [...categoryItems, item];
        }
      })
    }
  })

  onDestroy(unsubscribe);
</script>

<main>
  <Header />
  <Navigation items={items} />
  <div class='grid'>
    {#each categoryItems as item}
      <div transition:fly={{y: 200, duration: 250}} class='grid-item'>
        <img src={item.src} alt={item.title} />
        <div class="item-info">
          <div class='item-name'>{item.title}</div>
          <div class='item-cost'>${item.cost}</div>
        </div>
      </div>
    {/each}
  </div>
</main>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-auto-rows: 500px;
    box-sizing: border-box;
  }
  
  .grid-item {
    position: relative;
    border: 1px solid #eee;

    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.2s ease-in-out;
  }

  .grid-item img {
    width: 300px;
    height: auto;
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
  
  @media(min-width: 900px) {
    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      grid-auto-rows: 500px;
    }

    .item-info {
      color: white;
    }

    .grid-item:hover {
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
