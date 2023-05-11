<template>
	<ul>
		<li v-for="(todo, index) in todos" :key="index">{{ index+1 }}. {{ todo }}</li>
	</ul>
</template>

<script>
	export default{
		props: {
			todos: {
				type: Array,
				default: []
			}
		}
	}
</script>