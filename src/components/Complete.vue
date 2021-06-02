<template>
    <div class="complete-area">
        <h2>完了のTODO</h2>
        <ul v-for="(list, index) in completeTodos" :key="list">
            <li>{{ list }}</li>
            <button @click="myDeleteCompleteTodos(list, index)">削除</button>
        </ul>
    </div>
</template>
<script>
export default {
    props: {
        completeTodos: Array
    },
    data() {
        return {

        }
    },
    methods: {
        myDeleteCompleteTodos(value, index) {
            this.$emit("my-delete-complete-todos", value, index)
        }
    }
}
</script>