<script>
</script>

<header>
  <div class='header-title grid-item'>things i want</div>
  <div on:mouseover on:mouseleave class='blog grid-item'>
    <a href="https://blog.madelen.me" target="_blank" rel="noopener noreferrer">https://blog.madelen.me</a>

  </div>
  <div on:mouseover on:mouseleave class='email grid-item'>
    <a href="mailto:rolemadelen@pm.me">rolemadelen@pm.me</a>
  </div>
  <div class='header-desc grid-item'>
    Welcome to my carefully curated list of coveted items. 
    As a developer, taiko player, and curious human being, I have compiled a collection of objects that I aspire to have in my life. 
    From high-quality monitors and AR/VR gears to mechanical and ergonomic keyboards and authentic taiko drums. 
   This collection embodies a diverse range of coveted objects that fuel my passions and aspirations.
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

  .email:hover {
    background-color: #111;
    color: #eee;
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

  .blog {
    display: none;
  }

  .blog,
  .email {
    color: #777;
    padding: 1rem 0;
  }

    .blog a,
    .email a {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
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
      line-height: 1.25;
      padding: 2rem;
    }

    .blog {
      display: flex;
    }
    .blog,
    .email {
      color: #777;
    }

    .blog:hover,
    .email:hover {
      color: #eee;
      background-color: #111;
      transition: all 0.2s ease-in-out;
    }
  }

  @media(min-width: 900px) {
      .header-title {
        font-size: 3rem;
      }
      .header-desc {
        padding: 2rem 5rem;
      }

      .blog, .email {
        padding: none;
      }
    }

</style>
