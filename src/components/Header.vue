<template>
	<header class="d-flex">
		<div class="logo-img">
			<img src="../assets/images/logo.png" alt="Gianflix" />
		</div>
		<div class="form">
			<Searchbar
				@passoQuery="passoQuery"
				:moviesGenre="moviesGenre"
				:seriesGenre="seriesGenre"
			/>
		</div>
	</header>
</template>

<script>
import Searchbar from "./Searchbar";
export default {
	name: "Header",
	components: {
		Searchbar
	},
	props: {
		moviesGenre: Array,
		seriesGenre: Array
	},
	methods: {
		passoQuery(queryString) {
			this.$emit("passoQuery", queryString);
		}
	}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
header {
	position: fixed;
	z-index: 10;
	height: $headerHeight;
	width: 100%;
	padding: 0 1%;
	justify-content: space-between;
	background-color: $netflixGrey;
	img {
		height: 100%;
	}
	.form {
		align-self: center;
	}
}
</style>
