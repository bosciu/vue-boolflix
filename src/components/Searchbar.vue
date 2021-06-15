<template>
	<form class="row g-3">
		<Select
			class="col-auto"
			:datas="seriesGenre"
			msg="Filtra il genere delle serie TV"
		/>
		<Select
			class="col-auto"
			:datas="moviesGenre"
			msg="Filtra il genere dei film"
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
	}
};
</script>

<style scoped></style>
