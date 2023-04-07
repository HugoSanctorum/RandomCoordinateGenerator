<template>
	<div class="toolbar">
		<div class="generate-button" @click="searchRandomCoordinateAction">Nouvelle coordonnées aléatoires</div>
		<div class="result-container">
			<ul>
				<li>Pays: {{country}}</li>
				<li>Coordonnées: [{{x}}, {{y}}]</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	name: "ToolBar",
	props: {
		country: String,
		x: Number,
		y: Number,
	},
	methods: {
		searchRandomCoordinateAction: function () {
			this.$emit('newSearchEvent');
		}
	}
};
</script>

<style scoped>
.toolbar {
	border: 1px solid grey;
	width: 400px;
	height: 90%;
	display: flex;
	align-items: center;
	flex-direction: column;
}
.generate-button {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 10px 20px;
	background-color: cadetblue;
	color: white;
	font-weight: bold;
	border-radius: 20px;
	margin: 30px 0;
	cursor: pointer;
}

.result-container {
	width: 100%;
	display: flex;
}

</style>
