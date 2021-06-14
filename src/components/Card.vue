<template>
	<div class="card">
		<ul>
			<li>Titolo: {{ filmObject.title }}</li>
			<li>Titolo originale: {{ filmObject.original_title }}</li>
			<li>
				Lingua originale:
				<div v-if="flagFinded" class="flag-container">
					<img :src="flagPath" alt="" />
				</div>
				<div v-else class="lang-info">
					{{ filmObject.original_language }}
				</div>
			</li>
			<li>Voto: {{ filmObject.vote_average }}</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	data() {
		return {
			flagFinded: false,
			flagPath: ""
		};
	},
	props: {
		filmObject: Object
	},
	created() {
		const originalLang = this.filmObject.original_language;
		if (originalLang == "it" || originalLang == "en") {
			if (originalLang == "it") {
				this.flagPath = require("../assets/images/it.png");
			} else if (originalLang == "en") {
				this.flagPath = require("../assets/images/en.png");
			}
			this.flagFinded = true;
		}
	}
};
</script>

<style lang="scss" scoped>
.card {
	width: calc(100% / 5 - 30px);
	margin: 0 15px 30px;
	padding: 15px;
	height: 350px;
	background-color: red;
	img {
		width: 35px;
	}
}
</style>
