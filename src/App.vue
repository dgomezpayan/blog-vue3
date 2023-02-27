<script setup>
	import { ref, computed, onMounted } from "vue"
	import BlogPost from "./components/BlogPost.vue"
	import PaginatePost from "./components/PaginatePost.vue"
	import LoadingSpinner from "./components/LoadingSpinner.vue"

	//variables
	const posts = ref([])
	const favorito = ref("")
	const postForPage = 10
	const indexPageInicio = ref(0)
	const indexPageFin = ref(postForPage)
  const loading = ref(false)

	//metodos
	const postFavorito = (title) => {
		favorito.value = title
	}

	const btnPrev = () => {
		indexPageInicio.value += -postForPage
		indexPageFin.value += -postForPage
	}

	const btnNext = () => {
		indexPageInicio.value += postForPage
		indexPageFin.value += postForPage
	}

  //computed
  const maxLength = computed(() => {
    return posts.value.length
  })

  onMounted(async () =>{
    loading.value = true

    try {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts")
      posts.value = await res.json()
    } catch (error) {
      console.log(error);
    } finally {
      loading.value = false
    }
  })
</script>

<template>
  <LoadingSpinner v-if="loading"/>
	<div v-else class="container">
		<br />
		<h1 class="text-center">Posts del Mes</h1>
		<h2 class="text-center">Mi Post Favorito: {{ favorito }}</h2>
		<br />
		<PaginatePost
			@prev="btnPrev"
			@next="btnNext"
			:inicio="indexPageInicio"
			:fin="indexPageFin"
      :total="maxLength"
			class="mb-2"
		/>
		<BlogPost
			v-for="post in posts.slice(indexPageInicio, indexPageFin)"
			:key="post.id"
			:title="post.title"
			:id="post.id"
			:description="post.body"
			class="mb-3"
			@postFavorito="postFavorito"
		></BlogPost>
	</div>
</template>

<style scoped></style>
