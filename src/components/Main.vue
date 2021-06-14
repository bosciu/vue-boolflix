<template>
	<main class="p-5 container-fluid">
		<h2>Movies</h2>
		<div class="row">
			<Card
				:datas="movies.results[index]"
				v-for="(movie, index) in movies.results"
				:key="movie.id"
				titleKey="title"
				originalTitleKey="original_title"
			/>
		</div>
		<h2>Series</h2>
		<div class="row">
			<Card
				:datas="series.results[index]"
				v-for="(serie, index) in series.results"
				:key="serie.id"
				titleKey="name"
				originalTitleKey="original_name"
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
			movies: {},
			series: {}
		};
	},
	props: {
		queryString: String
	},
	watch: {
		queryString: function (val) {
			const getMovies = () =>
				axios.get("https://api.themoviedb.org/3/search/movie/", {
					params: {
						api_key: "0584d677244cfdd2883b2bb13c97888b",
						language: "it-IT",
						query: val
					}
				});
			const getSeries = () =>
				axios.get("https://api.themoviedb.org/3/search/tv/", {
					params: {
						api_key: "0584d677244cfdd2883b2bb13c97888b",
						language: "it-IT",
						query: val
					}
				});
			Promise.all([getMovies(), getSeries()]).then((res) => {
				this.movies = res[0].data;
				this.series = res[1].data;
			});
			/* axios
				.get("https://api.themoviedb.org/3/search/movie/", {
					params: {
						api_key: "0584d677244cfdd2883b2bb13c97888b",
						language: "it-IT",
						query: val
					}
				})
				.then((res) => {
					this.filmObject = res.data;
				}); */
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
