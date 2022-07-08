<template>
  <div class="black-bg" v-if="isOpen == true">
    <div class="white-bg">
      <!-- 사용자가 누른 상품 번호로 보여주기 -->
      <img :src="oneroom[clicked].image" style="width: 100%" />
      <h4>{{ oneroom[clicked].title }}</h4>
      <p>{{ oneroom[clicked].content }}</p>
      <!-- @input = 입력할 때마다 실행해주세요 라는 뜻 -->
      <!-- 유저가 입력할 때마다 month에 그 값을 저장해주세요 -->
      <!-- <input @input="month = $event.target.value"> -->
      <!-- 유저가 입력한 데이터를 저장하기 -->
      <input v-model="month">
      <p>{{month}}개월 선택함 : {{ oneroom[clicked].price * month}}원</p>
      <!-- <button @click="isOpen = false">닫기</button> -->
      <!-- props로 받아온 데이터는 read-only! -->
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name : 'Modal',
    data() {
      return {
        month : 3, //문자를 입력 받을거라면 초기값을 문자로 설정해야함
      }
    },
    watch : {
      month(a) { //데이터이름으로 함수 만들고, 파라미터 추가하면 month데이터 가져다 쓸 수 있음
      //파라미터를 두개 넣으면 (변경후데이터, 변경전데이터) = (a,b)
        //month라는 데이터가 변경될 때마다 여기있는 코드가 실행됨

        //사용자가 month에 입력한 데이터가13보다 크면 경고문 띄우기
        // if(a >= 13) {
        //   alert('13이상의 숫자는 입력할 수 없습니다')
        //   this.month = 1;
        // }

        //사용자가 문자를 입력하면 경고창 띄우고 숫자 1로 바꿔버리기
        if(isNaN(a) == true) { //false일 경우 숫자, 글자일 경우 true
          alert('문자는 입력할 수 없습니다')
          this.month = 3;
        }
},
    },
    beforeUpdate() {
      if(this.month == 2) {
        alert('3이상의 숫자만 입력 가능합니다')
        this.month = 3;
      }
    },
    props : {
        oneroom : Object,
        clicked : Number,
        isOpen : Boolean,
    },
    methods : {
      closeModal() {
        this.$emit('closeModal')
      }
    }
};
</script>

<style>
</style>

