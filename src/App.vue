<template>
  <div id="app">
    <button>MORTİ</button>
    <div class="card">
      <ul v-for="i in item" :key="i.id">
        <li><img :src="i.image" alt="" /></li>
        <div class="identity">
          <li><strong>ID: </strong> {{ i.id }}</li>
          <li><strong>GENDER:</strong> {{ i.gender }}</li>
          <li><strong>NAME:</strong> {{ i.name }}</li>
          <li><strong> STATUS: </strong> {{ i.status }}</li>
          <li><strong>SPECIES: </strong> {{ i.species }}</li>
          <li><strong>LOCATION: </strong> {{ i.location }}</li>
        </div>
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
    for (let i = 1; i < 10; i++) {
      this.num.push(i);
    }
    await this.rickAndMorty();
  },
};
</script>

<style lang="scss">
body {
  display: flex;
  flex-wrap: wrap;
  overflow-x: hidden;
}

.card {
  display: flex;
  justify-content: center;

  width: 100vw;
  flex-wrap: wrap;
}

ul {
  display: flex;
  flex-direction: column;
  position: relative;
  justify-content: start;
  width: 410px;
  height: 300px;
  margin: 20px;
  list-style-type: none;
  background: #3cab;
}

ul li img {
  position: absolute;
  left: 0;
  width: 200px;
  height: 300px;
}

.identity {
  display: flex;
  justify-content: center;
  position: absolute;
  left: 200px;
  width: 55%;
  flex-direction: column;
}

.identity li {
  padding: 10px;
  margin-top: 8px;
  box-shadow: -1px -1px 3px rgba(175, 237, 223, 0.733),
    1px 1px 3px rgba(79, 147, 132, 0.733);
}
</style>
