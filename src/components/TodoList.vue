<template>
    <div class="container">
        <div class="add-block">
            <div class="input-wrap">
                <input type="text" v-model="newTitle" placeholder="Task name" @keyup.enter="addTodo">
            </div>
            <button @click.prevent="addTodo" class="btn-floating btn-large waves-effect waves-light red"><i
                    class="material-icons">add</i></button>
        </div>
        <transition name="fadeIn" class="filter-list">
            <div v-if="todos.length >= 2">
                <button class="waves-effect waves-light btn black" @click="filter = 'all'">All</button>
                <button class="waves-effect waves-light btn purpure" @click="filter = 'do'">Do</button>
                <button class="waves-effect waves-light btn green" @click="filter = 'done'">Done</button>
            </div>
        </transition>
        <transition-group name="fade" tag="ul" class="todo-list">
            <li class="todo-item fade" v-for="(todo, index) in todosFiltered" :key="todo.id">
                <div class="todo-holder" :class="{editing: todo.editing}">
                    <label class="todo-wrap">
                        <input type="checkbox" class="filled-in" v-model="todo.completed"/>
                        <span :class="{checked: todo.completed, hidden: todo.editing}">{{todo.title}}</span>
                        <div class="input-wrap">
                            <input v-if="todo.editing" type="text"
                                   v-model="todo.title"
                                   @change="doneEdit(todo)"
                                   @keyup.enter="doneEdit(todo)"
                                   @keyup.esc="cancelEdit(todo)"
                            >
                        </div>
                    </label>
                </div>
                <div>
                    <button class="waves-effect waves-light btn red" @click="removeTodo(index)">Delete</button>
                    <button class="waves-effect waves-light btn"
                            :disabled="todo.completed"
                            @click="editTodo(todo)">Edit
                    </button>
                </div>
            </li>
        </transition-group>
        <div class="claer-all">
            <label class="todo-wrap" v-if="todos.length >= 2">
                <input type="checkbox" class="filled-in"
                       :checked="!anyRemaining"
                       @change="checkAll"/>
                <span>Check all</span>
            </label>
            <span><strong>{{remaining}}</strong> item left</span>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'todoList',
        data() {
            return {
                newTitle: '',
                todoId: 0,
                todos: [],
                filter: 'all'
            }
        },
        computed: {

            todosFiltered() {
                if (this.filter === 'all') {
                    return this.todos
                }
                if (this.filter === 'done') {
                    return this.todos.filter(todo => todo.completed)
                }
                if (this.filter === 'do') {
                    return this.todos.filter(todo => !todo.completed)
                }
                return this.todos
            },
            remaining() {
                return this.todos.filter(todo => !todo.completed).length
            },
            anyRemaining() {
                return this.remaining != 0
            },
        },
        methods: {
            addTodo() {
                if (this.newTitle.trim().length === 0) {
                    return
                }
                this.todos.push({
                    'id': this.todoId,
                    'title': this.newTitle,
                    'completed': false,
                    'editing': false
                });
                this.newTitle = ''
                this.todoId++
            },
            removeTodo(index) {
                this.todos.splice(index, 1);
            },
            editTodo(todo) {
                this.beforeEditTitle = todo.title;
                if (!todo.completed) {
                    todo.editing = true;
                }
            },
            doneEdit(todo) {
                if (todo.title.trim().length === 0) {
                    return
                }
                todo.editing = false;
            },
            cancelEdit(todo) {
                todo.title = this.beforeEditTitle;
                todo.editing = false;
            },
            checkAll() {
                this.todos.map(todo => todo.completed = event.target.checked)
            }
        }
    }
</script>

<style lang="scss">
    .container {
        max-width: 600px;
        width: 100%;
        margin: 50px auto;
    }

    .add-block {
        display: flex;
        justify-content: space-between;
    }

    .input-wrap {
        max-width: 500px;
        width: 100%;
    }

    .todo-holder {
        position: relative;
        span {
            margin: 0;
            display: block;
            font-size: 20px !important;
            font-weight: 600;
            color: #000000;
            &.checked {
                text-decoration: line-through;
            }
            &.hidden {
                /*position: absolute;*/
                /*opacity: 0;*/
            }
        }

    }

    .todo-wrap {
        display: flex;
        align-items: center;
        & > .input-wrap {
            /*padding-right: 30px;*/
            max-width: none;
            margin-bottom: 0;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            background-color: #fff;
            input {
                border: 1px solid #a7a7a7;
                padding: 5px 10px;
                margin-bottom: 0;
                height: 20px !important;
            }
        }
        label {
            display: flex;
            align-items: center;
        }

    }

    .todo-item {
        align-items: center;
        border-top: 1px solid #ccc;
        padding: 20px 0;
        display: flex;
        justify-content: space-between;

        &:first-child {
            border-top: none;
        }
        &:last-child {
            border-bottom: 1px solid #ccc;
        }
    }

    .claer-all {
        & > span {
            float: right;
        }
        .todo-wrap {
            float: left;
        }
    }

    .fade {
        transition: all 0.3s;
    }

    .fade-enter, .fade-leave-to
        /* .card-leave-active for <2.1.8 */
    {
        opacity: 0;
        transform: scale(0);
        position: absolute;
    }

    .fade-enter-to {
        opacity: 1;
        transform: scale(1);

    }

    .fade-leave-active {
        position: absolute;
        max-width: 600px;
        width: 100%;
    }

    .fade-move {
        opacity: 1;
        transition: all 0.3s;

    }

    .fadeIn-enter-active, .fadeIn-leave-active {
        transition: opacity .5s;
    }

    .fadeIn-enter, .fadeIn-leave-to /* .fade-leave-active below version 2.1.8 */
    {
        opacity: 0;
    }
</style>