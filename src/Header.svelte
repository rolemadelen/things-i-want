<script>
</script>

<header>
  <div class='header-title grid-item'>things i want</div>
  <div class='hello grid-item'>Hello!</div>
  <div class='email grid-item'>
    <a href="mailto:hello@jiieu.com">hello@jiieu.com</a>
  </div>
  <div class='header-desc grid-item'>
    Welcome to my carefully curated list of things I want. 
    This collection represents a compilation of items that hold a special place in my heart, 
    both as a developer and as a passionate taiko player. <br />
    These coveted items embody the fusion of my professional 
    aspirations and personal passions, encapsulating both the products of my pure curiosity and the tools that can bring my dreams to life.
  </div>
</header>

<style>
    header {
    display: grid;
    grid-template-columns: repeat(1, 100vw);
  }

  .header-title {
    font-size: 2rem;
    font-family: 'Ysabeau SC', sans-serif;
    padding: 2rem 0;
  }

  .header-desc {
    font-size: 14px;
    padding: 1rem;
  }

  .hello,
  .email {
    color: white;
  }

  .hello:hover,
  .email:hover {
    background-color: #111;
    transition: all 0.2s ease-in-out;
  }

  .grid-item {
    position: relative;
    border: 1px solid #eee;

    display: flex;
    justify-content: center;
    align-items: center;
      flex-wrap: wrap;
  }

  a {
    color: inherit;
  }

  @media(min-width: 500px) {
    header {
      grid-template-columns: repeat(2,1fr);
    }
    .header-title {
      font-size: 2.5rem;
      grid-row: 1 / span 2;
    }

    .header-desc {
      font-size: 1rem;
      grid-column: 1 / span 2;
    }
  }

  @media(min-width: 900px) {
      .header-title {
        font-size: 3rem;
      }
    }

</style>
