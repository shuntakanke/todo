<template>
    <div>
        <form @submit="addTodo">
            <input type="text" name="title" v-model="title" placeholder="add todo">
            <input type="submit"  value="register" class="btn">
        </form>
    </div>
</template>


<script>
import { v4 as uuidv4 } from 'uuid';

export default {
    name: "AddTodo",
    data() {
        return {
            title:''
        }
    },
    methods : {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                id:uuidv4(),
                title: this.title,
                completed:false
            }
            confirm("don't you give up halfaway???")
            this.$emit('add-todo',newTodo);

            this.title ='';
        }
    }
}
</script>



<style scoped>
    form {
        display:flex;

    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }

</style>