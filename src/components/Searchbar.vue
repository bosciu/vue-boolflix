<template>
	<form class="row g-3">
		<div class="col-auto">
			<input
				type="text"
				class="form-control"
				placeholder="Input"
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
export default {
	name: "Searchbar",
	data() {
		return {
			queryString: ""
		};
	}
};
</script>

<style scoped></style>
