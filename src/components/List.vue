<template>
	<ul>
		<li v-for="(todo, index) in todos" :key="index" class="my-2 flex justify-between">
			<div v-if="todo.isDone">
				<del>{{ index+1 }}. {{ todo.activity }}</del>
			</div>
			<div v-else>
				<span>{{ index+1 }}. {{ todo.activity }}</span>
			</div>
			<div class="flex gap-4">
				<button @click="doneTodo(index)">✅</button>
				<button @click="deleteTodo(index)">❌</button>
			</div>
		</li>
	</ul>
</template>

<script>
	export default{
		//menyiapkan props untuk menerima data todos dari parent
		props: {
			todos: {
				type: Array,
				default: []
			}
		},
		methods: {
			deleteTodo(index){
				this.$emit('deleteTodoList', index);
			},
			
			doneTodo(index){
				this.$emit('doneTodoList', index); 
				//parameter pertama nama emit untuk dipanggil di parent dan parameter kedua adalah value yang dikirim
			}
		}
	}
</script>