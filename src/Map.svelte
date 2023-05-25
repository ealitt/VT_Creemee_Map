<script>
    import { onMount } from 'svelte';
    import L from 'leaflet';
    import locations from './locations.json';
  
    let mapContainer;
    let map;
  
    onMount(() => {
      map = L.map(mapContainer).setView([44.5, -72.7], 7);
  
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
        maxZoom: 19,
      }).addTo(map);
  
      locations.forEach((location) => {
        L.marker(location.coordinates).addTo(map)
          .bindPopup(location.name)
          .openPopup();
      });
    });
  </script>
  
  <div bind:this={mapContainer} style="height: 500px;"></div>
  