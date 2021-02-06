<template>
    <section id="register">
      <div id="title">
        <div><h1>Cadastro</h1></div>
      </div>  
      <form action="" id="Form">
        <label for="userName">Nome</label>
        <input v-model="userName" type="text" name="name" id="userName" placeholder="" class="form-control" required />
        <label for="userEmail">Email</label>
        <input v-model="userEmail" type="email" name="email" id="userEmail" placeholder="" class="form-control" required />
        <label for="userCPF">CPF</label>
        <input v-model="userCPF" type="text" name="CPF" id="userCPF" placeholder="111.111.111-01" class="form-control" maxlength="14" v-mask="'###.###.###-##'" required/>
        <div id="address">
          <div class="subAddress">
            <label for="userAddress">Endereço</label>
            <input v-model="userAddress" type="text" name="Address" id="userAddress" placeholder="Rua, Número e Bairro" class="form-control" required/>
          </div>
          <div class="subAddress">
            <label for="userState">Estado</label>
            <select id="estados" v-model="selectedLand" required>
              <option>Selecione o Estado</option>
              <option value="AC">Acre</option>
              <option value="AL">Alagoas</option>
              <option value="AP">Amapá</option>
              <option value="AM">Amazonas</option>
              <option value="BA">Bahia</option>
              <option value="CE">Ceará</option>
              <option value="DF">Distrito Federal</option>
              <option value="ES">Espirito Santo</option>
              <option value="GO">Goiás</option>
              <option value="MA">Maranhão</option>
              <option value="MS">Mato Grosso do Sul</option>
              <option value="MT">Mato Grosso</option>
              <option value="MG">Minas Gerais</option>
              <option value="PA">Pará</option>
              <option value="PB">Paraíba</option>
              <option value="PR">Paraná</option>
              <option value="PE">Pernambuco</option>
              <option value="PI">Piauí</option>
              <option value="RJ">Rio de Janeiro</option>
              <option value="RN">Rio Grande do Norte</option>
              <option value="RS">Rio Grande do Sul</option>
              <option value="RO">Rondônia</option>
              <option value="RR">Roraima</option>
              <option value="SC">Santa Catarina</option>
              <option value="SP">São Paulo</option>
              <option value="SE">Sergipe</option>
              <option value="TO">Tocantins</option>
            </select>
          </div>
          <div class="subAddress">
            <label for="userCEP" >CEP</label>
            <input v-model="userCEP" type="text" name="CEP" placeholder="22.222-000" class="form-control" maxlength="10" v-mask="'##.###-###'" required/>
          </div>
          <div class="subAddress">
            <label for="userCity">Cidade</label>
            <select v-model="userCity" name="city" id="city" required>
              <option>Selecione a Cidade</option>
              <option  v-for="element in city" :key="element">{{element}}</option>
            </select>
          </div>
        </div>

        <div id="payText">Forma de pagamento</div>

        <div id="payOptions">
          <input type="radio" id="creditCard" name="card" value="creditCard" required/>
          <label for="creditCard">Cartão de Crédito</label>
          <input type="radio" id="debitCard" name="card" value="debitCard" required/>
          <label for="debitCard">Cartão de Débito</label>
        </div>

        <div id="payConfig">
          <div class="SubPayConfig">
            <label for="cardName">Nome no Cartão</label>
            <input v-model="cardName" type="text" name="cardName" id="cardName" placeholder="Nome no cartão" required/>
          </div>
          <div class="SubPayConfig">
            <label for="cardData">Data de Expiração</label>
            <div id="cardData">
              <select name="month" id="month" required>
                  <option>Escolha o mês</option>
                  <option value="01">Jan</option>
                  <option value="02">Fev</option>
                  <option value="03">Mar</option>
                  <option value="04">Abr</option>
                  <option value="05">Mai</option>
                  <option value="06">Jun</option>
                  <option value="07">Jul</option>
                  <option value="08">Ago</option>
                  <option value="09">Set</option>
                  <option value="10">Out</option>
                  <option value="11">Nov</option>
                  <option value="12">Dez</option>
              </select>
              <select name="year" id="year">
                <option>Escolha o ano</option>
                  <option value="01">2021</option>
                  <option value="02">2022</option>
                  <option value="03">2023</option>
                  <option value="04">2024</option>
                  <option value="05">2025</option>
                  <option value="06">2026</option>
                  <option value="07">2027</option>
                  <option value="08">2028</option>
                  <option value="09">2029</option>
              </select>
            </div>
          </div>
          <div class="SubPayConfig">
            <label for="cardNumber">Número do Cartão</label>
            <input v-model="cardNumber" type="text" name="cardNumber" id="cardNumber" placeholder="5555 5555 5555 5555" maxlength="19" v-mask="'#### #### #### ####'" required/>
          </div>
          <div class="SubPayConfig">
            <label for="cardCod">Código de Segurança</label>
            <input v-model="cardCod" type="text" name="cardCod" id="cardCod" placeholder="XXX" maxlength="3" required/>
          </div>
        </div>

        <div id="value">Seu cartão será debitado em {{ currencyBRL(value) }}</div>

        <input type="submit" @click="submit" value="REALIZAR MATRÍCULA" id="submit" required/>
        <div id="info">Informações seguras e criptografadas</div>

      </form>
    </section>
</template>


