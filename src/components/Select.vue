<template>
	<select class="form-select" aria-label="Default select example">
		<option selected disabled>{{ msg }}</option>
		<option v-for="(genre, index) in datas" :key="index" value="1">
			{{ genre.name }}
		</option>
	</select>
</template>

<script>
export default {
	name: "Select",
	props: {
		datas: Array,
		msg: String
	}
};
</script>

<style scoped>
.form-select {
	width: unset;
}
</style>
