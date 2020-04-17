<template>
    <div>
        <form @submit="addAlien">
            <input type="text" v-model="name" name="name" placeholder="Add Alien...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>

export default {
    name: "AddAlien",
    data() {
        return {
            name: ''
        }
    },
    methods: {
        addAlien(e) {
            e.preventDefault();
            const newAlien = {
                name: this.name
            }
            //send up to parent
            this.$emit('add-alien', newAlien);
            this.name = '';
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
        flex: 2;
    }
</style>