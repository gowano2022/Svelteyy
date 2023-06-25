<script>
export let name;

  import { onMount } from "svelte";

  async function getLocation() {
    try {
      const result = await navigator.permissions.query({ name: "geolocation" });
      if (result.state === "granted") {
        const position = await navigator.geolocation.getCurrentPosition();
        const latitude = position.coords.latitude;
        const longitude = position.coords.longitude;
        const response = await fetch(`https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${latitude}&longitude=${longitude}&localityLanguage=en`);
        const data = await response.json();
        console.log("Location:", data.locality);
        console.log("IP address:", data.ipString);
      } else if (result.state === "denied") {
        const response = await fetch("https://api.bigdatacloud.net/data/client-ip");
        const data = await response.json();
        console.log("IP address:", data.ip);
      } else {
        const permission = await navigator.permissions.request({ name: "geolocation" });
        if (permission.state === "granted") {
          getLocation();
        } else if (permission.state === "denied") {
          const response = await fetch("https://api.bigdatacloud.net/data/client-ip");
          const data = await response.json();
          console.log("IP address:", data.ip);
        }
      }
    } catch (error) {
      console.log("Error getting location permission:", error);
    }
  }

  onMount(getLocation);
</script>


<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<br>
	<p>And check out <a href="https://render.com">Render</a>'s Svelte <a href="https://render.com/docs/deploy-svelte">quickstart guide</a> to see how this site was deployed.</p>
	<p class="large">🧑‍💻</p>
</main>
