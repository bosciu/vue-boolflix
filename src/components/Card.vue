<template>
	<div class="card">
		<ul>
			<li>Titolo: {{ datas[titleKey] }}</li>
			<li>Titolo originale: {{ datas[originalTitleKey] }}</li>
			<li>
				Lingua originale:
				<div v-if="flagFinded" class="flag-container">
					<img :src="flagPath" alt="" />
				</div>
				<div v-else class="lang-info">
					{{ langUppercase }}
				</div>
			</li>
			<li>Voto: {{ datas.vote_average }}</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	data() {
		return {
			flagFinded: false,
			flagPath: "",
			language: this.datas.original_language
		};
	},
	props: {
		datas: Object,
		titleKey: String,
		originalTitleKey: String
	},
	created() {
		const originalLang = this.language;
		if (originalLang == "it" || originalLang == "en") {
			if (originalLang == "it") {
				this.flagPath = require("../assets/images/it.png");
			} else if (originalLang == "en") {
				this.flagPath = require("../assets/images/en.png");
			}
			this.flagFinded = true;
		}
	},
	computed: {
		langUppercase() {
			return this.language.toUpperCase();
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
