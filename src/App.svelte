<script>
	import Map from './Map.svelte';
	import MapMarker from './MapMarker.svelte';
</script>

<h1>Hola</h1>	

<Map lat={19} lon={-99} zoom={8}>
	<MapMarker lat={19.8225} lon={-99.0024} label="Svelte Body Shaping"/>
	<MapMarker lat={19.8981} lon={-99.4169} label="Svelte Barbershop & Essentials"/>
	<MapMarker lat={19.7230} lon={-99.4189} label="Svelte Waxing Studio"/>
	<MapMarker lat={19.3378} lon={-99.3966} label="Svelte 30 Nutritional Consultants"/>
	<MapMarker lat={19.6483} lon={-99.0237} label="Svelte Brands LLC"/>
	<MapMarker lat={19.6986} lon={-99.4100} label="Svelte Medical Systems"/>
</Map>