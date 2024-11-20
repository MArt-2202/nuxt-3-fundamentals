<template>
	<div class="container">
		<NuxtLayout>
			<NuxtPage />
		</NuxtLayout>
	</div>
</template>

<script setup>
useHead({
	titleTemplate: (titleChunk) =>
	{
		return titleChunk ? `${titleChunk} - My movie site` : "My movie site";
	},
});
</script>

<style>
.container {
	max-width: 1000px;
	margin-left: auto;
	margin-right: auto;
}

nav {
	display: flex;
	gap: 10px;
}
</style>
