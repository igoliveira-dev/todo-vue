<script setup>
    const props = defineProps({
        tarefas: {
            type: Array,
            required: true
        },
        filtro: {
            type: String
        }
    })
</script>

<template>
    <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.título" type="checkbox" name="" id="">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.título">
                {{ tarefa.título }}
            </label>
        </li>
    </ul>
    <p class="mt-5" v-else>Você não possui tarefas {{ filtro }}</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
