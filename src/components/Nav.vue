<template>
  <div>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <nav>
      <div class="nav-wrapper #4db6ac teal lighten-2">
        <a href="#" class="brand-logo">Hola</a>
        <ul id="nav-mobile" class="right hide-on-med-and-down">
          <li><router-link :to="{path:'/'}">Home</router-link></li>
          <li><a @click="Salir"><i class="tiny material-icons">power_settings_new</i></a></li>
        </ul>
      </div>
    </nav>
  </div>
</template>
<script>
export default {
  name:"Nav",
  methods:{
    Salir(){
      this.$store.dispatch('Salir');
    }
  }
}
</script>