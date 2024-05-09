<script setup>
import { onMounted, ref } from 'vue'
import movies from './movies.json'

import MovieDatails from './components/MovieDetails.vue';
import VideoCarousel from './components/VideoCarousel.vue';

import Magnify from 'vue-material-design-icons/Magnify.vue';
import HomeOutline from 'vue-material-design-icons/HomeOutline.vue';
import TrendingUp from 'vue-material-design-icons/TrendingUp.vue';
import Television from 'vue-material-design-icons/Television.vue';
import MovieOutline from 'vue-material-design-icons/MovieOutline.vue';
import Plus from 'vue-material-design-icons/Plus.vue';
import ChevronLeft from 'vue-material-design-icons/ChevronLeft.vue';

import { useMovieStore } from './stores/movie';
import { storeToRefs } from 'pinia';
const useMovie = useMovieStore();
const { movie, showFullWideo } = storeToRefs(useMovie);

onMounted(() => {
	setTimeout(() => movie.value = movies[0][0], 100)
})
</script>

<template>

	<div class="fixed w-full h-screen bg-black">
		<!-- Sidebar: START -->
		<div v-if="!showFullWideo" id="SideBar" class="flex z-40 items-center w-[120px] h-screen bg-black relative">
			<img class="absolute top-0 w-[35px] mt-10 ml-10" src="/images/netflix-logo.png">
			<!-- Section With The Icons: START -->
			<div>
				<div class="py-2 mx-10 my-6 ">
					<Magnify fillColor="white" :size="40" class="cursor-pointer" />
				</div>
				<div class="py-2 mx-10 my-6 border-b-4 border-b-red-500">
					<HomeOutline fillColor="white" :size="40" class="cursor-pointer" />
				</div>
				<div class="py-2 mx-10 my-6 ">
					<TrendingUp fillColor="white" :size="40" class="cursor-pointer" />
				</div>
				<div class="py-2 mx-10 my-6 ">
					<Television fillColor="white" :size="40" class="cursor-pointer" />
				</div>
				<div class="py-2 mx-10 my-6 ">
					<MovieOutline fillColor="white" :size="40" class="cursor-pointer" />
				</div>
				<div class="py-2 mx-10 my-6 ">
					<Plus fillColor="white" :size="40" class="cursor-pointer" />
				</div>
			</div>
			<!-- Section With The Icons: END -->
		</div>
		<!-- Sidebar: END -->

		<!-- Section with the movie: START -->
		<div v-if="!showFullWideo">
			<div class="fixed flex z-20 top-0 right-0 w-full h-[50%] bg-black pl-[120px] bg-clip-border">

				<!-- Gradient: START -->
				<div
					class="absolute z-30 h-[600px] left-[120px] w-[77%] right-0 top-0 bg-gradient-to-r from-black via-black" />
				<!--  Gradient: END -->

				<!-- Movie Details: START -->
				<MovieDatails v-if="movie" :movie="movie" />
				<!-- Movie Details: END -->

				<!-- Video: START -->
				<video v-if="movie" :src="'/videos/' + movie.name + '.mp4'" class="absolute z-0 h-[600px] right-0 top-0"
					autoplay loop />
				<!-- Video: END -->

				<!-- Carousel: START -->
				<div class="fixed z-30 bottom-0 right-0 w-full h-[55%] pl-[120px] overflow-y-auto">
					<VideoCarousel class="pb-14 pt-14" category="Popular Movies" :movies="movies[0]" />
					<VideoCarousel class="pb-14 pt-14" category="Horror Movies" :movies="movies[1]" />
					<VideoCarousel class="pb-32 pt-14" category="Featured Movies" :movies="movies[2]" />
				</div>
				<!-- Carousel: END -->
			</div>
		</div>
		<!-- Section with the movie: END -->

		<!-- Full Screen Video Section: START -->
		<div v-if="showFullWideo">
			<div @click="showFullWideo = false"
				class="absolute z-50 p-2 m-4 bg-white bg-opacity-50 rounded-full cursor-pointer">
				<ChevronLeft fillColor="white" :size="40" />
			</div>
			<video v-if="movie" :src="'/videos/' + movie.name + '.mp4'" class="absolute z-0 w-[100vw] h-full object-fit"
				autoplay controls loop />
		</div>
		<!-- Full Screen Video Section: END -->
	</div>
</template>
