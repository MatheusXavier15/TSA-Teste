<template>
  <div>
    <section id="contentList">
      <div id="title">
        <div><h1>Lista</h1></div>
      </div>
      <div id="content">
        <div id="listText">Lista de clientes</div>
        <div id="contentSearch">
          <label for="userSearch">Nome do cliente</label>
          <input v-model="filterProperty" type="search" name="userSearch" id="userSearch">
        </div>
        <table>
          <tr>
            <td>Nome</td>
            <td>Email</td>
            <td>CPF</td>
            <td>Criado em</td>
          </tr>
          <tr v-for="client in tableFilter" :key="client.name">
            <td>{{client.nome}}</td>
            <td>{{client.email}}</td>
            <td>{{client.CPF}}</td>
            <td>{{client.data}}</td>
          </tr>
          <tr id="whiteSpace">
            <td></td>
            <td></td>
            <td></td>
            <td></td>
          </tr>
        </table>
      </div>
    </section>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        filterProperty: "",
      };
    },
    computed: {
      //função que recebe o armazenameto local e filtra os dados não nulos/vazios
      clients: function () {
        const storedData = JSON.parse(localStorage.getItem("storedData"));
        if(!storedData)
          return [];
        const storedFiltered = storedData.filter((e) => {
          return e.nome !== null && e.nome !== "";
        });
        return storedFiltered;
      },
      //função que recebe o clients e filtra de acordo com o valor pesquisado
      tableFilter: function () {
        let params = this.filterProperty;
        const filtered = this.clients.filter((e) => {
          if (params !== "") {
            params = params.toLowerCase();
            return (
              e.nome.toLowerCase().includes(params) ||
              e.email.toLowerCase().includes(params) ||
              e.CPF.includes(params) ||
              e.data.includes(params)
            )
          } 
          //caso não seja pesquisado nada, retorna todos os elementos
          return true;
        });
        return this.clients && filtered;
      },
    },
  };
</script>

<style>
  @media screen and (max-device-width: 701px) {
    #title div {
      width: 100%;
    }
    #content {
      width: 75vw!important;
      margin: auto;
      }
      
  table {
    font-weight: bold;
    font-family: "Nunito", sans-serif;
    border-collapse: collapse;
    margin-top: 2vh;
    margin-bottom: 5vh;
    border-spacing: 0px;
    max-width: 100%;
    height: 70vh;
     font-size: clamp(1em, 1em + 1vw, 1.5em);
  }
  }
  #contentList {
    font-family: "Nunito", sans-serif;
    margin: auto;
    display: flex;
    flex-direction: column;
    gap: 2vh;
    justify-content: space-between;
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
    width: 60vw;
  }

  #title h1 {
    font-family: "Alice", serif;
    font-weight: 200;
    font-size: 4em;
    color: #445565;
    margin: 0;
  }

  #content {
    width: 75vw;
    margin: auto;
  }

  #listText {
    font-weight: bold;
    height: 5vh;
    margin: 2vh 0 2vh 0;
    border-bottom: #eff4f8 3px solid;
    color: #1188ee;
  }

  #contentSearch {
    display: flex;
    flex-direction: column;
    gap: 2vh;
  }

  table, th, td {
    border: 3px solid #eff4f9;
  }

  td, th {
    padding: 5px 5px 5px 10px;
  }

  td {
    width: 25%;
    max-width: 25%;
  }

  table {
    font-weight: bold;
    font-family: "Nunito", sans-serif;
    border-collapse: collapse;
    margin-top: 2vh;
    margin-bottom: 5vh;
    border-spacing: 0px;
    width: 75vw;
    height: 70vh;
  }

  tr {
    height: 6vh;
    max-height: 6vh;
  }

  #whiteSpace {
    height: 60vh;
  }
</style>
