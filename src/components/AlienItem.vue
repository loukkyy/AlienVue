<template>
    <div class="alien-item">
        <div class="alien-image">
            <img :src="`http://localhost:7878${alien.image.url}`" />
        </div>
        <div class="alien-info">
            <p>
                Name: {{alien.name}}
            </p>
            
            <div class="itemList" v-bind:key="weapon._links.self.href" v-for="weapon in weapons">
                {{weapon.name}}
            </div>
        </div>
        <div class="alien-controls">
            <button @click="$emit('del-alien', alien)" class="del">x</button>
            <input type="checkbox">
        </div>
    </div>
</template>

<script>

export default {
    name: "AlienItem",
    props: ["alien", "img"],
    /*data() {
        return {
        weapons: []
        }
    },*/
    methods: {
        markComplete() {
            //this.alien.completed = !this.alien.completed;
        },
        /*loadWeapons() {
            fetch(`${alien._links.weapons.href}`)
            .then(console.log(`${alien._links.weapons.href}`))
            .then(response => response.json())
            .then(data => this.weapons = data._embedded.weapons)
            .catch(error => console.error(error));
        }*/
    }
}
</script>

<style scoped>
    .alien-item {
        background: #f4f4f4;
        padding: 10px;
        border: 2px solid  #42b983;
        overflow: hidden;
    }
    .alien-image {
        float: left;
    }

    .alien-item:hover {
        background:  #42b983;
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
    }
    .alien-controls {
        float: right;
    }
</style>