<template>
  <div class="black-bg" v-if="dialogView">
    <div class="white-bg">
      <img :src="onerooms[detailnum].image" class="room-img" />
      <h4>{{ onerooms[detailnum].title }}</h4>
      <p>{{ onerooms[detailnum].content }}</p>
      <!-- <input @input="month = $event.target.value"/> -->
       <input v-model="month"/>
      <p>{{month}}개월 선택함 : {{ onerooms[detailnum].price * month}} 만원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name : 'DiaLog',
    data(){
        return{
            month : 1,
        }
    },
    watch : {
      // 첫번째 파라미터는 변경전 데이터, 두번째는 변경 후 데이터
      month(a){
        if(typeof a != 'number'){
          alert("숫자를 입력해주세요");
          a = 1;
        }
      }
    },
    props : {
      onerooms : Array,
      detailnum : Number,
      dialogView : Boolean,
    },
}
</script>

<style>

</style>