<script setup></script>

<template>
	<button class="button">
		<slot />
	</button>
</template>

<style scoped>
.button {
	border: none;
	border-radius: 100px;
	padding: 16px 10px;
	color: var(--color-white);
	background-color: var(--color-primary);
	cursor: pointer;
	font-family: var(--font);
	font-weight: 400;
	font-size: 24px;
	line-height: 150%;
	transition: background-color 0.3s ease-in-out;
	min-width: 335px;
}

.button:hover {
	background-color: var(--color-primary-hover);
}
</style>
