<script>
  import { onMount } from "svelte";
  import * as Ably from "ably";

  let messages = $state([]);
  let channel = $state();

  onMount(() => {
    const ably = new Ably.Realtime({
      key: "your-api-key-here",
      clientId: "someid",
    });

    channel = ably.channels.get("your-channel-name");

    channel.subscribe((message) => {
      messages.push(message);
    });

    return () => {
      channel?.unsubscribe(channel);
      channel?.detach();
    };
  });

  const sendMessage = () => {
    channel.publish("test-message", { text: "message text" });
  };
</script>

<div class="App">
  <h1>Ably Svelte Demo</h1>
  <div>
    <button onclick={sendMessage}>Send Message</button>
  </div>

  <h2>Messages</h2>
  <ul>
    {#each messages as msg}
      <li>{msg.data.text}</li>
    {/each}
  </ul>
</div>
