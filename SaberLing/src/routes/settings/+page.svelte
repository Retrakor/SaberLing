<script lang="ts">
  let profileName = '';
  let avatar = '';
  let profileBanner = '';
  let signature = '';
  let language = 'en';

  function saveSettings() {
    // Implement logic to save settings
    alert('Settings saved!');
  }

  function deleteAccount() {
    // Implement logic to delete account
    alert('Account deleted!');
  }

  function logout() {
    // Implement logic to log out
    alert('Logged out!');
  }
</script>

<h1>Settings</h1>

<form on:submit|preventDefault={saveSettings}>
  <section>
    <h2>Profile</h2>
    <div class="setting">
      <label for="profileName">Link your BeatLeader account!</label>
      <input type="text" id="profileName" bind:value={profileName}>
    </div>
    <!--<div class="setting">
      <label for="avatar">Avatar</label>
      <input type="file" id="avatar" bind:value={avatar} accept="image/*">
    </div>-->
    <div class="setting">
      <label for="profileBanner">Profile Banner</label>
      <input type="file" id="profileBanner" bind:value={profileBanner} accept="image/*">
    </div>
  </section>

  <section>
    <h2>Signature</h2>
    <div class="setting">
      <label for="signature">Signature</label>
      <textarea id="signature" bind:value={signature}></textarea>
    </div>
  </section>

  <section>
    <h2>Options</h2>
    <div class="setting">
      <label for="language">Language</label>
      <select id="language" bind:value={language}>
        <option value="en">English</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
      </select>
    </div>
    <div class="setting">
      <button type="button" on:click={deleteAccount} class="danger">Delete Account</button>
    </div>
    <div class="setting">
      <button type="button" on:click={logout}>Log Out</button>
    </div>
  </section>

  <button type="submit">Save Settings</button>
</form>

<style>
  h1 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  h2 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    
  }

  form {
    background-color: #1a1a1a;
    padding: 2rem;
    border-radius: 8px;
    max-width: 500px;
    margin: 0 auto;
  }

  section {
    margin-bottom: 2rem;
  }

  .setting {
    margin-bottom: 1rem;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
  }

  input[type="text"],
  input[type="file"],
  select,
  textarea {
    width: 100%;
    padding: 0.5rem;
    background-color: #2a2a2a;
    color: #ffffff;
    border: none;
    border-radius: 4px;
  }

  textarea {
    height: 100px;
    resize: vertical;
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

  button.danger {
    background-color: #e74c3c;
  }

  button.danger:hover {
    background-color: #c0392b;
  }
</style>