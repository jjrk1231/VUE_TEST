<template>
   <div>
    <img :src="oneroom.image" class="room-img"> <!-- rooms.image, rooms.title, rooms.price 라고 써도 됨 -->
    <h4 @click="openModal">{{oneroom.title}}</h4>
    <p>{{oneroom.price}}원</p>
    <!-- <button @click="increase0">허위매물 신고</button> <span>신고수 : {{report[0]}} </span> -->
  </div>
</template>

<script>
export default {
    name : 'Card',
    props : {
        oneroom : Object,
    },
    methods : {
      openModal() {
        this.$emit('openModal', this.oneroom.id)
      }
    }

}
</script>

<style>

</style>