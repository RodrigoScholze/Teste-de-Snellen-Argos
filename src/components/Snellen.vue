<template>
<div id="container">
  <div class="Chart_MainBox">
      <div class="Chart_ExternalBox" v-if="InformationProperties.InformationBool == false">
        <p class="arrows" id="arrow_left" @click="Next(37)">B</p>

        <div class="Chart_InnerBox">
          <p class="arrows" @click="Next(38)">C</p>

          <p id="symbol" v-bind:style="{fontSize: SequenceProperties.FontSize + 'px', marginTop: SequenceProperties.SymbolMargin + 'px', marginBottom: SequenceProperties.SymbolMargin + 'px'}">
            {{ SequenceProperties.Symbol }}
          </p>

          <p class="arrows" @click="Next(40)">D</p>
        </div>

        <p class="arrows" id="arrow_right" @click="Next(39)">A</p>
      </div>

      <div class="information" v-if="InformationProperties.InformationBool">
        <p>{{ InformationProperties.Information }}</p>
        <img v-if="InformationProperties.ImgName == 'ChangeEye_Right'" src="../assets/images/ChangeEye_Right.png">
        <img v-if="InformationProperties.ImgName == 'ChangeEye_Left'" src="../assets/images/ChangeEye_Left.png">
        <p class="reminder" v-if="InformationProperties.ImgName == 'ChangeEye_Right' | InformationProperties.ImgName == 'ChangeEye_Left'">Aperte "ENTER" para continuar</p>
      </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Snellen',
  data(){
    return {
      Step: 0,
      SequenceProperties: {
                            Symbol: 'a',
                            FontSize: 77.70708661,
                            SymbolMargin: 80,
                            PressedKeys: []
                          },      
      InformationProperties: {
                                Information: undefined,
                                ImgName: undefined,
                                InformationBool: false
                             },
      EyeProperties: {
                        EyeStep: 0,
                        SideEye: 'Left',
                        Result: {
                                  Right: undefined,
                                  Left: undefined
                                },
                        Right:{
                                Mistakes: []
                              },
                        Left:{
                                Mistakes: []
                             }
                     }
    }
  },
  watch: {
    Step: function (value) {
      switch (value) {
        case 1:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 77.70708661
          this.SequenceProperties.SymbolMargin = 80
        break;

        case 2:
          this.LineMistakes(200, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 50.5096063
          this.SequenceProperties.SymbolMargin = 95
        break;

        case 3:
          this.LineMistakes(150, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 38.85354331
          this.SequenceProperties.SymbolMargin = 100
        break;

        case 4:
          this.LineMistakes(100, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 31.08585827
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 5:
          this.LineMistakes(80, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 25.25480315
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 6:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 25.25480315
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 7:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 25.25480315
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 8:
          this.LineMistakes(60, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 23.31212598
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 9:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 23.31212598
          this.SequenceProperties.SymbolMargin = 105
        break;

        case 10:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 23.31212598
          this.SequenceProperties.SymbolMargin = 105  
        break;

        case 11:
          this.LineMistakes(50, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 15.54141732
          this.SequenceProperties.SymbolMargin = 110  
        break;

        case 12:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 15.54141732
          this.SequenceProperties.SymbolMargin = 110  
        break;

        case 13:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 15.54141732
          this.SequenceProperties.SymbolMargin = 110
        break;

        case 14:
          this.LineMistakes(40, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 11.65606299
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 15:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 11.65606299
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 16:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 11.65606299
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 17:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 11.65606299
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 18:
          this.LineMistakes(30, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 9.713385827
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 19:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 9.713385827
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 20:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 9.713385827
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 21:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 9.713385827
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 22:
          this.LineMistakes(25, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 7.770708661
          this.SequenceProperties.SymbolMargin = 115  
        break;

        case 23:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 7.770708661
          this.SequenceProperties.SymbolMargin = 115
        break;

        case 24:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 7.770708661
          this.SequenceProperties.SymbolMargin = 115  
        break;

        case 25:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 7.770708661
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 26:  
          this.LineMistakes(20, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)

          this.SequenceProperties.Symbol = 'c'
          this.SequenceProperties.FontSize = 5.828031496
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 27:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 5.828031496
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 28:
          this.SequenceProperties.Symbol = 'a'
          this.SequenceProperties.FontSize = 5.828031496
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 29:
          this.SequenceProperties.Symbol = 'b'
          this.SequenceProperties.FontSize = 5.828031496
          this.SequenceProperties.SymbolMargin = 113  
        break;

        case 30:
          this.LineMistakes(15, this.SequenceProperties.PressedKeys, this.EyeProperties.SideEye, this.EyeProperties.EyeStep)
          this.EyeProperties.SideEye == 'Right' ? this.GenerateResult(this.EyeProperties.Right.Mistakes, this.EyeProperties.SideEye, this.EyeProperties.EyeStep) : this.GenerateResult(this.EyeProperties.Left.Mistakes, this.EyeProperties.SideEye, this.EyeProperties.EyeStep);
        break;

        case 'ChangeEye':
          this.ChangeEye(this.EyeProperties.SideEye)
        break;
      }
    }
  },
  methods: {
    LineMistakes: function(Line, PressedKeys, SideEye, EyeStep){
      switch (Line) 
      {
        case 200:
          if (PressedKeys[0] != 39)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 150:
          if (PressedKeys[0] != 40)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 100:
          if (PressedKeys[0] != 39)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 80:
          if (PressedKeys[0] != 37)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 60:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 50:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 40:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 30:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39 && PressedKeys[3] != 40)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 25:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39 && PressedKeys[3] != 40)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 20:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39 && PressedKeys[3] != 40)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;

        case 15:
          if (PressedKeys[0] != 37 && PressedKeys[1] != 40 && PressedKeys[2] != 39 && PressedKeys[3] != 40)
          {
            SideEye == 'Right' ? this.EyeProperties.Right.Mistakes[EyeStep] = Line : this.EyeProperties.Left.Mistakes[EyeStep] = Line;
          }
        break;
      }

      switch (SideEye) 
      {
        case 'Right':
          if (this.EyeProperties.Right.Mistakes[EyeStep] != undefined) this.GenerateResult(this.EyeProperties.Right.Mistakes, SideEye, EyeStep)  
        break;

        case 'Left':
          if (this.EyeProperties.Left.Mistakes[EyeStep] != undefined) this.GenerateResult(this.EyeProperties.Left.Mistakes, SideEye, EyeStep)
        break;
      }
      this.SequenceProperties.PressedKeys = []
    },
    GenerateResult: function(Mistakes, SideEye, EyeStep){
      switch (EyeStep) 
      {
        case 0:
          this.EyeProperties.EyeStep = 1
          this.Step = 1
        break;

        case 1:
          if (Mistakes[0] == Mistakes[1])
          {
            switch (SideEye) 
            {
              case 'Right':
                this.EyeProperties.Result.Right = Mistakes[0]
                this.EyeProperties.EyeStep = 0
                this.Step = 'ChangeEye'
              break;

              case 'Left':
                this.EyeProperties.Result.Left = Mistakes[0]
                this.EyeProperties.EyeStep = 0
                this.ChangeEye('Result')
              break;
            }
          }
          else
          {
            this.EyeProperties.EyeStep = 2
            this.Step = 1
          }
        break;

        case 2:
          switch (SideEye) 
          {
            case 'Right':
              this.EyeProperties.Result.Right = Mistakes[2]
              this.EyeProperties.EyeStep = 0
              this.Step = 'ChangeEye'
            break;

            case 'Left':
              this.EyeProperties.Result.Left = Mistakes[2]
              this.EyeProperties.EyeStep = 0
              this.ChangeEye('Result')
            break;
          }
        break;
      }
    },
    ChangeEye: function(SideEye){
      this.InformationProperties.InformationBool = true
      switch (SideEye) 
      {
        case 'Right':
          this.InformationProperties.Information = 'Tampe seu olho direito conforme a ilustração'
          this.InformationProperties.ImgName = 'ChangeEye_Left'
          this.EyeProperties.SideEye = 'Left'  
        break;

        case 'Left':
          this.InformationProperties.Information = 'Tampe seu olho esquerdo conforme a ilustração'
          this.InformationProperties.ImgName = 'ChangeEye_Right'
          this.EyeProperties.SideEye = 'Right'
        break;

        case 'Result':
          this.InformationProperties.Information = `Olho Esquerdo: ${this.EyeProperties.Result.Left} - Olho Direito: ${this.EyeProperties.Result.Right}`
          this.InformationProperties.ImgName = 'Result'
        break;
      }
    },
    Next: function(Key){
      if(Key == 13 && (this.Step == 'ChangeEye'))
      {
        this.Step = 1
        this.InformationProperties.InformationBool = false
      }
      else if (Key != 13 && (this.Step != 'ChangeEye'))
      {
        this.SequenceProperties.PressedKeys.push(Key)
        this.Step++
      }
    }
    },
    created: function() {
      document.addEventListener('keyup', event => {this.Next(event.keyCode)})
      this.Step = 'ChangeEye'
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
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.Chart_MainBox{
  font-family: Arrows;
}
.Chart_ExternalBox{
  width: 400px;
  display: inline-flex;
}
.Chart_InnerBox{
  width: 200px;
  text-align: center;
}
#symbol{
  font-family: Eyechart;
  text-align: center;
  color: black;
  margin: 0;
}
.arrows{
  font-size: 70px;
  color: #878787;
  cursor: pointer;
  margin: 16px;
}
#arrow_left, #arrow_right{
  margin-top: 175px;
}
#arrow_left{
  margin-right: 20px;
}
#arrow_right{
  margin-left: 20px;
}
.information{
  width: 850px;
  font-family: 'Montserrat', sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  text-align: center;
  color: #5551A6;
}
.reminder{
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  font-size: 20px;
  color: #333333;
  text-align: center;
  line-height: 1;
}
#reminder_form{
  font-family: 'Montserrat', sans-serif;
  font-weight: bold;
  font-size: 15px;
  color: #333333;
  text-align: center;
  line-height: 1;
}
#imgBlinkEye{
  width: 300px;
}
#imgChangeEye{
  width: 550px;
}
#imgEmoji{
  width: 200px;
} 
</style>