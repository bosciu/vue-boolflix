<template>
	<main class="p-5 d-flex container-fluid">
		<div class="row">
			<Card
				:filmObject="filmObject.results[index]"
				v-for="(film, index) in filmObject.results"
				:key="index"
			/>
		</div>
	</main>
</template>

<script>
import axios from "axios";
import Card from "./Card";
export default {
	name: "Main",
	components: {
		Card
	},
	data() {
		return {
			filmObject: {}
		};
	},
	props: {
		queryString: String
	},
	watch: {
		queryString: function (val) {
			axios
				.get("https://api.themoviedb.org/3/search/movie/", {
					params: {
						api_key: "0584d677244cfdd2883b2bb13c97888b",
						language: "it-IT",
						query: val
					}
				})
				.then((res) => {
					this.filmObject = res.data;
				});
		}
	},
	methods: {}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
main {
	flex-wrap: wrap;
	min-height: calc(100vh - #{$headerHeight});
}
</style>
