<template>
    <section>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem, index) in storedTodoItems" :key="todoItem">
                <i @click="toggleComplete(todoItem, index)" v-bind:class="{checkBtnCompleted: todoItem.completed}" class="checkBtn fas fa-check" aria-hidden="true"></i>
                <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <span class="removeBtn" type="button" @click="removeOneItem({todoItem, index})">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>

<script>
import {mapGetters, mapMutations} from 'vuex'

export default {
    computed: {
        // todoItems() {
        //     return this.$store.getters.storedTodoItems
        // },
        ...mapGetters(['storedTodoItems'])
        // getters에서 사용할 이름과 컴포넌트에서 사용할 이름이 다를 때
        // ...mapGetters({
        //     'storedTodoItems'
        // })
    },
    methods: {
        // ...mapMutations({
        //     removeTodo: 'removeOneItem'
        // }),
        ...mapMutations(['removeOneItem']),
        // removeTodo(todoItem, index) {
        //     this.$store.commit('removeOneItem', {todoItem, index});
        // },
        toggleComplete(todoItem, index) {
            this.$store.commit('toggleOneItem', {todoItem, index});
        }
    }
}
</script>

<style scoped>
    ul {
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
        cursor: pointer;
    }
    .removeBtn {
        margin-left: auto;
        color: #de4343;
        cursor: pointer;
    }
    .checkBtnCompleted {
        color: #b3adad;
    }
    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }

    .list-move,
    .list-enter-active,
    .list-leave-active {
        transition: all 1s cubic-bezier(0.55, 0, 0.1, 1);
    }
    .list-enter-form,
    .list-leave-to {
        opacity: 0;
        transform: translateX(30px);
    }
    .list-enter-active {
        position: absolute;
        transition: all 1s;
    }
</style>