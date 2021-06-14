<template>
	<header class="d-flex">
		<div class="logo-img">
			<img src="../assets/images/logo.png" alt="Gianflix" />
		</div>
		<div class="form">
			<Searchbar />
		</div>
	</header>
</template>

<script>
import Searchbar from "./Searchbar";
export default {
	name: "Header",
	components: {
		Searchbar
	}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
header {
	height: $headerHeight;
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
