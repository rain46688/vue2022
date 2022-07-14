<template>
    <div>
    <img :src="onerooms.image" class="room-img" />
    <h4 @click="$emit('openModal', onerooms.id)">{{ onerooms.title }}</h4>
    <p>{{ onerooms.price }} 만원</p>
  </div>
</template>

<script>
export default {
    name : 'CardComp',
    props : {
      onerooms : Object,
    },
}
</script>

<style>

</style>