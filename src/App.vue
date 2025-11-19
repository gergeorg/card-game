<script setup>
	import { ref, provide } from 'vue';

	import Button from './components/Button.vue';
	import Card from './components/Card.vue';
	import Header from './components/Header.vue';

	const data = ref();
	const error = ref();
	const score = ref(0);

	const API_ENDPOINT = 'http://localhost:8080';

	const updateScore = (status) => {
		if (status === 'success') score.value += 10;
		if (status === 'fail') score.value -= 4;
	};

	provide('score', score);
	provide('updateScore', updateScore);

	const getData = async () => {
		data.value = null;
		error.value = null;

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

	const handleChangeStatus = (index, status) => {
		data.value[index].status = status;

		updateScore(status);
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
				⚠️ Ошибка загрузки: {{ error.message || JSON.stringify(error) }}
			</div>

			<div v-else class="game">
				<ul class="cards-list">
					<Card
						v-for="(card, i) in data"
						:key="card.id ?? i"
						:word="card.word"
						:translation="card.translation"
						:initial-status="card.status"
						initial-state="closed"
						:num="card.id + 1"
						@change-status="(status) => handleChangeStatus(i, status)"
					/>
				</ul>

				<Button v-if="data" @click="getData()" class="new-game">Начать заново</Button>
			</div>
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
		margin-bottom: 100px;
	}

	.error {
		margin: 0 auto;
		background-color: #f0a4a4;
		max-width: max-content;
		padding: 10px 30px;
		border-radius: 5px;
	}

	.game {
		text-align: center;
	}

	.new-game {
		margin-bottom: 65px;
	}
</style>
