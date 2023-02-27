<script setup>
	defineProps({
		title: String,
		id: Number,
		description: {
			type: String,
			default: "Sin descripcion en el post",
		},
	})

	const emit = defineEmits(["postFavorito"])
</script>

<template>
	<div class="card">
		<div class="card-body">
			<h5 class="card-title">{{ id }} - {{ title }}</h5>
			<p>{{ description }}</p>
			<button
				@click="emit('postFavorito', `Post ${id}`)"
				class="btn btn-sm btn-outline-primary"
			>
				Favorito
			</button>
		</div>
	</div>
</template>
