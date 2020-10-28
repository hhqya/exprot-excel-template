<template>
  <div id="app">
      <ExportToExcel></ExportToExcel>
  </div>
</template>

<script>
    import ExportToExcel from './views/Excel_Export'
export default {
  name: 'App',
  components: {
      ExportToExcel
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
