<script setup>
  defineProps(['inicio', 'fin', 'total'])
	const emit = defineEmits(["next", "prev"])
</script>

<template>
	<div class="btn-group" role="group" data-bs-toggle="buttons">
		<button
			@click="emit('prev')"
			type="button"
			class="btn btn-primary"
			:disabled="inicio === 0"
		>
			Prev
		</button>
		<button
			@click="emit('next')"
			type="button"
			class="btn btn-primary"
			:disabled="fin >= total"
		>
			Next
		</button>
	</div>
</template>
