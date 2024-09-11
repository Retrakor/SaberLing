<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';

  let showDropdown = false;
  let avatarUrl = '';
  let isLoggedIn = false; // This should be controlled by your authentication logic

  onMount(async () => {
    // Fetch avatar URL from Discord (replace with actual API call)
    avatarUrl = 'https://media.discordapp.net/attachments/1134585812839829615/1283379108578852967/cute-anime-profile-pictures-wlr9y8qcovhhvnji.jpg?ex=66e2c76f&is=66e175ef&hm=c69a96e5847d385204eb49a8da10147d9e014af0958388c1d69a41d3ef411276&=&format=webp&width=906&height=905';
    // Set isLoggedIn based on your authentication logic
    isLoggedIn = true; // For demonstration purposes
  });

  function toggleDropdown() {
    showDropdown = !showDropdown;
  }

  function handleClickOutside(event: MouseEvent) {
    const target = event.target as HTMLElement;
    if (!target.closest('.profile-button') && !target.closest('.dropdown')) {
      showDropdown = false;
    }
  }
</script>

<svelte:window on:click={handleClickOutside} />

<nav>
  <div class="nav-content">
    <div class="left-buttons">
      <a href="/" class="logo">SaberLing</a>
      <a href="/">Home</a>
      <a href="/rankings">Rankings</a>
      <a href="/community">Community</a>
    </div>
    <div class="right-buttons">
      <div class="profile-container">
        <button on:click={toggleDropdown} class="profile-button">
          {#if isLoggedIn}
            <img src={avatarUrl} alt="Profile" />
          {:else}
            <span>Log In</span>
          {/if}
        </button>
        {#if showDropdown}
          <div class="dropdown" transition:fade="{{ duration: 100 }}">
            {#if isLoggedIn}
              <a href="/profile">My Profile</a>
              <a href="/settings">Settings</a>
              <button on:click={() => { /* Implement sign out logic */ }}>Sign out</button>
            {:else}
              <button on:click={() => { /* Implement login logic */ }}>Log In</button>
            {/if}
          </div>
        {/if}
      </div>
    </div>
  </div>
</nav>

<style>
  nav {
    background-color: rgba(0, 0, 0, 0.7);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    backdrop-filter: blur(10px);
  }

  .nav-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0.5rem 2rem;
  }

  .left-buttons, .right-buttons {
    display: flex;
    gap: 1rem;
    align-items: center;
  }

  a, button {
    color: #ffffff;
    text-decoration: none;
    font-size: 1rem;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    transition: background-color 0.3s ease;
  }

  a:hover, button:hover {
    background-color: rgba(255, 255, 255, 0.1);
  }

  .logo {
    font-weight: bold;
    font-size: 1.2rem;
    color: #ff66aa;
  }

  .profile-container {
    position: relative;
  }

  .profile-button {
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .profile-button img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 2px solid #ff66aa;
  }

  .profile-button span {
    padding: 0.5rem 1rem;
    background-color: #ff66aa;
    border-radius: 4px;
    color: #ffffff;
  }

  .dropdown {
    position: absolute;
    top: 100%;
    right: 0;
    background-color: rgba(0, 0, 0, 0.9);
    border-radius: 4px;
    padding: 0.5rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    min-width: 150px;
  }

  .dropdown a, .dropdown button {
    text-align: left;
    background: none;
    border: none;
    cursor: pointer;
    white-space: nowrap;
  }
</style>