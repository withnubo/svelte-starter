
<script>
  import spaceship from './assets/spaceship.svg';
  import planet    from './assets/planet.svg';
  import Counter   from "./lib/Counter.svelte"

  // Generate a random starfield
  let stars = Array.from({ length: 100 }, () => ({
    size:  Math.random() * 2 + 1,
    top:   Math.random() * 100,
    left:  Math.random() * 100,
    delay: Math.random() * 5
  }));
</script>

<main class="galaxy">
  {#each stars as star}
    <div
      class="star"
      style="
        --size: {star.size}px;
        top: {star.top}%;
        left: {star.left}%;
        animation-delay: {star.delay}s;
      "
    ></div>
  {/each}

  <div class="logos">
    <img src={spaceship} alt="Spaceship" class="logo spin" />
    <img src={planet}    alt="Planet"    class="logo orbit" />
  </div>

  <h1>👾 Warp to SvelteSpace Vite 🌌</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Navigate the cosmos of
    <a href="https://github.com/sveltejs/kit#readme" target="_blank">
      SvelteKit
    </a>!
  </p>
  <p class="read-the-docs">
    Click the spaceship or planet to see them twirl in zero‑G.
  </p>
</main>

<style>
  /* Global reset + nebula backdrop */
  :global(body) {
    margin: 0;
    overflow: hidden;
    background: radial-gradient(
      ellipse at center,
      #0d0d2b 0%,
      #000 80%
    );
    color: #fff;
    font-family: 'Orbitron', sans-serif;
  }

  main.galaxy {
    position: relative;
    width: 100vw;
    height: 100vh;
    padding: 2rem;
    box-sizing: border-box;
  }

  /* Twinkling stars */
  .star {
    position: absolute;
    width: var(--size);  height: var(--size);
    background: #fff;     border-radius: 50%;
    opacity: 0.3;         box-shadow: 0 0 5px #fff;
    animation: twinkle 5s infinite ease-in-out;
  }
  @keyframes twinkle {
    0%,100% { opacity: 0.3; }
    50%     { opacity: 1;   }
  }

  /* Logo container */
  .logos {
    display: flex;
    gap: 2rem;
    justify-content: center;
    align-items: center;
  }

  .logo {
    width: 8rem;
    cursor: pointer;
  }

  /* Hover animations */
  .logo.spin:hover   { animation: spin 4s linear infinite; }
  .logo.orbit:hover  { animation: orbit 6s linear infinite; }

  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }
  @keyframes orbit {
    0%   { transform: rotate(0deg) translateX(10px) rotate(0deg); }
    100% { transform: rotate(360deg) translateX(10px) rotate(-360deg); }
  }

  /* Title styling */
  h1 {
    text-align: center;
    font-size: 3rem;
    margin: 1rem 0;
    text-shadow: 0 0 10px #66f, 0 0 20px #66f;
  }

  /* Card glowy sci‑fi vibe */
  .card {
    margin: 0 auto;
    padding: 2rem;
    background: rgba(255,255,255,0.1);
    border: 1px solid #444;
    border-radius: 1rem;
    box-shadow: 0 0 20px rgba(0,255,255,0.2);
  }

  a {
    color: #66ffff;
    text-decoration: underline;
  }
  a:hover {
    color: #ff66ff;
  }

  .read-the-docs {
    text-align: center;
    font-style: italic;
    opacity: 0.7;
    margin-top: 1rem;
  }
</style>
