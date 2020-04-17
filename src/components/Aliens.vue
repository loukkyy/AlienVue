<template>
    <div>
        <div class="itemList" v-bind:key="alien._links.self.href" v-for="alien in aliens">
            <AlienItem v-bind:alien="alien" v-on:del-alien="$emit('del-alien', alien)" />
        </div>
    </div>
</template>

<script>
import AlienItem from './AlienItem'

export default {
    name: "Aliens",
    components: {
        AlienItem
    },
    props: ["aliens"]
}
</script>

<style scoped>
    .itemList {
        padding: 10px;
        margin: auto;
        width: 50%;
    }
</style>