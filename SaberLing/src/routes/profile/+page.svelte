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
      { beatmap: 'A Little Happiness', artist: 'Hebe Tien', score: 95100000, accuracy: 95.10, missCount: 3, pp: 297 },
      { beatmap: 'Golden Sky', artist: 'SMILE.dk', score: 99470000, accuracy: 99.47, missCount: 1, pp: 281 },
      { beatmap: 'Yuki no Hana', artist: 'Yura Hatsuki', score: 99140000, accuracy: 99.14, missCount: 2, pp: 279 },
      { beatmap: 'WONDERFUL WONDER (TV Size)', artist: 'EDOGA-SULLIVAN', score: 99260000, accuracy: 99.26, missCount: 0, pp: 274 },
      { beatmap: 'No Ordinary Girl', artist: 'Katarzyna Laska', score: 95040000, accuracy: 95.04, missCount: 5, pp: 270 },
    ];
  
    let playHistory = [
      { month: 'Jan', count: 1000 },
      { month: 'Feb', count: 1200 },
      { month: 'Mar', count: 1500 },
      { month: 'Apr', count: 1800 },
      { month: 'May', count: 2000 },
      { month: 'Jun', count: 2200 },
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
            {@html createRankGraph(rankData)}
          </div>
        </section>
  
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
  
    <section class="top-plays">
      <h2>Best Performance</h2>
      {#each topPlays as play}
        <div class="beatmap-section">
          <div class="beatmap-info">
            <span class="beatmap">{play.beatmap}</span>
            <span class="artist">by {play.artist}</span>
          </div>
          <div class="play-stats">
            <span class="stat" title="Score">{play.score.toLocaleString()}</span>
            <span class="stat" title="Accuracy">{play.accuracy.toFixed(2)}%</span>
            <span class="stat" title="Miss Count">{play.missCount}</span>
            <span class="stat" title="PP">{play.pp}pp</span>
          </div>
        </div>
      {/each}
    </section>
  
    <section class="play-history">
      <h2>Play History</h2>
      <!--<ResponsiveContainer width="100%" height={300}>
        <LineChart data={playHistory}>
          <XAxis dataKey="month" />
          <YAxis />
          <Tooltip />
          <Line type="monotone" dataKey="count" stroke="#ff66aa" />
        </LineChart>
      </ResponsiveContainer>-->
    </section>
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
      display: flex;
      width: 100%;
      gap: 2rem;
    }
  
    .rankings, .stats {
      flex: 1;
      display: flex;
      flex-direction: column;
    }
  
    .rank-box {
      flex: 1;
      text-align: center;
      margin-bottom: 1rem;
    }
  
    .rank {
      font-size: 1.3rem;
      font-weight: bold;
      color: #ff66aa;
    }
  
    .rank-progression {
      width: 100%;
      margin-top: auto;
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
  
    h1 {
      text-align: center;
      margin-top: 60px;
      font-size: 2rem;
    }
  
    h2 {
      margin-bottom: 1rem;
      color: #ff66aa;
    }
  
    .top-plays {
      width: 100%;
    }
  
    .beatmap-section {
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
      color: #999;
    }
  
    .play-stats {
      display: flex;
      gap: 1rem;
    }
  
    .stat {
      position: relative;
      max-width: 100px;
    }
  
    .stat:hover::after {
      content: attr(title);
      position: absolute;
      top: -20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      padding: 2px 5px;
      border-radius: 3px;
      font-size: 0.8rem;
    }
  
    .play-history {
      width: 100%;
    }
  </style>