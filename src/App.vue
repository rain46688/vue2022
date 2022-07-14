<template>

  <transition name="fade">
    <DiaLog @closeModal="dialogView = false" :onerooms="onerooms" :detailnum="detailnum" :dialogView="dialogView" />
  </transition>


  <div class="menu">
    <a v-for="(data, num) in menus" :key="num">{{ data }}</a>
  </div>

  <DisCount :disprice="disprice" v-if="showDiscount == true" />

  <button @click="titleAscSort">이름 오름차순 정렬</button>
  <button @click="titleDesSort">이름 내림차순 정렬</button>
  <button @click="priceAscSort">가격 오름차순 정렬</button>
  <button @click="priceDesSort">가격 내림차순 정렬</button>
  <br />
  <br />
  <button @click="priceBack">되돌리기</button>

  <CardComp @openModal="dialogView = true; detailnum = $event" :onerooms="data" v-for="(data, num) in onerooms"
    :key="num" />

</template>

<script>

import importdata from './assets/oneroom.js';
import DisCount from './components/DisCount.vue';
import DiaLog from './components/DiaLog.vue';
import CardComp from './components/CardComp.vue';

export default {
  name: 'App',

  // 데이터들
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
      // sort 함수를 사용하면 원본 배열이 변형되므로 기존 데이터를 먼저 origin에 복원해두려고함
      // 하지만 그냥 넣을 경우에는 복사가되는게 아니라 서로 같은 메모리 값을 공유하기 때문에
      // oneroomsOrigin: [...importdata], 이런 방식으로 아예 딥카피를 해줘야됨
      oneroomsOrigin: [...importdata],
      detailnum: 0,
      showDiscount: true,
      disprice : 30,


    }
  },

  // 함수들
  methods: {
    increase(data) {
      console.log(data);
      data.신고수 += 1
    },
    // 숫자 오름차순
    priceAscSort() {
      this.onerooms.sort(function (a, b) {
        return a.price - b.price;
      })
    },
    // 숫자 내침차순
    priceDesSort() {
      this.onerooms.sort(function (a, b) {
        return b.price - a.price;
      })
    },
    // 문자 오름차순
    titleAscSort() {
      this.onerooms.sort(function (a, b) {
        if (a.title < b.title) return -1;
        if (a.title > b.title) return 1;
        if (a.title === b.title) return 0;
      });
    },
    // 문자 내림차순
    titleDesSort() {
      this.onerooms.sort(function (a, b) {
        if (a.title < b.title) return 1;
        if (a.title > b.title) return -1;
        if (a.title === b.title) return 0;
      });
    },
    // 되돌리기
    priceBack() {
      // 여기도 배열 끼리의 =는 대입이 아니라 서로 같은 메모리 값을 공유해달라는거라서
      // [...this.oneroomsOrigin] 딥카피를해서 넣어줘야됨
      this.onerooms = [...this.oneroomsOrigin];
    },
  },

  // 라이프 사이클

  crated() {
    // ajax 사용해서 서버에서 데이터 가져올때 crated, mounted에서 로직 수행함
    console.log("crated");
  },
  beforeCreate() {
    console.log("beforeCreate");
    // 1초마다 실행해서 할인 가격 떨구기
    setInterval(() => {
      this.disprice--;
    }, 1000);
  },
  beforeMount() {
    console.log("beforeMount");
  },

  mounted() {
    // 라이프 사이클중 마운트 후에 2초 정도 후에 배너를 닫아달라
    // setTimeout(() => {
    //   this.showDiscount = false;
    // }, 2000);
  },
  beforeUpdate() {
    console.log("beforeUpdate");
  },
  updated() {
    console.log("updated");
  },
  beforeUnmount() {
    console.log("beforeUnmount");
  },
  unmounted() {
    console.log("unmounted");
  },

  // 컴포넌트
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

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 0.3s;
}

.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  transform: translateY(0px);
}

.fade-leave-active {
  transition: all 0.3s;
}

.fade-leave-to {
  transform: translateY(-1000px);
}
</style>
