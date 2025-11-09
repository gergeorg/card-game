<script setup>
import { ref } from "vue";
import CancelIcon from "./icons/CancelIcon.vue";
import SuccessIcon from "./icons/SuccessIcon.vue";

const props = defineProps({
	word: {
		type: String,
		default: "unknown",
	},
	translation: {
		type: String,
		default: "?",
	},
	initialState: {
		type: String,
		default: "closed",
		validator: (v) => ["closed", "opened"].includes(v),
	},
	initialStatus: {
		type: String,
		default: "pending",
		validator: (v) => ["pending", "success", "fail"].includes(v),
	},
});

const emit = defineEmits({
	flipCard: (payload) => typeof payload === "boolean" || payload === undefined,
	changeStatus: (payload) => typeof payload === "string" && ["success", "fail"].includes(payload),
});

const card = ref({
	word: props.word,
	translation: props.translation,
	state: props.initialState,
	status: props.initialStatus,
});

const handleFlipCard = () => {
	emit("flipCard", true);
};

const handleChangeStatus = () => {
	console.log("ChangeStatus");
};
</script>

<template>
	<div class="card" @click="handleFlipCard()">
		<div class="card-number">01</div>
		<div class="card-content">unadmitted</div>
		<div class="card-footer">
			<span class="card-text">Перевенуть</span>

			<div class="card-buttons">
				<button class="card-button">
					<CancelIcon />
				</button>

				<button class="card-button" @click="handleChangeStatus()">
					<SuccessIcon />
				</button>
			</div>
		</div>
	</div>
</template>

<style scoped>
.card {
	width: 250px;
	height: 376px;
	background-color: var(--color-white);
	border-radius: 16px;
	box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.1);
	padding: 28px 19px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	position: relative;
	transition: background-color 0.3s ease-in-out;
	cursor: pointer;
}

.card-number {
	background-color: var(--color-white);
	position: absolute;
	top: 20px;
	left: 35px;
	font-weight: 400;
	font-size: 14px;
	color: var(--color-text-card);
	transition: background-color 0.3s ease-in-out;
}

.card-content {
	text-align: center;
	flex-grow: 1;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 18px;
	font-weight: 400;
	color: var(--color-text-card);
	border: 1px solid var(--color-stroke);
	border-radius: 12px;
	transition: border 0.3s ease-in-out;
}

.card-footer {
	position: absolute;
	bottom: 19px;
	left: 50%;
	transform: translateX(-50%);
	font-weight: 700;
	font-size: 12px;
	line-height: 150%;
	letter-spacing: 0.12em;
	color: var(--color-text);
	text-transform: uppercase;
	background-color: var(--color-white);
	padding: 0 4px;
	transition: background-color 0.3s ease-in-out;
}

.card-buttons {
	display: flex;
	gap: 32px;
}

.card-button {
	background-color: transparent;
	border: none;
	cursor: pointer;
}

.card-button:hover {
	transform: scale(1.2);
}

.card:hover {
	background-color: var(--color-stroke);
}

.card:hover .card-number {
	background-color: var(--color-stroke);
}

.card:hover .card-content {
	border: 1px solid var(--color-primary);
}

.card:hover .card-footer {
	background-color: var(--color-stroke);
}
</style>
