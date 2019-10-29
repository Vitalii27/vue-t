<!--<template>-->
    <!--<div>-->
    <!--<div class="todo-holder" :class="{editing: editing}">-->
        <!--<label class="todo-wrap">-->
            <!--<input type="checkbox" class="filled-in" v-model="completed"/>-->
            <!--<span :class="{checked: completed, hidden: editing}">{{title}}</span>-->
            <!--<div class="input-wrap">-->
                <!--<input v-if="editing" type="text"-->
                       <!--v-model="title" >-->
                       <!--&lt;!&ndash;@change="doneEdit()"&ndash;&gt;-->
                       <!--&lt;!&ndash;@keyup.enter="doneEdit()"&ndash;&gt;-->
                       <!--&lt;!&ndash;@keyup.esc="cancelEdit()"&ndash;&gt;-->
            <!--</div>-->
        <!--</label>-->
    <!--</div>-->
    <!--<div>-->
        <!--<button class="waves-effect waves-light btn red" @click="removeTodo(index)">Delete</button>-->
        <!--<button class="waves-effect waves-light btn"-->
                <!--:disabled="completed"-->
                <!--@click="doneTodo()">-->
        <!--Edit-->
        <!--</button>-->
    <!--</div>-->
    <!--</div>-->
<!--</template>-->
<!--<script>-->
    <!--export default {-->
        <!--name: 'todo-item',-->
        <!--props: {-->
            <!--todo: {-->
                <!--type: Object,-->
                <!--required: true-->
            <!--},-->
            <!--index:{-->
                <!--type: Number,-->
                <!--required: true-->
            <!--}-->

        <!--},-->
        <!--data(){-->
            <!--return{-->
                <!--'id': this.todo.id,-->
                <!--'title': this.todo.title,-->
                <!--'completed': this.todo.completed,-->
                <!--'editing': this.todo.editing-->
            <!--}-->
        <!--},-->
        <!--methods:{-->
            <!--removeTodo(index){-->
                <!--this.$emit('remove', index)-->
            <!--},-->
            <!--editTodo() {-->
                <!--if (this.title.trim().length === 0) {-->
                    <!--return-->
                <!--}-->
                <!--this.editing = false;-->
            <!--},-->
            <!--doneTodo() {-->
                <!--this.beforeEditTitle = this.title;-->
                <!--if (this.completed) {-->
                    <!--this.editing = false;-->
                <!--}-->
                <!--this.editing = true;-->
                <!--this.$emit('finishedEdit', {-->
                    <!--'index': this.index,-->
                    <!--'todo':{-->
                        <!--'id': this.id,-->
                        <!--'title': this.title,-->
                        <!--'completed': this.completed,-->
                        <!--'editing': this.editing-->
                    <!--}-->
                <!--})-->

            <!--},-->
        <!--},-->
        <!--computed:{-->

        <!--}-->
    <!--}-->
<!--</script>-->
<!--<style></style>-->