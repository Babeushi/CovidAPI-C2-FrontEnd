<template>
  <div id="app">
    <nav class="navbar navbar-expand">
      <a href="/pacientes" class="navbar-brand btn">Pacientes</a>      
    </nav>
    <div class="container mt-3">
      <router-view />
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  }
}
</script>

<style>
body{
  background:rgba(243, 197, 233, 0.445);
  background-image: url("./assets/fundo.jpg");
}
/*.navbar{
  background-color: #d465aa;
}*/
.navbar-brand{
  color: rgb(255, 255, 255);
  font-size: 24px;
  font-weight: bold;
  padding: 10px;
  background: #cc66add7;
}
.navbar-brand:hover{
  color: rgb(255, 255, 255);
}
.table-title{
  padding-bottom: 15px;
    background: #cc66ad;
    color: #fff;
    padding: 16px 30px;
    margin: -20px -25px 10px;
    border-radius: 3px 3px 0 0;
}
.table-wrapper {
    background: rgba(200, 193, 201, 0.445);
    padding: 20px 25px;
    margin: 30px 0;
    border-radius: 3px;
    box-shadow: 0 1px 1px rgba(0,0,0,.05);
    /*background-image: url("./assets/frufru.jpg");*/
}
table.table td a.edit{
  color:rgb(0, 0, 0);
}
.addEdit {
    background: rgba(200, 193, 201, 0.445);
    padding: 20px 25px;
    margin: 30px 0;
    border-radius: 3px;
    box-shadow: 0 1px 1px rgba(0,0,0,.05);
    background-image: url("./assets/frufru.jpg");
}
.addButton{
  background: #cc66ad;
  color: #fff;
}
.size{
  width: 400px;
  margin: auto;
}
</style>
