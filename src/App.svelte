<script>
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
      }
    } catch (error) {
      console.log("Error getting location permission:", error);
    }
  }

  onMount(getLocation);
</script>

<h1>Location Permission Example</h1>
