<script lang="ts">
    let posts = [
      { id: 1, author: 'User1', content: 'Just reached a new high score!', likes: 15 },
      { id: 2, author: 'User2', content: 'Looking for teammates for the upcoming tournament', likes: 8 },
      // Add more posts as needed
    ];
  </script>
  
  <h1>Community</h1>
  
  <div class="post-container">
    {#each posts as post}
      <div class="post">
        <h3>{post.author}</h3>
        <p>{post.content}</p>
        <button class="like-button">👍 {post.likes}</button>
      </div>
    {/each}
  </div>
  
  <style>
    h1 {
      font-size: 2rem;
      margin-bottom: 1rem;
    }
  
    .post-container {
      display: grid;
      gap: 1rem;
    }
  
    .post {
      background-color: #1a1a1a;
      padding: 1rem;
      border-radius: 4px;
    }
  
    h3 {
      margin: 0 0 0.5rem;
      color: #4a90e2;
    }
  
    p {
      margin: 0 0 1rem;
    }
  
    .like-button {
      background-color: #2a2a2a;
      border: none;
      color: #ffffff;
      padding: 0.5rem 1rem;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
  
    .like-button:hover {
      background-color: #333333;
    }
  </style>