<script>    
    let messages = $state([]);
  </script>
  
  <div class="App">
    <h1>Ably Svelte Demo</h1>
    <div>
      <button>Send Message</button>
    </div>
  
    <h2>Messages</h2>
    <ul>
      {#each messages as msg}
        <li>{msg.data.text}</li>
      {/each}
    </ul>
  </div>