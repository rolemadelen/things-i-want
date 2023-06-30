<script>
  const issues = [
    {
      id: 7,
      title: 'Issue #7',
      color: '#ff608c',
      img: '/src/assets/issue7.png'
    },
    {
      id: 6,
      title: 'Issue #6',
      color: '#fff',
      img: '/src/assets/issue6.png'
    },
    {
      id: 5,
      title: 'Issue #5',
      color: '#00c1b5',
      img: '/src/assets/issue5.png'
    },
    {
      id: 4,
      title: 'Issue #4',
      color: '#ff6519',
      img: '/src/assets/issue4.png'
    },
    {
      id: 3,
      title: 'Issue #3',
      color: '#ffbe00',
      img: '/src/assets/issue3.png'
    },
    {
      id: 2,
      title: 'Issue #2',
      color: '#1d3fbb',
      img: '/src/assets/issue2.png'
    },
    {
      id: 1,
      title: 'Issue #1',
      color: '#E30512',
      img: '/src/assets/issue1.png'
    }
  ];
</script>

<main>
  <header>
    <img src="/src/assets/logo.png" class='logo'/>
    <div class='contact'>info@backstagetalks.com</div>
  </header>
  <div class='main'>
    {#each issues as issue}
      <div class='fullscreen' id="{issue.id}" data-issue="{issue.id}">
        <img src="{issue.img}"/>
      </div>
    {/each}
  </div>
  <footer>
      <div class='description'>Backstage Talks is a magazine of casual, but in depth dialogues on design and business. Our decisions shape and influence this complex world—to have a chance to make the right ones, we need to talk.</div>
      <div class="copyright">@ 2023 <a href='#'>Published by Büro Milk</a></div>
      <div>
        <a href="#">Privacy Policy</a>
      </div>
  </footer>
  <nav>
    <ul>
      {#each issues as issue}
        <a href="#{issue.id}"><li>{issue.title}</li></a>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .main {
    height: 100vh;
    background-color: #ff608c;
    z-index: -1;
  }

  header {
    position: fixed;
    top: 0;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  .logo {
    width: 320px;
    height: auto;
  }

  .contact {
    font-weight: 600;
    font-size: 1.3rem;
  }

  footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 320px;
  }

  .description {
    font-size: 1.1rem;
    font-weight: 600;
  }

  .copyright {
    font-size: 0.8rem;
    font-weight: light;
  }

  nav {
    position: fixed;
    right: 0;
    bottom: 0;
    font-size: 1.1rem;
  }

  nav li {
    margin-bottom: 0.5rem;
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
