<template>
	<MapViewer :geo-json="geoJson" :new-coordinates="newCoordinates"/>
	<ToolBar :x="x" :y="y" :country="country" v-on:newSearchEvent="searchRandomCoordinateAction"/>
</template>

<script>
import MapViewer from './components/MapViewer.vue';
import ToolBar from './components/ToolBar.vue';
import GeoJsonGeometriesLookup from "geojson-geometries-lookup";
import { isProxy, toRaw } from 'vue';

export default {
	name: 'App',
	components: {
		MapViewer,
		ToolBar
	},
	data() {
		return {
			geoJson: undefined,
			newCoordinates: [47.41322, -1.219482],
			country: "France",
			x: 47.41322,
			y: -1.219482,
		};
	},
	methods: {
		getRandomValue(min, max) {
			let cal = (Math.random() * (max - min)) + min;
			return parseFloat(cal);
		},
		searchRandomCoordinateAction: function () {
			const glookup = new GeoJsonGeometriesLookup(this.geoJson);
			let randomCoords;
			let container;
			let found = false;
			while (!found) {
				randomCoords = [this.getRandomValue(-90.0, 90.0), this.getRandomValue(-180.0, 180.0)];
				container = glookup.getContainers({type: "Point", coordinates: [randomCoords[1], randomCoords[0]]}, {ignorePoints: true, ignoreLines: true});
				if (container.features.length > 0) {
					found = true;
					let proxyProperties = container.features[0].properties;
					if (isProxy(proxyProperties)) {
						const rawProperties = toRaw(proxyProperties);
						this.country = rawProperties.french_short;
					}
				}
			}
			this.newCoordinates = randomCoords;
			this.x = randomCoords[0];
			this.y = randomCoords[1];
		}
	},
	async created() {
		const response = await fetch(
			"https://raw.githubusercontent.com/HugoSanctorum/RandomCoordinateGenerator/main/src/json/world-administrative-boundaries.geojson"
		);
		this.geoJson = await response.json();
	},

}
</script>

<style>
body {
	margin: 0;
	padding: 0;
}
#app {
	font-family: Calibri;
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100vh;
	gap: 20px;
	padding: 0 30px;
}
</style>
