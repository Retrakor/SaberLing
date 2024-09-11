<script lang="ts">
    let notifications = true;
    let darkMode = true;
    let language = 'en';
  
    function saveSettings() {
      // Implement logic to save settings
      alert('Settings saved!');
    }
  </script>
  
  <h1>Settings</h1>
  
  <form on:submit|preventDefault={saveSettings}>
    <div class="setting">
      <label for="notifications">
        <input type="checkbox" id="notifications" bind:checked={notifications}>
        Enable Notifications
      </label>
    </div>
  
    <div class="setting">
      <label for="darkMode">
        <input type="checkbox" id="darkMode" bind:checked={darkMode}>
        Dark Mode
      </label>
    </div>
  
    <div class="setting">
      <label for="language">Language</label>
      <select id="language" bind:value={language}>
        <option value="en">English</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
      </select>
    </div>
  
    <button type="submit">Save Settings</button>
  </form>
  
  <style>
    h1 {
      font-size: 2rem;
      margin-bottom: 1rem;
    }
  
    form {
      background-color: #1a1a1a;
      padding: 2rem;
      border-radius: 8px;
      max-width: 400px;
      margin: 0 auto;
    }
  
    .setting {
      margin-bottom: 1rem;
    }
  
    label {
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
  
    input[type="checkbox"] {
      width: 1.2rem;
      height: 1.2rem;
    }
  
    select {
      width: 100%;
      padding: 0.5rem;
      background-color: #2a2a2a;
      color: #ffffff;
      border: none;
      border-radius: 4px;
      margin-top: 0.5rem;
    }
  
    button {
      background-color: #4a90e2;
      color: #ffffff;
      border: none;
      padding: 0.75rem 1.5rem;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      transition: background-color 0.3s ease;
    }
  
    button:hover {
      background-color: #3a7ac5;
    }
  </style>