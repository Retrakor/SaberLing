<script lang="ts">
  let players = [
    { rank: 1, name: 'Player 1', score: 10000, country: '🇺🇸' },
    { rank: 2, name: 'Player 2', score: 9500, country: '🇯🇵' },
    { rank: 3, name: 'Player 3', score: 9000, country: '🇩🇪' },
    // Add more players as needed
  ];

  let selectedFilter = 'global';

  function handleFilterChange(filter: string) {
    selectedFilter = filter;
    // Implement filter logic here
    console.log(`Filter changed to: ${filter}`);
  }
</script>

<h1>Rankings</h1>

<div class="filter-container">
  <button 
    class:active={selectedFilter === 'global'} 
    on:click={() => handleFilterChange('global')}
  >
    Global
  </button>
  <button 
    class:active={selectedFilter === 'country'} 
    on:click={() => handleFilterChange('country')}
  >
    Country
  </button>
  <button 
    class:active={selectedFilter === 'level'} 
    on:click={() => handleFilterChange('level')}
  >
    Level (old)
  </button>
</div>

<div class="rankings-container">
  {#each players as player, index}
    <div class="player-card" style="animation-delay: {index * 0.1}s">
      <div class="rank">#{player.rank}</div>
      <div class="player-info">
        <span class="country">{player.country}</span>
        <span class="name">{player.name}</span>
      </div>
      <div class="score">{player.score.toLocaleString()}</div>
    </div>
  {/each}
</div>

<style>
  h1 {
    font-size: 2.5rem;
    margin-bottom: 2rem;
    text-align: center;
  }

  .filter-container {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 2rem;
  }

  .filter-container button {
    background-color: rgba(255, 255, 255, 0.1);
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
  }

  .filter-container button:hover {
    background-color: rgba(255, 255, 255, 0.2);
  }

  .filter-container button.active {
    background-color: #ff66aa;
    color: #ffffff;
  }

  .rankings-container {
    display: grid;
    gap: 1rem;
  }

  .player-card {
    display: flex;
    align-items: center;
    background-color: rgba(255, 255, 255, 0.05);
    padding: 1rem;
    border-radius: 8px;
    transition: transform 0.3s ease, background-color 0.3s ease;
    animation: fadeIn 0.5s ease forwards;
    opacity: 0;
  }

  .player-card:hover {
    transform: translateY(-5px);
    background-color: rgba(255, 255, 255, 0.1);
  }

  .rank {
    font-size: 1.5rem;
    font-weight: bold;
    color: #ff66aa;
    width: 60px;
  }

  .player-info {
    flex-grow: 1;
  }

  .country {
    font-size: 1.2rem;
    margin-right: 0.5rem;
  }

  .name {
    font-size: 1.2rem;
    font-weight: bold;
  }

  .score {
    font-size: 1.2rem;
    color: #66ccff;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>