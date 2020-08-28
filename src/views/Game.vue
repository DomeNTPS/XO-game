<template>
  <div class="game">
    <h1>This is Game page </h1>
    
  <div class="game-field">
    <div v-for="(item, index) in box" :key="index">
      <button class="game-box" v-if="item.label == ''" :disabled="index == Number(randomInt)" @click="handlePlay(index)">
        {{item.label}}
      </button>
      <button class="game-box" v-else :disabled="true" @click="handlePlay(index)">
        {{item.label}}
      </button>
    </div>
  </div>
  <modal class="modal" v-if="showModal" >
        <div class="modal-box">
          <div class="end">Game End</div>
          <div class="enter">Enter name to record score</div>
          <div>
            <input class="input" v-model="newName">
          </div>
             <router-link to="/score">
             <button class="submit" @click="addName">
                    Submit
             </button>
             </router-link>
        </div>
  </modal>
      <div>
        <button @click="handleRefresh()">Restart</button>
      </div>
  </div>
  
</template>


       

<script>
export default {
  //
    data() {
      return {
        box: [{'label':''},{'label':''},{'label':''},{'label':''},
        {'label':''},{'label':''},{'label':''},{'label':''},
        {'label':''},{'label':''},{'label':''},{'label':''},
        {'label':''},{'label':''},{'label':''},{'label':''}],
        current : '',
        wincondition : [[0,1,2,3],[4,5,6,7],[8,9,10,11],[12,13,14,15],[0,4,8,12],
                        [1,5,9,13],[2,6,10,14],[3,7,11,15],[0,5,10,15],[3,6,9,12]],
        name: [],
        newName: '',
        scoreShow: [],
        scorexo: 0,
        showModal: false,
        randomInt : sessionStorage.getItem('randomNum')
      }
    },
    
     mounted() {
       sessionStorage.getItem('randomNum')
       if (sessionStorage.getItem('name')) {
          this.name = sessionStorage.getItem('name').split(',')
       }
       if (sessionStorage.getItem('scores')) {
          this.scoreShow = sessionStorage.getItem('scores').split(',')
       }
    },

    methods: {
      handleRefresh(){
        location.reload()
      },
      handlePlay(index) {
       if (this.current === 'X') {
          this.current = 'O'
        }
        else {
          this.current = 'X'
        }
        this.box[index].label = this.current
        this.win(index)
      },
      addName() {
        if (!this.newName) {
          return;
        }    
        this.name.push(this.newName)
        this.scoreShow.push(this.scorexo)
        sessionStorage.setItem("name", this.name)
        sessionStorage.setItem("scores", this.scoreShow)
      },
      win() {
          let mark
          for (let i = 0; i < this.wincondition.length; i++) {
            mark = 'X'
            let j = 0
            if (this.box[this.wincondition[i][j]].label === mark && this.box[this.wincondition[i][j+1]].label === mark && this.box[this.wincondition[i][j+2]].label === mark && this.box[this.wincondition[i][j+3]].label === mark ) {
              this.countScore()
              this.showModal = true
              break 
            }  
          }
          for (let i = 0; i < this.wincondition.length; i++) {
            mark = 'O'
            let j = 0
            if (this.box[this.wincondition[i][j]].label === mark && this.box[this.wincondition[i][j+1]].label === mark && this.box[this.wincondition[i][j+2]].label === mark && this.box[this.wincondition[i][j+3]].label === mark ) {
              this.countScore()
              this.showModal = true
              break 
            }  
          }
      },
      countScore() {
        this.box.map((score) => {
          if (score.label == '') this.scorexo++
        })
      }
    },
}

</script>

<style>

.game-field {
  /* border: 1px salmon solid; */
  width: 765px;
  /* height: 1000px; */
  margin: auto;
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
  box-sizing: border-box;
  /* background-color: salmon; */
}
.game-box {
  border: 1px burlywood solid;
  width: 170px;
  height: 170px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: cursive;
  font-size: 50px;
  text-transform: uppercase;
  border-radius: 10px;
  cursor: pointer;
  margin: 10px;
  background-color: antiquewhite;
}
.game-box:disabled{
   border: 1px burlywood solid;
  width: 170px;
  height: 170px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: cursive;
  font-size: 50px;
  text-transform: uppercase;
  border-radius: 10px;
  cursor: pointer;
  margin: 10px;
  background-color: gray;
}
.modal-box {
  height: 700px;
  width: 700px;
  background-color: darksalmon;
  position: absolute;
  margin-top: 50px;
  justify-self: center;
  border-radius: 20px;
}
.input {
   margin-top: 50px;
   border: 1px burlywood solid;
   background-color: whitesmoke;
   border: 3px black;
   height: 60px;
   width: 400px;
   
}
.submit{
  margin-top: 70px;
  background-color: papayawhip;
  color: black;
  height: 70px;
  width: 130px;
  font: 60px;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
.end {
  margin-top: 60px;
  color: black;
  /* background-color: wheat; */
  font: 80px sans-serif;
}
.enter {
  margin-top: 70px;
  color: black; 
  /* background-color: wheat; */
  font: 50px sans-serif;
}
.modal {
  position: absolute;
  top: 130px;
  left: 600px;
}
</style>