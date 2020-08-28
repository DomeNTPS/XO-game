<template>
  <div class="score">
    <div class="head"><h1>This is Score page</h1></div>
      <div class="table" v-for="(item, index) in names" :key="index">
        <div>
          {{names[index]}}
          {{scores[index]}}
        </div>
      </div>
    </div>
</template>

<script>

export default {
  
  data() {
    return {
      names  : sessionStorage.getItem('name').split(','),
      scores : sessionStorage.getItem("scores").split(','),
    }
  },

  methods: {
    addName() {
      
        console.log(this.names)
        console.log(sessionStorage.getItem("scores"))
      },
  },
}
</script>

<style>

.table {
  margin-top: 15px;
}
.head {
  margin-bottom: 30px;
}
</style>