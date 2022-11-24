<template>
  <div id="app">
    <button>MORTİ</button>
    <div>
      <ul v-for="i in item" :key="i.id">
        <li>
          {{ i.name }}
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
      item: [
        { id: "", name: "", status: "", species: "", type: "", location: "" },
      ],
    };
  },
  created() {
    for (let i = 1; i < 800; i++) {
      this.num.push(i);
    }
    this.num.forEach((i) => {
      axios
        .get(`https://rickandmortyapi.com/api/character/${i}`)
        .then((res) => {
          let rick = res.data;
        });
    });
  },
};
</script>

<style lang="scss"></style>
