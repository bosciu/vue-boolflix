<template>
	<main class="container-fluid" v-if="ricercaAvviata">
		<h2 class="text-center mb-5">MOVIES</h2>
		<div class="row justify-content-center">
			<div class="col-2" v-for="(movie, index) in movies" :key="movie.id">
				<Card
					:datas="movies[index]"
					titleKey="title"
					originalTitleKey="original_title"
					category="movie"
					:genresTypes="moviesGenres"
				/>
			</div>
		</div>
		<h2 class="text-center m-5">SERIES</h2>
		<div class="row justify-content-center">
			<div class="col-2" v-for="(serie, index) in series" :key="serie.id">
				<Card
					:datas="series[index]"
					titleKey="name"
					originalTitleKey="original_name"
					category="tv"
					:genresTypes="seriesGenres"
				/>
			</div>
		</div>
	</main>
	<div class="loader d-flex justify-content-center align-items-center" v-else>
		Esegui una ricerca
	</div>
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
			series: {},
			ricercaAvviata: false,
			api_key: "0584d677244cfdd2883b2bb13c97888b",
			moviesGenres: [],
			seriesGenres: []
		};
	},
	props: {
		queryString: String
	},
	watch: {
		/* FACCIO CHIAMATA FILM E SERIE CON QUERY  DI HEADER */
		queryString: function (val) {
			if (val == "") {
				this.ricercaAvviata = false;
			} else {
				const getMovies = () =>
					axios.get("https://api.themoviedb.org/3/search/movie/", {
						params: {
							api_key: this.api_key,
							language: "it-IT",
							query: val
						}
					});
				const getSeries = () =>
					axios.get("https://api.themoviedb.org/3/search/tv/", {
						params: {
							api_key: this.api_key,
							language: "it-IT",
							query: val
						}
					});
				Promise.all([getMovies(), getSeries()]).then((res) => {
					this.movies = res[0].data.results;
					this.series = res[1].data.results;
					this.ricercaAvviata = true;
				});
			}
		}
	},
	methods: {},
	created() {
		/* SALVO ARRAY DEI GENERI FILM & SERIES */
		const getMoviesGenres = () =>
			axios.get("https://api.themoviedb.org/3/genre/movie/list", {
				params: {
					api_key: this.api_key,
					language: "it-IT"
				}
			});
		const getSeriesGenres = () =>
			axios.get("https://api.themoviedb.org/3/genre/tv/list", {
				params: {
					api_key: this.api_key,
					language: "it-IT"
				}
			});
		Promise.all([getMoviesGenres(), getSeriesGenres()]).then((res) => {
			this.moviesGenres = res[0].data.genres;
			this.seriesGenres = res[1].data.genres;
		});
	}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
main {
	flex-wrap: wrap;
	padding: 80px 3rem 3rem;
	min-height: 100vh;
	background-color: $netflixGrey;
	.row {
		& > [class*="col"] {
			margin-left: 1%;
		}
	}
	h2 {
		color: $netflixRed;
	}
}
.loader {
	height: 100vh;
	padding-top: $headerHeight;
	font-size: 45px;
}
</style>
