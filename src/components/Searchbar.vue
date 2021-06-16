<template>
	<form class="row g-3">
		<Select
			class="col-auto"
			:datas="seriesGenre"
			@passoGenereSelezionato="genereSerieSelezionato"
			msg="Filtra il genere delle serie TV"
			firstOption="Tutte le serie"
		/>
		<Select
			class="col-auto"
			:datas="moviesGenre"
			@passoGenereSelezionato="genereFilmSelezionato"
			msg="Filtra il genere dei film"
			firstOption="Tutti i film"
		/>
		<div class="col-auto">
			<input
				type="text"
				class="form-control"
				placeholder="Inserisci titolo"
				v-model="queryString"
			/>
		</div>
		<div class="col-auto">
			<button
				type="submit"
				class="btn btn-primary"
				@click.prevent="$emit('passoQuery', queryString)"
			>
				Ricerca
			</button>
		</div>
	</form>
</template>

<script>
import Select from "./Select";
export default {
	name: "Searchbar",
	components: {
		Select
	},
	props: {
		moviesGenre: Array,
		seriesGenre: Array
	},
	data() {
		return {
			queryString: ""
		};
	},
	methods: {
		genereSerieSelezionato(genereSerieSelezionato) {
			this.$emit("genereSerieSelezionato", genereSerieSelezionato);
		},
		genereFilmSelezionato(genereFilmSelezionato) {
			this.$emit("genereFilmSelezionato", genereFilmSelezionato);
		}
	}
};
</script>

<style scoped>
form {
	width: 100%;
	justify-content: flex-end;
	align-items: center;
}
</style>
