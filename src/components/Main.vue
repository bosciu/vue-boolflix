<template>
	<div>
		<transition name="fade">
			<div class="loader-gif" v-if="!isLoaded">
				<img src="../assets/images/loader.gif" alt="Netflix" />
			</div>
		</transition>
		<div>
			<main class="container-fluid" v-show="ricercaAvviata">
				<h2 class="text-center mb-5">Film</h2>
				<h3 v-show="ricercaAvviata && filteredMovies.length == 0">
					La ricerca non ha prodotto risultati
				</h3>
				<div class="row justify-content-center">
					<div
						class="col-2"
						v-for="movie in filteredMovies"
						:key="movie.id"
					>
						<Card
							:datas="movie"
							titleKey="title"
							originalTitleKey="original_title"
							category="movie"
							:genresTypes="moviesGenres"
						/>
					</div>
				</div>
				<h2 class="text-center m-5">Serie TV</h2>
				<h3 v-show="ricercaAvviata && filteredSeries.length == 0">
					La ricerca non ha prodotto risultati
				</h3>
				<div class="row justify-content-center">
					<div
						class="col-2"
						v-for="serie in filteredSeries"
						:key="serie.id"
					>
						<Card
							:datas="serie"
							titleKey="name"
							originalTitleKey="original_name"
							category="tv"
							:genresTypes="seriesGenres"
						/>
					</div>
				</div>
			</main>
			<div
				class="loader d-flex justify-content-center align-items-center"
				v-if="!ricercaAvviata && isLoaded"
			>
				Esegui una ricerca
			</div>
		</div>
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
			movies: [],
			series: [],
			ricercaAvviata: false,
			api_key: "0584d677244cfdd2883b2bb13c97888b",
			moviesGenres: [],
			seriesGenres: [],
			isLoaded: false
		};
	},
	props: {
		queryString: String,
		genereSerieSelezionato: Number,
		genereFilmSelezionato: Number
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
	computed: {
		filteredMovies() {
			var filteredArray = [];
			if (
				this.genereFilmSelezionato == undefined ||
				this.genereFilmSelezionato == -1
			) {
				filteredArray = this.movies;
			} else {
				filteredArray = this.movies.filter((element) => {
					return element.genre_ids.includes(
						this.genereFilmSelezionato
					);
				});
			}
			return filteredArray;
		},
		filteredSeries() {
			var filteredArray = [];
			if (
				this.genereSerieSelezionato == undefined ||
				this.genereSerieSelezionato == -1
			) {
				filteredArray = this.series;
			} else {
				filteredArray = this.series.filter((element) => {
					return element.genre_ids.includes(
						this.genereSerieSelezionato
					);
				});
			}
			return filteredArray;
		}
	},
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
			this.$emit("passoGeneri", this.moviesGenres, this.seriesGenres);
		});
		setTimeout(() => {
			this.isLoaded = true;
		}, 2000);
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
	h3 {
		text-align: center;
		color: white;
		text-decoration: underline;
		font-size: 36px;
	}
}
.loader {
	height: 100vh;
	padding-top: $headerHeight;
	font-size: 45px;
}
.loader-gif {
	color: transparent;
	position: relative;
	z-index: 100;
	background-color: black;
	height: 100vh;
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 60%;
	}
}
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
	opacity: 0;
}
</style>
