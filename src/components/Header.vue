<script setup>
import Score from "../components/Score.vue";

const data = {
	currentScore: 100,
};
</script>

<template>
	<header class="header">
		<div class="container header-container">
			<h1 class="title">Запомни слово</h1>
			<Score :data />
		</div>
	</header>
</template>

<style scoped>
.header {
	padding: 49px 0;
}

.header-container {
	display: flex;
	justify-content: space-between;
	align-items: center;
}
</style>
