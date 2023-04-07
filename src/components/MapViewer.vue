<template>
	<div class="map">
		<l-map ref="map" v-model:zoom="zoom" :center="[47.41322, -1.219482]">
			<l-tile-layer
				url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
				layer-type="base"
				name="OpenStreetMap"
			></l-tile-layer>
			<l-geo-json :geojson="geojson" :options-style="geoStyler"></l-geo-json>
		</l-map>
	</div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer, LGeoJson } from "@vue-leaflet/vue-leaflet";

export default {
	name: "MapViewer",
	components: {
		LMap,
		LTileLayer,
		LGeoJson,
	},
	data() {
		return {
			zoom: 2,
			geojson: undefined,
			geoStyler: (feature) => ({
				opacity: feature.properties.code / 100000,
			}),
		};
	},
	async created() {
		const response = await fetch(
			""
		);
		this.geojson = await response.json();
	},
};
</script>

<style scoped>
.map {
	border: 1px solid grey;
	width: 90%;
	height: 90%;
}
</style>
