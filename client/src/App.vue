<template >
  <div >
    <v-row>
      <v-col>
        <img alt="Vue logo" src="./assets/MazaGram.png" width="500">
      </v-col>
      
    </v-row>

    <PostComponent />
  </div>
  
</template>

<script>
import PostComponent from './components/PostComponent.vue'

export default {
  name: 'App',
  components: {
    PostComponent
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
