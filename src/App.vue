<template>

  <DiaLog @closeModal="dialogView = false" :onerooms="onerooms" :detailnum="detailnum" :dialogView="dialogView" />

  <DisCount />

  <div class="menu">
    <a v-for="(data, num) in menus" :key="num">{{ data }}</a>
  </div>

  <CardComp @openModal="dialogView = true; detailnum=$event" :onerooms="data" v-for="(data, num) in onerooms" :key="num" />

</template>

<script>

import importdata from './assets/oneroom.js';
import DisCount from './components/DisCount.vue';
import DiaLog from './components/DiaLog.vue';
import CardComp from './components/CardComp.vue';

export default {
  name: 'App',
  data() {
    return {
      menus: ['Home', 'Shop', 'About'],
      products: [
        { title: '역삼동원룸', price: 50, 신고수: 0, image: require("./assets/room0.jpg") },
        { title: '천호동원룸', price: 60, 신고수: 0, image: require("./assets/room1.jpg") },
        { title: '마포구원룸', price: 70, 신고수: 0, image: require("./assets/room2.jpg") }
      ],
      dialogView: false,
      onerooms: importdata,
      detailnum: 0,
    }
  },
  methods: {
    increase(data) {
      console.log(data);
      data.신고수 += 1
    }
  },
  components: {
    DisCount: DisCount,
    DiaLog: DiaLog,
    CardComp: CardComp,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>
