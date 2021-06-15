<template>
	<div class="card" @mouseover="isHover = true" @mouseleave="isHover = false">
		<img
			:src="imgSrc"
			:alt="datas[titleKey]"
			v-if="!isHover"
			class="poster"
		/>
		<ul>
			<li>Titolo: {{ datas[titleKey] }}</li>
			<li v-if="datas[titleKey] != datas[originalTitleKey]">
				Titolo originale: {{ datas[originalTitleKey] }}
			</li>
			<li>
				Lingua originale:
				<span v-if="flagFinded" class="flag-container">
					<img :src="flagPath" alt="" class="flag" />
				</span>
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
			language: this.datas.original_language,
			imgPath: "https://image.tmdb.org/t/p/w342/",
			isHover: false
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
		},
		imgSrc() {
			let path = this.imgPath;
			if (this.datas.poster_path != null) {
				path += this.datas.poster_path;
			} else {
				if (this.datas.backdrop_path != null) {
					path += this.datas.backdrop_path;
				} else {
					path = require("../assets/images/generalFilm.jpg");
				}
			}
			return path;
		}
	}
};
</script>

<style lang="scss" scoped>
.card {
	/* width: calc(100% / 5 - 30px); */
	position: relative;
	margin: 0 15px 30px;
	padding: 15px;
	height: 350px;
	background-color: red;
	img.poster {
		height: 100%;
		width: 100%;
		position: absolute;
		transform: translate(-15px, -15px);
	}
	.flag {
		width: 35px;
	}
}
</style>
