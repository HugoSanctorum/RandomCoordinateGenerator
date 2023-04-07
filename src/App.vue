<template>
	<MapViewer/>
</template>

<script>
import MapViewer from './components/MapViewer.vue'

export default {
	name: 'App',
	components: {
		MapViewer
	}
}
</script>

<style>
body {
	margin: 0;
	padding: 0;
}
#app {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100vh;
	width: 100vw;
}
</style>
