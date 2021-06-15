<template>
	<div id="app">
		<Header
			@passoQuery="salvoQuery"
			:moviesGenre="moviesGenre"
			:seriesGenre="seriesGenre"
		/>
		<Main :queryString="queryString" @passoGeneri="salvoGeneri" />
	</div>
</template>

<script>
import Header from "./components/Header";
import Main from "./components/Main";
export default {
	name: "App",
	components: {
		Header,
		Main
	},
	data() {
		return {
			queryString: "",
			moviesGenre: [],
			seriesGenre: []
		};
	},
	methods: {
		salvoQuery(queryString) {
			this.queryString = queryString;
		},
		salvoGeneri(moviesGenre, seriesGenre) {
			moviesGenre.forEach((element) => {
				this.moviesGenre.push(element);
			});
			seriesGenre.forEach((element) => {
				this.seriesGenre.push(element);
			});
		}
	}
};
</script>

<style lang="scss">
@import "./style/generic";
</style>
