<script setup>
import { ref } from "vue";

import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";

const cards = ref([
	{ id: 1, word: "unadmitted", translation: "непризнанный", status: "pending" },
	{ id: 2, word: "camel caravan", translation: "караван верблюдов", status: "pending" },
	{ id: 3, word: "pollination", translation: "опыление", status: "success" },
	{ id: 4, word: "oscillotron", translation: "осциллотрон", status: "fail" },
]);

const handleFlip = (index, isOpened) => {
	console.log(`Card ${index} is now ${isOpened ? "open" : "closed"}`);
};

const handleChangeStatus = (index, status) => {
	cards.value[index].status = status;
};
</script>

<template>
	<Header />

	<main class="main">
		<div class="container">
			<Button>Начать игру</Button>

			<ul class="cards-list">
				<Card
					v-for="(card, i) in cards"
					:key="card.id"
					:word="card.word"
					:translation="card.translation"
					:initial-status="card.status"
					initial-state="closed"
					@flip-card="(isOpened) => handleFlip(i, isOpened)"
					@change-status="(status) => handleChangeStatus(i, status)"
				/>
			</ul>
		</div>
	</main>
</template>

<style scoped>
.cards-list {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: 66px 107px;
}
</style>
