<template>

  <section class="src-components-header" :style="{backgroundColor: won}">
    <h1>The Great <br><span id="colorDisplay">{{winColor}}</span><br>Guessing Game</h1>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-header',
    props: ['winColor', 'isRight'],
    mounted () {

    },
    data () {
      return {
      }
    },
    methods: {

    },
    computed: {
      won: function(){
        return this.isRight? this.winColor : "steelblue";
      }
    }
}


</script>

<style scoped lang="css">
  .src-components-header {
    transition: all 0.3s;
    background: steelblue;
    text-transform: uppercase;
    text-align: center;
    margin: 0;
    color: white;

  }


  #colorDisplay {
	font-size: 200%;
}

</style>
