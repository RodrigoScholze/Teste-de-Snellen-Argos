<template>
<div id="container">
  <div id="InputsForm" v-if="CheckboxScreen != true">
    <p id="Title">Dados pessoais</p>

    <p>Nome:</p>
    <input type="text" placeholder="João da Silva" class="TextInput" v-model="UserDataset.Name">

    <p>E-mail:</p>
    <input type="email" placeholder="joao@email.com" class="TextInput" v-model="UserDataset.Email">

    <p>Telefone (WhatsApp):</p>
    <input type="number" placeholder="47 99999.9999" class="TextInput" v-model="UserDataset.Telephone_WhatsApp">
  </div>

  <div id="CheckboxesForm" v-if="CheckboxScreen">
    <p id="Title">Responda esse breve questionário sobre a sua saúde:</p>
    
    <div id="CheckboxesContainer">
      <div>
        <p>Você usa óculos e/ou lentes de contato ?</p>
        
          <input type="radio" name="Glasses_Lens" value="Não" v-model="UserDataset.Questions.Glasses_Lens">
          <label>Não</label><br>  

          <input type="radio" name="Glasses_Lens" value="Somente óculos" v-model="UserDataset.Questions.Glasses_Lens">
          <label>Somente óculos</label><br>

          <input type="radio" name="Glasses_Lens" value="Somente lentes de contato" v-model="UserDataset.Questions.Glasses_Lens">
          <label>Somente lentes de contato</label><br>

          <input type="radio" name="Glasses_Lens" value="Óculos e lentes de contato" v-model="UserDataset.Questions.Glasses_Lens">
          <label>Óculos e lentes de contato</label><br>

        <p>Sem os seus óculos ou lentes você sente dificuldade visual ?</p>

          <input type="radio" name="VisualDifficulty" value="Nenhuma dificuldade" v-model="UserDataset.Questions.VisualDifficulty">
          <label>Nenhuma dificuldade</label><br>

          <input type="radio" name="VisualDifficulty" value="Dificuldade para ver de longe" v-model="UserDataset.Questions.VisualDifficulty">
          <label>Dificuldade para ver de longe</label><br>

          <input type="radio" name="VisualDifficulty" value="Dificuldade para ver de perto" v-model="UserDataset.Questions.VisualDifficulty">
          <label>Dificuldade para ver de perto</label><br>

          <input type="radio" name="VisualDifficulty" value="Dificuldade para ver de longe e perto" v-model="UserDataset.Questions.VisualDifficulty">
          <label>Dificuldade para ver de longe e perto</label><br>
      </div>

      <div>
        <p>Apresenta alguma(s) das seguintes condições de saúde ?</p>

          <input type="checkbox" name="HealthConditions" value="Diabetes" v-model="UserDataset.Questions.HealthConditions">
          <label>Diabetes</label><br>

          <input type="checkbox" name="HealthConditions" value="Glaucoma (pressão ocular elevada)" v-model="UserDataset.Questions.HealthConditions">
          <label>Glaucoma (pressão ocular elevada)</label><br>

          <input type="checkbox" name="HealthConditions" value="Degeneração macular relacionada à idade" v-model="UserDataset.Questions.HealthConditions">
          <label>Degeneração macular relacionada à idade</label><br>

        <p>Já realizou alguma cirurgia ou procedimento nos olhos ?</p>
      
          <input type="radio" name="Surgery" value="Sim" v-model="UserDataset.Questions.Surgery">
          <label>Sim</label><br>

          <input type="radio" name="Surgery" value="Não" v-model="UserDataset.Questions.Surgery">
          <label>Não</label>
      </div>
    </div>
  </div>

  <div id="ContainerButton">
    <button id="SendButton" :disabled="UserDataset.Name == '' || UserDataset.Email == ''" @click="ChangeScreen()">{{ TitleButton }}</button>
  </div>  
</div>
</template>

<script>
export default {
  name: 'Form',
  props: {
    SnellenResult: {
      type: Object,
      required: true
    }
  },
  data(){
    return {
      TitleButton: 'Próximo',
      CheckboxScreen: false,
      UserDataset: {
                      Name: '',
                      Email: '',
                      Telephone_WhatsApp: undefined,
                      SnellenResult: this.SnellenResult,
                      Questions:{
                                  Glasses_Lens: 'Não',
                                  HealthConditions: [],
                                  VisualDifficulty: 'Nenhuma dificuldade',
                                  Surgery: 'Não'
                                }
                   }
    }
  },
  methods: {
    ChangeScreen: function() {
      switch (this.CheckboxScreen) 
      {
        case true:
          this.FormPOST()
        break;

        case false:
          this.CheckboxScreen = true
          this.TitleButton = 'Enviar'
        break;
      }
    },
    FormPOST: function() {
        let axios = require('axios')
        axios({
              method: 'POST',
              url: 'http://argoshackvision.tech/Backend/',
              data: JSON.stringify(this.UserDataset)
            })
        .then(function () {
          window.location.href = "http://www.argoshackvision.tech/argos_obrigado.html";
        })
        .catch(function (response) {
          console.log(response);
        })
    }
  }
}
</script>

<style scoped>
@import '/assets/css/normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');
#InputsForm{
  font-family: 'Montserrat', 'sans-serif';
  text-align: center;
  height: 45%;
  width: 60%;
}
#CheckboxesForm{
  font-family: 'Montserrat', 'sans-serif';
}
#CheckboxesContainer{
  display: inline-flex;
}
#CheckboxesContainer div{
  margin-left: 20px;
}
#CheckboxesContainer p{
  font-weight: bold;
}
#CheckboxesContainer label{
  margin-left: 5px;
}
#CheckboxesContainer input{
  margin-bottom: 10px;
}
#Title{
  font-style: normal;
  font-weight: bold;
  font-size: 28px;
  color: #5551A6;
  margin: 0 0 30px 0;
}
.TextInput{
  width: 100%;
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
[type="number"]::-webkit-inner-spin-button {
  display: none;
}
#ContainerButton{
  position: absolute;
  bottom: 0px;
  width: 100%;
  text-align: center;
  margin-bottom: 30px;
}
#SendButton{
  font-family: 'Montserrat', 'sans-serif';
  font-weight: 500;
  background-color: #5551A6;
  border: none;
  border-radius: 32px;
  color: white;
  padding: 8px 12px;
  font-size: 22px;
  width: 330px;
  cursor: pointer;
}
#SendButton[disabled]{
  cursor: default;
  opacity: 0.5;
}
</style>