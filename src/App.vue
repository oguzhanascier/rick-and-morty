<template>
  <div id="app">
    <img class="title" src="./assets/toppng.com-rick-and-morty-logo-art-of-rick-and-morty-by-justin-roiland-801x295.png" alt="">
    <div class="card">
      <ul v-for="i in item" :key="i.id">
        <li><img :src="i.image" :alt="i.name+' has no a photo on the server'" style="color:white" /></li>
        <div class="identity">
          <li><strong style="color:#496e9a">ID: </strong> {{ i.id }}</li>
          <li><strong style="color:#496e9f">GENDER:</strong> {{ i.gender }}</li>
          <li><strong style="color:#496e9f">NAME:</strong> {{ i.name }}</li>
          <li><strong style="color:#496e9f"> STATUS: </strong> {{ i.status }}</li>
          <li><strong style="color:#496e9f">SPECIES: </strong> {{ i.species }}</li>
          <li><strong style="color:#496e9f">LOCATION: </strong> {{ i.location }}</li>
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
    for (let i = 1; i < 820; i++) {
      this.num.push(i);
    }
    await this.rickAndMorty();
  },
};
</script>

<style lang="scss">
body {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  overflow-x: hidden;
  background: #131419;


}

.title{
  position: fixed;

  top: 20%;
  left:13%;
  width: 70%;
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
  background: #131419;
 
}

ul li img {
  position: absolute;
  left: 0;
  width: 200px;
  height: 300px;
  animation: anime 5s infinite;
}

.identity {
  display: flex;
  justify-content: center;
  position: absolute;
  left: 200px;
  width: 55%;
  height: 100%;
  flex-direction: column;
  color: #496e7f;
  background: #131419;
  box-shadow: -1px -1px 6px rgba(255, 255, 255, 0.1), 
  2px 2px 10px rgba(0, 0, 0, 0.2);
}

.identity li {
  padding: 10px;
  position: relative;
  margin-top: 8px;
  
}

.identity li:not(:last-child)::before{
  position: absolute;
  bottom: 0;
  content: '';
  width: 90%;
  height: 1px;
  background: #496e7f;

}

@keyframes anime {
  0%{
    // filter: blur(0.2rem);
    filter:hue-rotate(0deg);

  }
  25%{
    // filter: blur(0.2rem);
    filter:hue-rotate(120deg);

  }

  50%{
    // filter: blur(0.2rem);
    filter:hue-rotate(200deg);

  }
  75%{
    filter:hue-rotate(280deg);
    
  }
  100%{
    filter:hue-rotate(360deg);
    
  }

  
}
</style>