<script>
  
  import Vue from 'vue'
  import arrayLands from "./../assets/cities.js";
  import { VueMaskDirective } from 'v-mask'
  Vue.directive('mask', VueMaskDirective);

  //Função que recebe um elemento e o transforma em algorismo com dois dígitos ex... 1 -> 01
  const zeroFill = (n) => {
    return ("0" + n).slice(-2);
  };

  export default {
    data() {
      return {
        value: 49,
        selectedLand: "Selecione o Estado",
        userName: "",
        userEmail: "",
        userCPF: "",
        userCEP:"",
        userAddress:"",
        userCity:"Selecione a Cidade",
        cardName:"",
        cardNumber:"",
        cardCod:"",
      };
    },
    computed: {
      //função que recebe o object filtrado através do estado selecionado pelo usuário
      city: function () {
        const landSelected = this.selectedLand;
        const landFiltered = arrayLands.filter((e) => {
          return e.sigla == landSelected;
        });
        return landFiltered.length > 0 && landFiltered[0].cidades;
      },
    },
    methods: {
      //método que recebe um valor e o transforma para a forma local de escrita monetária (real) ex... 10 -> R$10,00
      currencyBRL: (value) => {
        const options = { style: "currency", currency: "BRL" };
        return value.toLocaleString("pt-BR", options);
      },
      //método que é ativado com o click do botão submit
      submit: function (event) {
        if(!this.userName || !this.userEmail || !this.userCPF){
          // alert('preencha todos os dados')
          return;
        }
        // localStorage.clear();
        //date recebe a função nativa Date() do JavaScript para instanciar a data do sistema
        const date = new Date();
        //aplica a função para mudar os algorismos e recebe o dia o mês e o ano através das funções 'get'
        const dateSystem = zeroFill(date.getDate()) + "-" + zeroFill(date.getMonth() + 1) + "-" + zeroFill(date.getYear());
        event.preventDefault();//previne comportamento padrão do submit
        console.log("teste");
        const storedData = JSON.parse(localStorage.getItem("storedData") || "[]");//cria armazenamento no local
        storedData.push({
          nome: this.userName,
          email: this.userEmail,
          CPF: this.userCPF,  
          data: dateSystem,
        });
        localStorage.setItem("storedData", JSON.stringify(storedData));
        alert(`O usuario ${this.userName} foi cadastrado!`); //indica ao usuário que o formulário foi submetido
        this.clearForm();
      },
      //função que limpa o formulário depois que é enviado
      clearForm: function() {
        this.value = 49;
        this.selectedLand = "Selecione o Estado";
        this.userName = "";
        this.userEmail = "";
        this.userCPF = "";
        this.userCEP ="";
        this.userAddress="";
        this.userCity="";
        this.cardName="";
        this.cardNumber ="";
        this.cardCod ="";
      }
    },
  };
</script>

<style>
  ::-webkit-input-placeholder {
    font-weight: bold;
    color: #bbccdc;
  }

  :-ms-input-placeholder {
    font-weight: bold;
    color: #bbccdc;
  }

  ::placeholder {
    font-weight: bold;
    color: #bbccdc;
  }

  section {
    margin-bottom: 6vh;
  }

  @media screen and (max-device-width: 700px) {
    section {
    width: 100%;
    margin-bottom: 6vh;
    }
    form{
      font-family: "Nunito", sans-serif;
      margin: auto;
      width: 90%;
      display: flex;
      flex-direction: column;
      gap: 2vh;
      justify-content: space-between;
    }
    #title div {
      width: 100%;
    }
    #address {
      display: grid;
      grid-area: 100vh;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      grid-column-start: 0;
      grid-column-end: 1;
      gap: 2vh;
    }
  }

  @media screen and (min-device-width: 701px) {
    form {
      font-family: "Nunito", sans-serif;
      margin: auto;
      width: 40vw;
      display: flex;
      flex-direction: column;
      gap: 2vh;
      justify-content: space-between;
    }
  }

  #title {
    width: 100%;
    height: 15vh;
    background-color: #eff4f8;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
    box-sizing: border-box;
    margin-top: 0;
    margin-bottom: 5vh;
  }

  #title div {
    width: 40vw;
  }

  #title h1 {
    font-family: "Alice", serif;
    font-weight: 200;
    font-size: 4em;
    color: #445565;
    margin: 0;
  }

  input, select {
    font-weight: bold;
    box-sizing: border-box;
    padding-left: 0.5vw;
    border-radius: 5px;
    color: #bbccdc;
    background-color: #eff4f9;
    box-shadow: 0px 2px 2px rgba(187, 204, 221, 0.4);
    border: none;
    outline: none;
    height: 6vh;
  }

  label {
    font-weight: bold;
    color: #445566;
  }

  #address {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 2vh;
  }
  .subAddress, .SubPayConfig {
    width: 100%;
    display: flex;
    gap: 2vh;
    flex-direction: column;
  }

  #payText {
    font-weight: bold;
    height: 5vh;
    margin: 2vh 0 2vh 0;
    border-bottom: #eff4f8 3px solid;
    color: #1188ee;
  }

  #payOptions {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1vh;
  }

  #payOptions input {
    background-color: transparent;
    box-shadow: none;
    margin: 0;
  }

  #payConfig {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 2vh;
    padding-bottom: 4vh;
    border-bottom: #eff4f8 3px solid;
  }

  #cardData {
    display: flex;
    justify-content: space-between;
    gap: 1vh;
  }

  #cardData select {
    width: 50%;
  }

  #value {
    margin-top: 6vh;
    font-weight: bold;
    color: #445566;
  }

  #submit {
    width: 50%;
    color: white;
    background-color: #1188ee;
    left: 0;
  }

  #info {
    font-weight: 400;
    color: #445566;
  }

</style>
