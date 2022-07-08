<template>
  <!-- class명을 조건부로 넣으려면 {클래스명 : 조건} -->
  <!-- isOpen이 true가 되면 class에 end 부착 -->
  <!-- <div class="start" :class="{ end : isOpen }"> -->


  <transition name="fade">
    <Modal @closeModal="isOpen = false" :oneroom="oneroom" :clicked="clicked" :isOpen="isOpen"/>
  </transition>
  <!-- </div> -->
  <div class="menu">
    <a v-for="a in menu" :key="a"> {{a}} </a>
  </div>
  
  <Discount v-if="showDiscount == true" :percent="percent"/>

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <button @click="priceReSort">가격역순정렬</button>

  <Card @openModal="isOpen = true; clicked = $event" :oneroom="oneroom[i]" v-for="(a, i) in oneroom" :key="a"/>

  <!-- <div>
    <img :src="oneroom[a].image" class="room-img">
    <h4 @click="isOpen = true">{{oneroom[0].title}}</h4>
    <p>{{oneroom[0].price}}</p>
    <button @click="increase0">허위매물 신고</button> <span>신고수 : {{report[0]}} </span> 
  </div> -->
  <!-- <div> 
    <img :src="oneroom[1].image" class="room-img">
    <h4 @click="isOpen = true">{{oneroom[1].title}}</h4>
    <p>{{oneroom[1].price}}</p>
    <button @click="increase1">허위매물 신고</button> <span>신고수 : {{report[1]}} </span>
  </div>
  <div>
    <img :src="oneroom[2].image" class="room-img">
    <h4 @click="isOpen = true">{{oneroom[2].title}}</h4>
    <p>{{oneroom[2].price}}</p>
    <button @click="increase2">허위매물 신고</button> <span>신고수 : {{report[2]}} </span>
  </div> -->
    
    <!-- <div v-for="(a,i) in products" :key="i">
    <h4>{{products[i]}}</h4>
    <p>70만원</p> -->
</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data() {
    return {
      //데이터는 object자료로 저장
      // {자료이름: 자료내용}
      percent : 30,
      showDiscount : true,
      oneroomOrigin : [...data],
      clicked : 0,
      oneroom : data, 
      isOpen : false,
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      menu : ['Home', 'Products', 'About'],
      report : [0,0,0],
    };
  },

  methods : {
    priceSort() {
      this.oneroom.sort(function(a,b) {
        return a.price - b.price;
      })
    },
    priceReSort() {
      this.oneroom.sort(function(a,b) {
        return b.price - a.price;
      })
    },
    sortBack() {
      this.oneroom = [...this.oneroomOrigin];
      //array의 shallow copy를 만들어서 집어넣어주세요.
    },
  },
    //lifecycle hook을 활용
    mounted() { //컴포넌트가 html에 장착돼서 화면에 보이는 상태
      //mount되고 나서 실행
      // setTimeout(()=> {
      //  this.showDiscount = false; 
      // } , 2000);

      setInterval(()=> {
          this.percent--;
      }, 1000);


    },


    // increase0() {
    //   this.report[0] += 1;
    //   //함수 안에서 데이터 사용할 때 무조건 this.써야함
    // },
    // increase1() {
    //   this.report[1] += 1;
    //   //함수 안에서 데이터 사용할 때 무조건 this.써야함
    // },  
    // increase2() {
    //   this.report[2] += 1;
    //   //함수 안에서 데이터 사용할 때 무조건 this.써야함
    // }
    components : {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  },
};
</script>

<style>
body {
  margin: 0;
}

div{
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}

.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;  
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: rgb(133, 193, 80);
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}

</style>
