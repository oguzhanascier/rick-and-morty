<template>
  <div id="app">
    <button>MORTİ</button>
    <div>
      <ul v-for="i in item" :key="i.id">
        <li>
          {{i.name}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},

  data() {
    return {
      num: [],
      item:[]
    };
  },

  created() {
    for (let i = 1; i < 250; i++) {
      this.num.push(i);
    }
    this.num.forEach((i) => {
      axios
        .get(`https://rickandmortyapi.com/api/character/${i}`)
        .then((res) => {
          let rick = res.data;

          this.item.push({
            id:rick.id,
            name:rick.name,
            status:rick.status,
            species:rick.species,
            location:rick.location.name
          })
          // this.item.id = rick.id;
          this.name = rick.name;
          // this.item.status = rick.status;
          // this.item.species = rick.species;
          // this.item.location = rick.location.name;

          console.log(this.item.status);
        });
    });
  },
};
</script>

<style lang="scss"></style>
