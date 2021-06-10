<template>

  <section class="src-components-main">
    <Square v-for="(color, index) in colors"
      :key="index"
      :id="index"
      :color="color"
      @clickedColor="clickedColor($event)"
    />
  </section>
</template>

<script lang="js">
import Square from './Square.vue'

  export default  {
    name: 'src-components-main',
    props: ['isEasy','needReset'],
    components:{
      Square
    },
    mounted(){
      this.init();
    },
    data () {
      return {
          easyAmmount: 3,
          hardAmmount: 6,
          colors: [],
      }
    },
    methods: {
      pickColor(){
        return Math.floor(Math.random() * this.ammount );
      },

      clickedColor(clickedColor){
        let isRight= false;
        if (this.colors[clickedColor] === this.colors[this.pickedColor]) {
          isRight = true;
          this.setAllColorsTo();
        } else {
          this.colors.splice(clickedColor, 1, "#232323")
        }
        this.$emit('isRight', isRight);
      },
      createNewColors(){
        var arr = [];
        for (var i = 0; i < this.ammount; i++) {
          arr.push(this.createRandomStringColor());
        }
        return arr;
      },

      setAllColorsTo(){
        for (var i = 0; i < this.ammount; i++) {
          this.colors.splice(i, 1, this.colors[this.pickedColor]);
        }
      },
    
      createRandomStringColor(){
        var newColor = "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")" ;
        return newColor;
      },

      randomInt(){
        return Math.floor(Math.random() * 256);
      },

      init(){
        this.ammount = this.isEasy? this.easyAmmount : this.hardAmmount;
        this.colors = this.createNewColors();
        this.pickedColor = this.pickColor();
        this.$emit('winColor', this.colors[this.pickedColor]);
      }
    },
    watch: {
      needReset: function() {
        this.init();
        this.$emit('reseted');
      }
    }
}


</script>

<style scoped lang="css">
  .src-components-main {
  margin: 20px auto;
	max-width: 600px;
  }
</style>
