<template>
  <div id="app">
    <button>MORTİ</button>
    <div>
      <ul v-for="i in item" :key="i.id">
        <li>
          {{ i.name }}
          {{ i.id }}
          {{ i.status }}
          {{ i.species }}
          {{ i.location }}
          {{ i.gender }}
          <img :src="i.image" alt="" />
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
      item: [],
    };
  },

  methods: {
    async rickAndMorty() {
      await this.num.forEach((i) => {
        axios
          .get(`https://rickandmortyapi.com/api/character/${i}`)
          .then((res) => {
            let rick = res.data;

            this.item.push({
              id: rick.id,
              name: rick.name,
              status: rick.status,
              species: rick.species,
              location: rick.location.name,
              gender: rick.gender,
              image: rick.image,
            });
            console.log(rick);
          });
      });
    },
  },

  async created() {
    for (let i = 1; i < 850; i++) {
      this.num.push(i);
    }
   await this.rickAndMorty();
  },
};
</script>

<style lang="scss"></style>
