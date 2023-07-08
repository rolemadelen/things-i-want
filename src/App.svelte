<script>
  import Navigation from './Navigation.svelte'
  import Header from './Header.svelte'
  import Image from './Image.svelte'
  import { category } from './store.js'
  import { onDestroy } from 'svelte'
  import { fly } from 'svelte/transition'

  const items = [
    {
      title: 'Apple Pro Display XDR | Nano-texture glass',
      cost: '5,999.00',
      src: '/assets/apple-pro-display-xdr.png',
      link: 'https://www.apple.com/shop/buy-mac/pro-display-xdr',
      tags: ['monitor', 'electronic']
    },
    {
      title: '14-inch MacBook Pro | M2 Max, 64GB, 1TB SSD',
      cost: '3,099.00',
      src: '/assets/macbook-pro-14inch.png',
      link: 'https://www.apple.com/shop/buy-mac/macbook-pro/14-inch-space-gray-apple-m2-max-with-12-core-cpu-and-30-core-gpu-1tb',
      tags: ['electronic', 'laptop']
    },
    {
      title: '12.9-inch iPad Pro Wi-Fi 512GB + Apple Pencil',
      cost: '1,528.00',
      src: '/assets/ipad-pro-12-9-inch.png',
      link: 'https://www.apple.com/shop/buy-ipad/ipad-pro/12.9-inch-display-512gb-space-gray-wifi',
      tags: ['electronic', 'tablet']
    },
    {
      title: 'Nagado Daiko',
      cost: '894.01',
      src: '/assets/nagado-daiko.png',
      link: "https://taiko-shop.com/products/nagado-daiko-smile-brown?variant=32251795046471",
      tags: ['taiko']
    },
    {
      title: 'Azio Cascade Slim',
      cost: '99.99',
      src: '/assets/azio-cascade-slim.png',
      link: 'https://www.aziocorp.com/collections/keyboard/products/cascade-slim-75-wireless-hot-swappable-keyboard',
      tags: ['keyboard']
    },
    {
      title: 'Atomph Window 2',
      cost: '499.00',
      src: '/assets/atmoph-window-2.png',
      link: 'https://store.atmoph.com/en/collections/atmoph-window-2/products/atmoph-window-2-basic-1?variant=21032164491318',
      tags: ['electronic']
    }, 
    {
      title: 'Bolt Jime Shime Daiko',
      cost: '1,081.21',
      src: '/assets/bolt-jime-shime-daiko.png',
      link: "https://taiko-shop.com/collections/shime-daiko-taiko-drum/products/bamboo-bolt-jime-shime-daiko-namitsuke",
      tags: ['taiko']
    },
    {
      title: 'Ergodox EZ',
      cost: '354.00',
      src: '/assets/ergodox-ez.png',
      link: 'https://ergodox-ez.com/buy',
      tags: ['keyboard']
    },
    {
      title: 'Flexispot EC1 Standing Desk',
      cost: '239.00',
      src: '/assets/flexispot-ec1.png',
      link: 'https://www.amazon.com/Flexispot-Electric-Workstation-Whole-Piece-Adjustable/dp/B0851BF95W/ref=sr_1_1_sspa?keywords=flexispot+standing+desk&qid=1688845372&sprefix=flexispot+stand%2Caps%2C126&sr=8-1-spons&ufe=app_do%3Aamzn1.fos.f5122f16-c3e8-4386-bf32-63e904010ad0&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1',
      tags: ['electronic', 'desk']
    },
    {
      title: 'Kensington iPad Docking',
      cost: '199.99',
      src: '/assets/kensington-ipad-docking.png',
      link: 'https://store.kensington.com/collections/studiodock/products/studiodock%E2%84%A2-ipad-docking-station-ipad-pro-12-9-2021',
      tags: ['electronic']
    },
    {
      title: 'Keychron Q8',
      cost: '195.00',
      src: '/assets/keychron-q8.png',
      link: 'https://www.keychron.com/products/keychron-q8-alice-layout-qmk-custom-mechanical-keyboard',
      tags: ['keyboard']
    }, 
    {
      title: 'Kinesis Advantage 2',
      cost: '369.99',
      src: '/assets/kinesis-advantage-2.png',
      link: 'https://kinesis-ergo.com/shop/advantage2/',
      tags: ['keyboard']
    },
    {
      title: 'Lukcy Cat Artisan Keycap',
      cost: '59.00',
      src: '/assets/lucky-cat-artisan-keycap.png',
      link: 'https://www.etsy.com/listing/1217142330/lucky-cat-artisan-keycap-for-cherry-mx?ref=listing_page_ad_row-5&plkey=bdf26c910c03b84270405cbd29546e72b94b0641%3A1217142330&listing_id=1217142330&listing_slug=lucky-cat-artisan-keycap-for-cherry-mx',
      tags: ['keycap']
    },
    {
      title: 'Kaonashi Artisan Keycap',
      cost: '39.00',
      src: '/assets/kaonashi-artisan-keycap.webp',
      link: 'https://www.etsy.com/listing/1440589845/spirited-away-no-face-artisan-keycap-for?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=artisan+keycaps&ref=sr_gallery-6-30&frs=1&organic_search_click=1',
      tags: ['keycap']
    },
    {
      title: 'Starbucks Coffee Artisan Keycap',
      cost: '24.99',
      src: '/assets/starbucks-coffee-artisan-keycap.jpg',
      link: 'https://www.etsy.com/listing/1062092028/starbucks-coffee-keycaps-handmade-resin?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=artisan+keycaps&ref=sr_gallery-8-31&organic_search_click=1&variation0=2192027624',
      tags: ['keycap']
    },
    {
      title: 'Susuwatari Artisan Keycap',
      cost: '39.00',
      src: '/assets/susuwatari-artisan-keycap.webp',
      link: 'https://www.etsy.com/listing/1414040794/spirited-away-soot-sprite-artisan-keycap?click_key=406ed5652e349b3d43b3ace60680de5657694608%3A1414040794&click_sum=0943f18f&ref=market_strv-2&frs=1',
      tags: ['keycap']
    },
    {
      title: 'Kaonashi Keycap Sculpture',
      cost: '216.05',
      src: '/assets/kaonashi-keycap-sculpture.png',
      link: "https://www.etsy.com/listing/1374904925/no-face-keycap-sculpture-for-mechanical?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=artisan+keycaps&ref=sr_gallery-32-29&organic_search_click=1",
      tags: ['keycap']
    },
    {
      title: 'Rayneo XR Glasses',
      cost: '399.00',
      src: '/assets/rayneo-xr-glasses.png',
      link: 'https://www.rayneo.com/',
      tags: ['electronic']
    },
    {
      title: 'ROLAND Taiko-1',
      cost: '1,499.99',
      src: '/assets/roland-taiko-1.png',
      link: "https://asano.us/products/taiko-1-roland",
      tags: ['electronic', 'taiko']
    },
    {
      title: 'Ultimate Hacking Keyboard',
      cost: '320.00',
      src: '/assets/ultimate-hacking-keyboard.png',
      link: "https://ultimatehackingkeyboard.com/",
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
        <Image src={item.src} alt={item.title} />
        <div class="item-info">
          <div class='item-name'>{item.title}</div>
          <div class='item-cost'>${item.cost}</div>
        </div>
          <a href={item.link} target="_blank" rel="noopener noreferrer">
            <img class="link-arrow" src="/arrow.svg" width="25" height="25" alt="arrow" />
          </a>
      </div>
    {/each}
  </div>
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

  img.link-arrow {
    position: absolute;
    margin: 0.5rem 0.5rem 0 0;
    top: 3px;
    right: 3px;
    width: 15px;
    padding: 0.1rem;
    transition: all 0.2s ease-in-out;
    border-top: 2px solid black;
    border-right: 2px solid black;
  }

  img.link-arrow:hover {
    top: 0px;
    right: 0px;
  }
  
  @media(min-width: 500px) {
    .grid-item {
      width: auto;
    }
  }
  @media(min-width: 900px) {
    img.link-arrow {
      margin: 0;
      padding: 1rem;
      border: none;
    }
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
