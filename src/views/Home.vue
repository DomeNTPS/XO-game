<template>
  <div class="home">
    random space is : {{ran}} to disable.
      <div class="head">
      XO Game
      </div>
    <div>
      <router-link to="/game">
      <button class="start"  @click="handleRan">
        Start Game !
      </button>
    </router-link>
    </div>
  </div>
</template>

<script>



export default {
  
   data() {
    return {
      ran : Math.floor(Math.random() * 16),
      rand : []
    }
  },
  methods: {
      handleRan() {
      this.rand.push(this.ran)  
      sessionStorage.setItem("randomNum", this.ran)
      },
  }
}
</script>

<style>

@keyframes ex {

  0%
  { color: #f89; }
  50% 
  { color: #faf; }
  100% 
  { color: #ada; }

}
.head {
  margin-top: 180px;
  font-size: 90px;
  color: transparent;
  background-clip: text;
  animation-name: ex;
  animation-duration: 10s;
  animation-iteration-count: infinite
 
}
.start {
  margin-top: 170px;
  background-color: aquamarine;
  height: 130px;
  width: 20pc;
  border-radius: 100px;
  font-size: 20px;
}
.start:hover {
  color:gold;
  background-color: chocolate;
}



</style>