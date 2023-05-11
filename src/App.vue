<template>
	<div>
		<div class="mx-16 sm:mx-24 my-10 text-center">
			<h1 class="text-gray-700 p-4 bg-white shadow-md rounded-md font-bold text-xl uppercase">Simple Todo App</h1>
		</div>
		<div class="bg-white mx-8 p-4 shadow-md rounded-md text-lg">
			<div class="grid grid-cols-3 gap-2">
				<input 
					@keyup.enter="add" v-model="todo" type="text" 
					class="bg-slate-100 col-span-2 border border-blue-500 p-2 rounded-md focus:outline focus:outline-cyan-500" placeholder="Masukan todo"
				>
				<button @click="add" class="bg-gradient-to-r from-cyan-500 to-blue-500 px-2 py-1 rounded-md text-white shadow-md">Add📆</button>
			</div>
			<List :todos="todos"/> <!--mengirim data binding dari parent ke child component-->
		</div>
	</div>
</template>

<script>
	import List from './components/List.vue';
	export default{
		components: {List},
		data(){
			return {
				todo: '',
				todos: []
			}
		},
		methods: {
			add(){
				this.todos.push(this.todo);
				this.todo = "" //mengosongkan form input setelah enter atau add
			}
		}
	}
</script>