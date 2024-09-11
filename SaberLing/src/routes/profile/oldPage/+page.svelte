<script lang="ts">
    import { onMount } from 'svelte';
    import { LineChart, Line, XAxis, YAxis, Tooltip, ResponsiveContainer } from 'recharts';
    import type { SvelteComponentTyped } from "svelte";
  
    let user = {
      username: 'PlayerOne',
      avatar: 'https://media.discordapp.net/attachments/1134585812839829615/1283379108578852967/cute-anime-profile-pictures-wlr9y8qcovhhvnji.jpg?ex=66e2c76f&is=66e175ef&hm=c69a96e5847d385204eb49a8da10147d9e014af0958388c1d69a41d3ef411276&=&format=webp&width=906&height=905',
      banner: 'https://media.discordapp.net/attachments/1134585812839829615/1283390711521349686/wp6081414-533061985.jpg?ex=66e2d23d&is=66e180bd&hm=04f3fc2b7bcba8d24bc20fe76491d24c37f5e35eae76bff025f65e05b71d0961&=&format=webp&width=1609&height=905',
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
  
    onMount(() => {
      // Fetch user data and rank progression data here
    });


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



  </script>
  


  <div class="profile-container">
    <section class="profile-header">
      <div class="banner" style="background-image: url({user.banner});">
        <img src={user.avatar} alt={user.username} class="avatar" />
      </div>
      <h1>{user.username} <span class="country">{user.country}</span></h1>
    </section>
  
    <div class="content-wrapper">
      <div class="main-content">
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
              <!-- Rankings section -->
              <section class="rankings">
                <div class="rank-progression">
                  {@html createRankGraph(rankData)}
                </div>
          </div>
        </section>
  
        <section class="future-section">
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
      </div>
  
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
    .profile-container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 2rem;
    }
  
    section {
      background-color: rgba(255, 255, 255, 0.05);
      border-radius: 15px;
      padding: 1.5rem;
      margin-bottom: 2rem;
    }
  
    .profile-header {
      position: relative;
      overflow: hidden;
      padding: 0;
    }
  
    .banner {
      height: 200px;
      background-size: cover;
      background-position: center;
      position: relative;
    }
  
    .avatar {
      position: absolute;
      bottom: -50px;
      left: 50%;
      transform: translateX(-50%);
      width: 100px;
      height: 100px;
      border-radius: 50%;
      border: 4px solid #ff66aa;
    }
  
    .country {
      font-size: 1.5rem;
      margin-left: 0.5rem;
    }
  
    .content-wrapper {
      display: flex;
      gap: 2rem;
    }
  
    .main-content {
      flex: 1;
      margin-bottom: 1rem;
      margin-top: 1;
    }
  
    .rankings {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
    }
  
    .rank-box {
      flex: 1;
      min-width: 150px;
      text-align: center;
    }

    .rank-box2 {
      flex: 1;
      min-width: 80px;
      text-align: center;
    }
  
    .rank {
      font-size: 1.3rem;
      font-weight: bold;
      color: #ff66aa;
    }
  
    .rank-progression {
      width: 100%;
      margin-top: 0.5rem;
    }
  
    .stats {
      width: 300px;
      height: "main-content";
    }
  
    .stat-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 0.5rem;
    }
  
    .stat-label {
      color: #66ccff;
    }
  
    .stat-value {
      font-weight: bold;
    }
  
    .future-section {
      min-height: 200px;
    }

    h1 {
      text-align: center;
      margin-top: 60px;
      font-size: 2rem;
    }
  
    h2 {
      margin-bottom: 1rem;
      color: #ff66aa;
    }

    h3 {
      margin-bottom: 0.5rem;
      color: #ff66aa;
    }
  </style>