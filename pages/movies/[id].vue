<script setup>
const route = useRoute();

const { data, error } = await useFetch(`https://www.omdbapi.com/?apikey=85553f5e&i=${route.params.id}`,
	{
		key: route.params.id,
		pick: ['Title', 'Plot', 'Error', 'Poster'],
	}
);

if (error.value) {
	// console.log(error.value);
}

if (data.value.Error === "Incorrect IMDb ID.") {
	showError({ statusCode: 404, statusMessage: "Page Not Found" });
}

useHead({
	title: data.value.Title,
	meta: [
		{ name: "description", content: data.value.Plot },
		{ property: "og:description", content: data.value.Plot },
		{ property: "og:image", content: data.value.Poster },
		{ name: "twitter:card", content: `summary_large_image` },
	],
});

// const { data } = useAsyncData(`/movies/${route.params.id}`, () =>
// {
// 	return $fetch(`http://www.omdbapi.com/?apikey=85553f5e&i=${route.params.id}`)
// }, {
// 	pick: ['Title', 'Plot'],
// 	// transform(data)
// 	// {
// 	// 	// return data.Title
// 	// 	// return {
// 	// 	// 	Plot: data.Plot,
// 	// 	// 	Title: data.Title
// 	// 	// }
// 	// }
// })
</script>

<template>
	<div>
		<pre>{{ data }}</pre>
	</div>
</template>

<style scoped></style>
