<template>
	<main class="p-5">
		<Card />
	</main>
</template>

<script>
import Card from "./Card";
export default {
	name: "Main",
	components: {
		Card
	}
};
</script>

<style lang="scss" scoped>
@import "../style/variables";
main {
	min-height: calc(100vh - #{$headerHeight});
	background-color: yellow;
}
</style>
