<template>
	<l-icon :icon-url="iconUrl" :shadow-url="shadowUrl" :icon-size="iconSize" :iconAnchor="iconAnchor" :popup-anchor="popupAnchor" :shadow-size="shadowSize"></l-icon>
</template>

<script>
import { LIcon } from "@vue-leaflet/vue-leaflet";

export default {
	name: "CustomIcon",
	components: {
		LIcon,
	},
	data() {
		return {
			iconUrl: 'https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-red.png',
			shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
			iconSize: [25, 41],
			iconAnchor: [12, 41],
			popupAnchor: [1, -34],
			shadowSize: [41, 41]
		};
	},
}
</script>

<style scoped>

</style>
