<template>
  <div id="app">
    <div class="jumbotron">
      <Header 
        :winColor="winColor"
        :isRight="isRight"
      />
      <Navigator
        :isRight="isRight" 
        @reset="newGame($event)"
      />
      <Main
        :needReset="this.needReset"
        :isEasy="this.isEasy"
        @reseted="reseted()"
        @isRight="getResult($event)"
        @winColor="getColor($event)"
      />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Navigator from './components/Navigator.vue'
import Main from './components/Main.vue'


export default {
  name: 'App',
  components: {
    Header,
    Navigator,
    Main
  },
  data () {
    return {
      isEasy:false,
      isRight:null,
      winColor: null,
      needReset:false,
    }
  },
  methods:{
    newGame(difficulty){
      this.isRight = null;
      this.winColor = null;
      this.needReset = true;
      this.isEasy = difficulty;
    },
    getResult(e){
      this.isRight = e;
    },
    getColor(e){
      this.winColor = e;
    },
    reseted(){
      this.needReset = false;
    }
  }
}
</script>

<style>
#app {

}
body {
  background: #232323;
  margin: 0;
  font-family: "Montserrat", "Avenir";
}

h1 {
	font-weight: normal;
	line-height: 1.1;
	padding: 20px 0;

}
</style>
