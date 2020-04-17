<template>
  <div id="app">
    <AddAlien v-on:add-alien="addAlien" />
    <Aliens v-bind:aliens="aliens" v-on:del-alien="deleteAlien" />
  </div>
</template>

<script>
import Aliens from '../components/Aliens'
import AddAlien from '../components/AddAlien'

export default {
  name: 'Home',
  components: {
    Aliens,
    AddAlien
  },
  data() {
    return {
      aliens: []
    }
  },
  methods: {
    deleteAlien(alien) {
      fetch(`${alien._links.self.href}`, {
        method: 'DELETE'
      })
      .then(this.aliens.splice(this.aliens.indexOf(alien), 1))
    },
    addAlien(newAlien) {
      fetch('http://localhost:7878/api/aliens', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(newAlien)
      })
      .then(response => response.json())
      .then(data => this.aliens = [...this.aliens, data])
      .catch(error => console.error(error));
    }
  },
  created() {
    fetch('http://localhost:7878/api/aliens')
    .then(response => response.json())
    .then(data => this.aliens = data._embedded.aliens)
    .catch(error => console.error(error));
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>