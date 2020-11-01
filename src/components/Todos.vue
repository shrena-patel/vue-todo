// You can only have one div or fragment tag in the template tag, like in React render
<template>
    <div>
        <div v-for="todo in todos" v-bind:key="todo.id"> 
            <!-- todos refers to the props that are passed in export default -->
            <!-- v-for loops through the todos props, and return a todo for each of them, like a map function -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
   
</template>

<script>

import TodoItem from './TodoItem.vue'
// This is similar to export default in react - allows you to import Todos into App component
export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"] // so we can access todos as props in the template above

}

</script>

// using scoped in the style tag limits the styling to just this component
<style scoped>

</style>