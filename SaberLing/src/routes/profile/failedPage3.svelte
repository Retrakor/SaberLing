<script lang="ts">
    import { onMount } from 'svelte';
  
    let user = {
      username: 'PlayerOne',
      avatar: 'https://cdn.discordapp.com/avatars/123456789/abcdef123456.png',
      banner: 'https://example.com/banner.jpg',
      country: '🇺🇸',
      globalRank: 1337,
      countryRank: 42,
      rankedScore: 12345,
      passes: 500,
      playCount: 10000,
      totalPlayTime: '500h 30m',
      level: 100
    };
  
    let rankData = [
      { date: '90 days ago', rank: 2000 },
      { date: '60 days ago', rank: 1800 },
      { date: '30 days ago', rank: 1500 },
      { date: 'Today', rank: 1337 }
    ];
  
    let topPlays = [
      { beatmap: 'Beatmap 1', artist: 'Artist 1', score: 1000000, accuracy: 98.5, missCount: 1, pp: 300 },
      { beatmap: 'Beatmap 2', artist: 'Artist 2', score: 990000, accuracy: 97.8, missCount: 2, pp: 280 },
      { beatmap: 'Beatmap 3', artist: 'Artist 3', score: 980000, accuracy: 96.5, missCount: 3, pp: 260 },
      // Add more top plays as needed
    ];
  
    let playHistory = [
      { month: 'Jan', count: 1000 },
      { month: 'Feb', count: 1200 },
      { month: 'Mar', count: 1500 },
      { month: 'Apr', count: 1800 },
      { month: 'May', count: 2000 },
      // Add more months as needed
    ];
  
    function createRankGraph(data) {
      const width = 500;
      const height = 200;
      const padding = 30;
      const maxRank = Math.max(...data.map(d => d.rank));
      const minRank = Math.min(...data.map(d => d.rank));
  
      const xScale = (i) => (i / (data.length - 1)) * (width - 2 * padding) + padding;
      const yScale = (rank) => height - (((rank - minRank) / (maxRank - minRank)) * (height - 2 * padding) + padding);
  
      const points = data.map((d, i) => `${xScale(i)},${yScale(d.rank)}`).join(' ');
  
      return `
        <svg width="${width}" height="${height}" xmlns="http://www.w3.org/2000/svg">
          <polyline
            fill="none"
            stroke="#ff66aa"
            stroke-width="2"
            points="${points}"
          />
          ${data.map((d, i) => `
            <circle cx="${xScale(i)}" cy="${yScale(d.rank)}" r="4" fill="#ff66aa" />
            <text x="${xScale(i)}" y="${yScale(d.rank) - 10}" text-anchor="middle" font-size="12" fill="#ffffff">${d.rank}</text>
          `).join('')}
        </svg>
      `;
    }
  
    function createPlayHistoryGraph(data) {
      const width = 500;
      const height = 200;
      const padding = 30;
      const maxCount = Math.max(...data.map(d => d.count));
  
      const xScale = (i) => (i / (data.length - 1)) * (width - 2 * padding) + padding;
      const yScale = (count) => height - ((count / maxCount) * (height - 2 * padding) + padding);
  
      const points = data.map((d, i) => `${xScale(i)},${yScale(d.count)}`).join(' ');
  
      return `
        <svg width="${width}" height="${height}" xmlns="http://www.w3.org/2000/svg">
          <polyline
            fill="none"
            stroke="#66ccff"
            stroke-width="2"
            points="${points}"
          />
          ${data.map((d, i) => `
            <circle cx="${xScale(i)}" cy="${yScale(d.count)}" r="4" fill="#66ccff" />
            <text x="${xScale(i)}" y="${yScale(d.count) - 10}" text-anchor="middle" font-size="12" fill="#ffffff">${d.count}</text>
            <text x="${xScale(i)}" y="${height - 10}" text-anchor="middle" font-size="12" fill="#ffffff">${d.month}</text>
          `).join('')}
        </svg>
      `;
    }
  
    onMount(() => {
      // Fetch user data, rank progression data, top plays, and play history here
    });
  </script>
  
  <div class="profile-container">
    <!-- Profile header section (unchanged) -->
    <section class="profile-header">
      <div class="banner" style="background-image: url({user.banner});">
        <img src={user.avatar} alt={user.username} class="avatar" />
      </div>
      <h1>{user.username} <span class="country">{user.country}</span></h1>
    </section>
  
    <div class="content-wrapper">
      <div class="main-content">
        <!-- Rankings section -->
        <section class="rankings">
          <div class="rank-box">
            <h2>Global Ranking</h2>
            <p class="rank">#{user.globalRank}</p>
          </div>
          <div class="rank-box">
            <h2>Country Ranking</h2>
            <p class="rank">#{user.countryRank}</p>
          </div>
          <div class="rank-progression">
            <h2>Rank Progression (Last 90 days)</h2>
            {@html createRankGraph(rankData)}
          </div>
        </section>
  
        <!-- Top plays section -->
        <section class="top-plays">
          <h2>Top Plays</h2>
          <ul>
            {#each topPlays as play}
              <li>
                <div class="beatmap-info">
                  <span class="beatmap">{play.beatmap}</span>
                  <span class="artist">{play.artist}</span>
                </div>
                <div class="play-stats">
                  <span class="stat" title="Score">{play.score}</span>
                  <span class="stat" title="Accuracy">{play.accuracy}%</span>
                  <span class="stat" title="Miss Count">{play.missCount}</span>
                  <span class="stat" title="PP">{play.pp}</span>
                </div>
              </li>
            {/each}
          </ul>
        </section>
  
        <!-- Play history section -->
        <section class="play-history">
          <h2>Play History</h2>
          {@html createPlayHistoryGraph(playHistory)}
        </section>
      </div>
  
      <!-- Player stats section (unchanged) -->
      <section class="stats">
        <h2>Player Stats</h2>
        <div class="stat-item">
          <span class="stat-label">Ranked Score</span>
          <span class="stat-value">{user.rankedScore} pp</span>
        </div>
        <div class="stat-item">
          <span class="stat-label">Passes</span>
          <span class="stat-value">{user.passes}</span>
        </div>
        <div class="stat-item">
          <span class="stat-label">Play Count</span>
          <span class="stat-value">{user.playCount}</span>
        </div>
        <div class="stat-item">
          <span class="stat-label">Total Play Time</span>
          <span class="stat-value">{user.totalPlayTime}</span>
        </div>
        <div class="stat-item">
          <span class="stat-label">Level</span>
          <span class="stat-value">{user.level}</span>
        </div>
      </section>
    </div>
  </div>
  
  <style>
    /* ... (previous styles remain unchanged) ... */
  
    .top-plays ul {
      list-style-type: none;
      padding: 0;
    }
  
    .top-plays li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem 0;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    }
  
    .beatmap-info {
      display: flex;
      flex-direction: column;
    }
  
    .beatmap {
      font-weight: bold;
    }
  
    .artist {
      font-size: 0.9rem;
      color: #cccccc;
    }
  
    .play-stats {
      display: flex;
      gap: 1rem;
    }
  
    .stat {
      position: relative;
    }
  
    .stat:hover::after {
      content: attr(title);
      position: absolute;
      top: -30px;
      left: 50%;
      transform: translateX(-50%);
      background-color: rgba(0, 0, 0, 0.8);
      color: #ffffff;
      padding: 0.25rem 0.5rem;
      border-radius: 4px;
      font-size: 0.8rem;
      white-space: nowrap;
    }
  
    .play-history, .rank-progression {
      overflow-x: auto;
    }
  </style>