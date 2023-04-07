<template>
	<div class="map">
		<l-map ref="map" v-model:zoom="zoom" :center="newCoordinates">
			<l-tile-layer
				url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
				layer-type="base"
				name="OpenStreetMap"
			></l-tile-layer>
			<l-geo-json :geojson="geoJson" :options-style="geoStyler"></l-geo-json>
			<l-marker :lat-lng="coordinates">
				<CustomIcon/>
			</l-marker>
		</l-map>
	</div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer, LGeoJson, LMarker } from "@vue-leaflet/vue-leaflet";
import CustomIcon from "@/components/CustomIcon";

export default {
	name: "MapViewer",
	components: {
		LMap,
		LTileLayer,
		LGeoJson,
		LMarker,
		CustomIcon,
	},
	props: {
		newCoordinates: Array,
		geoJson: Object,
	},
	data() {
		return {
			zoom: 5,
			geoStyler: (feature) => ({
				opacity: feature.properties.code / 100000,
			}),
			coordinates: [47.41322, -1.219482],
			iconUrl: 'https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-red.png',
			shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
			iconSize: [25, 41],
			iconAnchor: [12, 41],
			popupAnchor: [1, -34],
			shadowSize: [41, 41]
		};
	},
	watch: {
		newCoordinates: function(coords) { // watch it
			this.coordinates = coords;
		}
	},
};
</script>

<style scoped>
.map {
	border: 1px solid grey;
	height: 90%;
	flex: 1;
}
.icon-class {
	background-color: red;
	content: '★';
	width: 3rem;
	height: 3rem;
	display: block;
	left: -1.5rem;
	top: -1.5rem;
	position: relative;
	border-radius: 3rem 3rem 0;
	transform: rotate(45deg);
	border: 1px solid #FFFFFF;
}
</style>
