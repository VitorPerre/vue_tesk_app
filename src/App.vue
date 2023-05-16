<template>
  <div class="header">
    <div class="header-left">
      <router-link to="/" class="logo">Aplicações Vue</router-link>
    </div>
    <div class="header-right">
      <router-link to="/" class="active">Home</router-link>
      <router-link to="/todolist">Lista de Tarefas</router-link>
      <router-link to="/about">Sobre</router-link>
    </div>
  </div>
  <router-view></router-view>
</template>

<script setup>
import { RouterView } from 'vue-router';
</script>

<style scoped>
.header {
  overflow: hidden;
  background-color: #f1f1f1;
  padding: 20px 10px;
}

.header a {
  float: left;
  color: black;
  text-align: center;
  padding: 12px;
  text-decoration: none;
  font-size: 18px;
  line-height: 25px;
  border-radius: 4px;
}

.header a.logo {
  font-size: 25px;
  font-weight: bold;
}

.header a:hover {
  background-color: #ddd;
  color: black;
}

.header a.active {
  background-color: dodgerblue;
  color: white;
}

.header-right {
  float: right;
}

@media screen and (max-width: 500px) {
  .header a {
    float: none;
    display: block;
    text-align: left;
  }
  .header-right {
    float: none;
  }
}
</style>