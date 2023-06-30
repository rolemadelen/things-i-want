<script>
  import { onMount } from 'svelte';

  const numberOfIssues = 7;
  let content;
  let lastScrollTop;
  let offsetY;

  onMount(() => {
    offsetY = document.body.offsetHeight;
  })

  const issues = [
    {
      id: 7,
      title: 'Issue #7',
      img: '/src/assets/issue7.png'
    },
    {
      id: 6,
      title: 'Issue #6',
      img: '/src/assets/issue6.png'
    },
    {
      id: 5,
      title: 'Issue #5',
      img: '/src/assets/issue5.png'
    },
    {
      id: 4,
      title: 'Issue #4',
      img: '/src/assets/issue4.png'
    },
    {
      id: 3,
      title: 'Issue #3',
      img: '/src/assets/issue3.png'
    },
    {
      id: 2,
      title: 'Issue #2',
      img: '/src/assets/issue2.png'
    },
    {
      id: 1,
      title: 'Issue #1',
      img: '/src/assets/issue1.png'
    }
  ];

  const handleScroll = () => {
    const offset = numberOfIssues - (lastScrollTop / offsetY);
    const main = document.querySelector('.main');

    if(offset > 6.5) {
      main.style.backgroundColor = '#ff608c';
    } else if (offset > 5.5) {
      main.style.backgroundColor = '#fff';
    } else if (offset > 4.5) {
      main.style.backgroundColor = '#00c1b5';
   } else if (offset > 3.5) {
      main.style.backgroundColor = '#ff6519';
    } else if (offset > 2.5) {
      main.style.backgroundColor = '#ffbe00';
    } else if (offset > 1.5) {
      main.style.backgroundColor = '#1d3fbb';
    } else {
      main.style.backgroundColor = '#E30512';
    }

    lastScrollTop = content.scrollTop;
  }
</script>

<main>
  <header>
    <img src="/src/assets/logo.png" class='logo'/>
    <div class='contact'>info@backstagetalks.com</div>
  </header>
  <div class='main' bind:this={content} on:scroll={handleScroll}>
    {#each issues as issue}
      <div class='fullscreen issue' id="issue{issue.id}" data-issue="{issue.id}">
        <img src="{issue.img}"/>
      </div>
    {/each}
  </div>
  <footer>
      <div class='description'>Backstage Talks is a magazine of casual, but in depth dialogues on design and business. Our decisions shape and influence this complex world—to have a chance to make the right ones, we need to talk.</div>
      <div class="copyright">@ 2023 <a href='#'>Published by Büro Milk</a></div>
      <div class='privacy-policy'>
        <a href="#">Privacy Policy</a>
      </div>
  </footer>
  <nav>
    <ul>
      {#each issues as issue}
        <a href="#issue{issue.id}"><li>{issue.title}</li></a>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .main {
    background-color: #ff608c;
    z-index: -1;
    height: 100vh;
    overflow: auto;
    scroll-snap-type: y mandatory;
    transition: background-color 0.3s ease-in-out;
  }

  .issue {
    scroll-snap-align: start;
  }

  header {
    position: fixed;
    top: 20px;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  .logo {
    width: 260px;
    height: auto;
    margin-left: 15px;
  }

  .contact {
    font-weight: 600;
    font-size: 1.1rem;
    margin-right: 15px;
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
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  .copyright {
    font-size: 0.7rem;
    font-weight: light;
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
    margin-right: 15px;
  }

  nav li {
    margin-bottom: 0.5rem;
  }

  nav li:hover {
    text-decoration: underline;
  }

  img {
    width: 420px;
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

</style>
