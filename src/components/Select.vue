<template>
	<select
		class="form-select"
		aria-label="Default select example"
		@change="$emit('passoGenereSelezionato', $event.target.value)"
	>
		<option selected disabled>{{ msg }}</option>
		<option value="-1">{{ firstOption }}</option>
		<option v-for="(genre, index) in datas" :key="index" :value="genre.id">
			{{ genre.name }}
		</option>
	</select>
</template>

<script>
export default {
	name: "Select",
	props: {
		datas: Array,
		msg: String,
		firstOption: String
	}
};
</script>

<style scoped>
.form-select {
	width: unset;
	margin-left: calc(var(--bs-gutter-x) / 2);
}
</style>
