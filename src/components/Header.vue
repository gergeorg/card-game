<script setup>
import Score from "../components/Score.vue";
</script>

<template>
	<header class="header">
		<div class="container header-container">
			<h1 class="title">Запомни слово</h1>
			<Score :current-score="100" />
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
