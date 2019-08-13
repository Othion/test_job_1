<template>
	<div id="app">
		<rating-board />
	</div>
</template>

<script>
import RatingBoard from './components/RatingBoard/RatingBoard'

export default {
	components: {
		RatingBoard
	}
}
</script>

<style lang="scss">
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #000;
	margin: 0 auto;
	max-width: 960px;
	height: 100vh;
}
</style>
