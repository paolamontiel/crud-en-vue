<template>
  <div id="app">
    <SongList />
  </div>
</template>

<script>
import SongList from "./components/SongList.vue";

export default {
  components: {
    SongList,
  },
};
</script>

<style>
/* Estilos generales de la aplicación */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #333;
  margin-top: 20px;
}
</style>
