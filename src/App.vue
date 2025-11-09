<script setup>
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";
</script>

<template>
	<Header />

	<main class="main">
		<div class="container">
			<Button>Начать игру</Button>

			<Card />
		</div>
	</main>
</template>

<style scoped></style>
