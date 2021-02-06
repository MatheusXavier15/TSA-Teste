<template>
  <div id="app">
    <header id="nav">
      <router-link to="/">Cadastro</router-link>
      <router-link to="/list">Lista</router-link>
    </header>
    <router-view/>
  </div>
</template>

<style>
    header {
    padding: 2vw;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    gap: 2vw;
    flex-direction: row-reverse;
    width: 100%;
    height: 6vh;
    background-color: #17222d;
    }
    header a {
    font-family: 'Nunito', sans-serif;
    color: white;
    text-decoration: none;
    }
</style>

