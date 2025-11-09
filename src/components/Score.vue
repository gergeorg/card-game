<script setup>
import HeartIcon from "./icons/HeartIcon.vue";
import { ref } from "vue";

const props = defineProps({
	currentScore: {
		type: Number,
		default: 100,
	},
});

const scoreRef = ref(props.currentScore);
</script>

<template>
	<div class="score">
		{{ scoreRef }}
		<HeartIcon />
	</div>
</template>

<style scoped>
.score {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 10px;
	max-width: min-content;
	border-radius: 36px;
	padding: 12px 24px;
	font-weight: 700;
	font-size: 16px;
	line-height: 1.5;
	color: var(--color-primary);
	box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
	background-color: var(--color-stroke);
}
</style>
