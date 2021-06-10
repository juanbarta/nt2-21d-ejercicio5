<template>

  <section class="src-components-navigator">
    <button id="reset" @click="reset()"> {{buttonMessage}}</button>
		<span id="message" :style="{ color: textColor }"> {{textMessage}} </span>
		<button id="easy" :class="{selected: isEasy}" @click="changeDifficulty($event)">easy</button>
		<button id="hard" :class="{selected: !isEasy}" @click="changeDifficulty($event)">hard</button>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-navigator',
    props: ['isRight'],
    mounted () {
      
    },
    data () {
      return {
        isEasy: false,
        textColor : "#ffffff",
        textMessage: "Try Again!",
        buttonMessage:"new colors!",
      }
    },
    methods: {
      changeDifficulty(e){
        let newisEasy;
        if (e.target.id === 'easy'){
          newisEasy = true;
        }else{
          newisEasy = false;
        }
        if (newisEasy != this.isEasy){
         this.isEasy = newisEasy;
         this.reset(); 
        }
      },
      reset(){
        this.$emit('reset', this.isEasy);
      },
    },
    watch: {
      isRight: function(){
        let change = this.isRight;
        this.buttonMessage = change? "play again!" : "new colors!"
        this.textMessage =  change? "You Picked Right!" : "Try Again!";
        this.textColor = change != null ? "#000000" : "#ffffff"
      }
    }
}


</script>

<style scoped lang="css">
  .src-components-navigator {
    background: #ffffff;
    height: 30px;
    text-align: center;
    margin: 0;
    margin-top: -30px;

  }
  button {
    border: none;
    background-color: white;
    font-family: "Montserrat", "Avenir";
    text-transform: uppercase;
    height: 100%;
    font-weight: 700;
    letter-spacing: 1px;
    color: steelblue;
    transition: all 0.3s;
    outline: none;
  }

  button:hover {
    color: white;
    background-color: steelblue;
  }

  .selected {
    background-color: steelblue;
    color: white;
  }
  #message {
    color: #000000;
    display: inline-block;
    width: 20%;
  }
</style>
