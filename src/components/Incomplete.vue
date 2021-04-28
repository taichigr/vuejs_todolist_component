<template>
    <div class="incomplete-area">
        <h2>未完了のTODO</h2>
        <ul v-for="list in incompleteTodos" :key="list">
            <li>{{ list }}</li>
            <button @click="emitMoveToComplete(list)">完了へ</button>
            <button @click="emitMoveToHoryu(list)">保留へ</button>
            <button @click="emitDeleteIncompleteTodos(list)">削除</button>
        </ul>
    </div>
</template>
<script>
    export default {
        props: {
            incompleteTodos: Array
        },
        data() {
            return {

            }
        },
        methods: {
            emitMoveToComplete(value) {
                this.$emit("my-move-to-complete", value)
            },
            emitMoveToHoryu(value) {
                this.$emit('my-move-to-horyu', value)
            },
            emitDeleteIncompleteTodos(value) {
                this.$emit('my-delete-incomplete-todos', value)
            }
        }
    }
</script>