<template>
    <div>
        <form @submit="addTodo"> 
            <!-- on submit, run the addTodo method -->
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
import {v4} from 'uuid'
const uuid = v4()
export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
            // If we had more than one input type, such as email, age, name etc. you'd put those in here, then use v-model="email", v-model="age" etc. in input tag
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault()
            const newTodo = {
                id: uuid,
                title: this.title,
                completed: false
            }
            // send up to parent
            this.$emit('add-todo', newTodo)
            this.title = ''
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2
    }

</style>