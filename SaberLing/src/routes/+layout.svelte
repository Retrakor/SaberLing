<script lang="ts">
    import Navbar from '$lib/components/Navbar.svelte';
  </script>
  
  <Navbar />
  
  <main>
    <slot />
  </main>
  
  <style>
    :global(body) {
      font-family: 'Exo 2', Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #111;
      color: #ffffff;
      background-image: 
        radial-gradient(circle at 50% 50%, rgba(102, 168, 255, 0.1) 0%, transparent 50%),
        radial-gradient(circle at 80% 20%, rgba(105, 102, 255, 0.1) 0%, transparent 50%);
      background-attachment: fixed;
    }
  
    :global(*) {
      box-sizing: border-box;
    }
  
    main {
      padding: 6rem 2rem 2rem;
      max-width: 1200px;
      margin: 0 auto;
    }
  
    :global(h1, h2, h3, h4, h5, h6) {
      font-weight: 700;
      color: #66ccff;
    }
  
    :global(a) {
      color: #66ccff;
      text-decoration: none;
      transition: color 0.3s ease;
    }
  
    :global(a:hover) {
      color: #ff66aa;
    }
  
    :global(button) {
      background-color: #ff66aa;
      color: #ffffff;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
  
    :global(button:hover) {
      background-color: #ff4d94;
    }
  </style>