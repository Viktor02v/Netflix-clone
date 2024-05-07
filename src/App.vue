<script setup>
import { onMounted, ref } from 'vue'

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
</script>

<template>

	<div class="fixed w-full h-screen bg-black">
		<!-- Sidebar: START -->
		<div v-if="!showFullWideo" id="SideBar" class="flex z-40 items-center w-[120px] h-screen bg-black relative">
			<img class="absolute top-0 w-[35px] mt-10 ml-10" src="/images/netflix-logo.png">
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
		</div>
		<!-- Sidebar: END -->
	</div>
</template>
