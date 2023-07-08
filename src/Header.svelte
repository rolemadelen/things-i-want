<script>
</script>

<header>
  <div class='header-title grid-item'>things i want</div>
  <div class='hello grid-item'>Hello!</div>
  <div class='email grid-item'>
    <a href="mailto:hello@jiieu.com">hello@jiieu.com</a>
  </div>
  <div class='header-desc grid-item'>
    Welcome to my carefully curated list of things I want. This collection represents a compilation of items that hold a special place in my heart, both as a developer and as a passionate taiko player. These coveted items embody the fusion of my professional aspirations and personal passions, encapsulating both the products of my pure curiosity and the tools that can bring my dreams to life
  </div>
</header>

<style>
    header {
    display: grid;
    grid-template-columns: repeat(2,1fr);
  }
  .header-title {
    font-size: 2rem;
    font-family: 'Ysabeau SC', sans-serif;
    grid-row: 1 / span 2;
    height: 150px;
  }

  .header-desc {
    grid-column: 1 / span 2;
    font-size: 1rem;
    font-family: 'Roboto';
    height: 100px;
    padding: 0.8rem;
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
  }

  a {
    color: inherit;
  }
</style>
