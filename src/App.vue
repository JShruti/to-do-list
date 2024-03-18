<script setup>
import {ref, onMounted, computed, watch} from'vue'

const todos = ref([])
const name = ref ('')

const input_content = ref ('')
const input_category = ref (null)

const todos_asc = computed(() => todos.value.sort((a,b) =>{
	return a.createdAt - b.createdAt
}))

watch(name, (newVal) => {
	localStorage.setItem('name', newVal)
})

onMounted(() => {
	name.value = localStorage.getItem('name') || ''
	
})
</script> 

<template>

 <main class="app">
		
		<section class="greeting">
			<h2 class="title">
				To Do List for <input type="text" id="name" placeholder="Name here" v-model="name">
			</h2>
		</section>

    <section class="create-todo">
			<h3>Make a list</h3>

			<form id="new-todo-form" @submit.prevent="addTodo">
				<h4>What's on your todo list?</h4>
				<input 
					type="text" 
					name="content" 
					id="content" 
					placeholder="e.g. to do grocery shopping"
					v-model="input_content" />
          <h4>Pick a category</h4>

          <div class ="options">
            <label>
<input 
type ="radio"
name="category"
value="business"
v-model="input_category"/>
<span class="bubble business"></span>
						<div>Business</div>


            </label>
            <label>
						<input 
							type="radio" 
							name="category" 
							id="category2" 
							value="personal"
							v-model="input_category" />
						<span class="bubble personal"></span>
						<div>Personal</div>
					</label>

          </div>

          <input type="submit" value="Add todo" />
          </form>
    </section>
    </main>
</template>
