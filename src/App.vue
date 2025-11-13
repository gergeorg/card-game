<script setup>
	import { ref } from 'vue';

	import Button from './components/Button.vue';
	import Card from './components/Card.vue';
	import Header from './components/Header.vue';

	const data = ref();
	const error = ref();

	const API_ENDPOINT = 'http://localhost:8080';

	const getData = async () => {
		try {
			const response = await fetch(`${API_ENDPOINT}/api/random-words`);

			if (!response.ok) {
				error.value = await response.json();
				data.value = null;
				return;
			}

			const rawData = await response.json();

			data.value = rawData.map((item, index) => ({
				...item,
				id: index,
				status: 'pending',
			}));

			error.value = null;
		} catch (err) {
			error.value = { message: err.message || 'Network error' };
			data.value = null;
		}
	};

	const handleFlip = (index, isOpened) => {
		console.log(`Card ${index} is now ${isOpened ? 'open' : 'closed'}`);
	};

	const handleChangeStatus = (index, status) => {
		if (data.value && data.value[index]) {
			data.value[index].status = status;
		}
	};
</script>

<template>
	<Header />

	<main class="main">
		<div class="container">
			<div class="button-wrapper" v-if="!data">
				<Button @click="getData()">Начать игру</Button>
			</div>

			<div v-if="error" class="error">
				Ошибка загрузки: {{ error.message || JSON.stringify(error) }}
			</div>

			<ul v-else class="cards-list">
				<Card
					v-for="(card, i) in data"
					:key="card.id ?? i"
					:word="card.word"
					:translation="card.translation"
					:initial-status="card.status"
					initial-state="closed"
					:num="card.id + 1"
					@flip-card="(isOpened) => handleFlip(i, isOpened)"
					@change-status="(status) => handleChangeStatus(i, status)"
				/>
			</ul>
		</div>
	</main>
</template>

<style scoped>
	.button-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		min-height: 500px;
	}
	.cards-list {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 66px 107px;
	}
</style>
