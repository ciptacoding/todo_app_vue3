<template>
	<div>
		<div class="mx-16 sm:mx-24 my-10 text-center">
			<h1 class="text-gray-700 p-4 bg-white shadow-md rounded-md font-bold text-xl uppercase">Simple Todo App</h1>
		</div>
		<div class="bg-white mx-8 p-4 shadow-md rounded-md text-lg">
			<div class="grid grid-cols-3 gap-2 mb-8">
				<input 
					@keyup.enter="add" v-model="todo" type="text" 
					class="bg-slate-100 col-span-2 border border-blue-500 p-2 rounded-md focus:outline focus:outline-cyan-500" placeholder="Masukan todo"
				>
				<button @click="add" class="bg-gradient-to-r from-cyan-500 to-blue-500 px-2 py-1 rounded-md text-white shadow-md">Add📆</button>
			</div>
			<!--mengirim data binding dari parent ke child component dan @deleteTodoList adalah emit yang dikirim dari child component-->
			<List :todos="todos" @deleteTodoList="deleteTodo" @doneTodoList="doneTodo" class="mb-6"/> 
			<small>Total Todo: {{ totalTodos }}</small>
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

		computed: {
			totalTodos(){
				return this.todos.length
			}
		},

		methods: {
			add(){
				//menambahkan / menampilkan data dari depan
				this.todos.unshift({
					activity: this.todo,
					isDone: false
				}); 
				this.todo = "" //mengosongkan form input setelah enter atau add
				this.saveToLocalStorage();
			},

			//jika index dari array todos tidak sama dengan todoIndex yang dikirim dari emit childcomponent, maka kembalikan dan tampilkan item dari setiap array todos. 
			//Jika nilai index array todos sama dengan todoIndex maka item tersebut jangan tampilkan(dihapus)
			deleteTodo(todoIndex){
				this.todos = this.todos.filter((item, index) => {
					if(index != todoIndex){ 
						return item
					}
				});
				this.saveToLocalStorage();
			},

			doneTodo(todoIndex){
				this.todos = this.todos.filter((item, index)=> {
					if(index === todoIndex){
						item.isDone = !item.isDone 
					}
					return item;
				});
				this.saveToLocalStorage();
			},

			saveToLocalStorage(){
				localStorage.setItem('todos', JSON.stringify(this.todos)); //menyimpan ke localstorage dan mengubah ke dlm bentuk string
			},			
		},

		mounted() {
			this.todos = JSON.parse(localStorage.getItem('todos')); //get todos dari localstorage dan mengubahnya ke dlm bentuk json
		},
	};
</script>