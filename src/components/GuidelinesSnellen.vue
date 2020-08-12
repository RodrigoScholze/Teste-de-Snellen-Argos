<template>
<div id="container">
  <div class="Chart_MainBox">
    <p id="title">{{ Result }}</p>
    <p id="descriptions">1. Clique na seta que corresponde à direção em que a abertura da letra E está direcionada</p>
    <p id="descriptions">2. Clique no botão "Começar" para iniciar o teste.</p>
        
    <div class="Chart_ExternalBox">
      <p class="arrows" @click="KeyResult(37)" id="arrow_left">B</p>

      <div class="Chart_InnerBox">
        <p class="arrows" @click="KeyResult(38)">C</p>
        <p id="symbol">{{ Symbol }}</p>
        <p class="arrows" @click="KeyResult(40)">D</p>
      </div>  
        <p class="arrows" @click="KeyResult(39)" id="arrow_right">A</p>
      </div>
      
  </div>
</div>
</template>

<script>
export default {
  name: 'GuidelinesSnellen',
  data(){
    return {
      Symbol: 'a',
      Result: 'Como o teste funciona:'
    }
  },
  methods: {
    KeyResult: function(Key) {
      this.Result = 'Você errou. Tente novamente.'
      switch (Key) 
      {
        case 37:
          if (this.Symbol == 'c') 
          {
            this.Result = 'Muito bom! Agora tente novamente.'
            this.Symbol = 'a'  
          }
          else
          {
            this.Symbol = 'a'
          }
        break;

        case 38:
          this.Symbol = 'a'
        break;

        case 39:
          if (this.Symbol == 'a') 
          {
            this.Result = 'Muito bom! Agora tente novamente.'
            this.Symbol = 'b'  
          }
          else
          {
            this.Symbol = 'a'
          }
        break;

        case 40:
          if (this.Symbol == 'b') 
          {
            this.Result = 'Muito bom! Agora tente novamente.'
            this.Symbol = 'c'  
          }
          else
          {
            this.Symbol = 'a'
          }
        break;
      }
    }
  },
  created: function() {
    document.addEventListener('keyup', event => {this.KeyResult(event.keyCode)})
  }
}
</script>

<style scoped>
@import '../assets/css/normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');
@font-face{
  font-family: Eyechart;
  src: url('../assets/fonts/Eyechart.ttf');
}
@font-face{
  font-family: Arrows;
  src: url('../assets/fonts/Arrows.ttf');
}
#container{
  width: 100%;
  height: 85%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
#title{
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  font-size: 26px;
  color: #5551A6;
  text-align: center;
}
#descriptions{
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  font-size: 20px;
  color: #333333;
  text-align: center;
  line-height: 1;
}
.Chart_MainBox{
  font-family: Arrows;
  text-align: center;
}
.Chart_ExternalBox{
  width: 400px;
  display: inline-flex;
  margin-left: 85px;
}
.Chart_InnerBox{
  width: 200px;
  text-align: center;
}
#symbol{
  font-family: Eyechart;
  font-size: 151px;
  text-align: center;
  color: black;
  margin: 0;
}
#image{
  width: 200px;
}
.arrows{
  font-size: 70px;
  color: #878787;
  cursor: pointer;
  margin: 1px;
  margin-bottom: 16px;
}
#arrow_left, #arrow_right{
  margin-top: 135px;
}
</style>