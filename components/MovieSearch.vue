<script setup>
const query = ref('batman');
const movies = ref([]);

const search = async () =>
{
	const { Search } = await $fetch(`https://www.omdbapi.com/?apikey=85553f5e&s=${query.value}`);
	movies.value = Search || [];
}

search();
</script>

<template>
	<section>
		<h1>Movies page</h1>
		<form @submit.prevent="search">
			<input type="text" v-model="query">
			<button>Search</button>
		</form>
		<ul v-if="movies.length" class="movies">
			<li v-for="movie in movies" :key="movie.imdbID">
				<NuxtLink :to="{ name: 'movies-id', params: { id: movie.imdbID } }">
					<NuxtImg :src="movie.Poster" :alt="movie.Title" width="300" fit="cover" format="webp" loading="lazy" />
				</NuxtLink>
			</li>
		</ul>
	</section>
</template>

<style scoped>
.movies {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: 10px;
	list-style: none;
}

.movies a {
	display: block;
	height: 100%;
}
</style>
