<template>
  <div>
   <Navbar/>
   <h4>Nueva Cita</h4><br><br>
   <form  @submit.prevent="Registrar" action="">
     <div class="row">
     <div class="col m4"></div> 
     <div class="input-field col m4">
      <input type="date" v-model="fecha" required>
    </div>
  </div> 
    <div class="row">
     <div class="col m4"></div> 
     <div class="input-field col m4">
      <select v-model="hora" required="required" id="select">
        <option value="defecto" disabled selected>Selecciona una hora</option>
        <option value="10:00">10:00</option>
        <option value="10:30">10:30</option>
        <option value="11:00">11:00</option>
        <option value="11:30">11:30</option>
        <option value="12:00">12:00</option>
        <option value="12:30">12:30</option>
      </select>
      <label>Hora</label>
    </div>
  </div>
  <div class="row">
    <div class="col m4"></div>  
    <div class="input-field col m4">
      <textarea id="textarea2" required v-model="dolencia" class="materialize-textarea" data-length="120"></textarea>
      <label for="textarea2">Dolencia</label>
    </div>
  </div>
 <div class="row">
    <div class="col m4"></div>  
    <div class="input-field col m4">
     <button type="submit" class="btn">Agendar</button>
     <!-- <button class="btn">Cancelar</button> -->
    </div>
  </div>
  </form>
  </div>
</template>
<script>
import Navbar from '@/components/Nav.vue'
import { db } from '@/firebase';
import M from 'materialize-css'

export default {
  name:"NuevaCita",
  components:{
    Navbar
  },
  computed:{
    user(){
      return this.$store.state.user
    }
  },
  data(){
    return{
     fecha:"",
     hora:"",
     dolencia:""
    }
  },
  mounted: function(){
      M.AutoInit();
    },
  methods:{
   Registrar(){
    db.collection("citas").add({
     paciente:{
      nombre:this.$store.state.user.name,
      id:this.$store.state.user.id
     },
     fecha:this.fecha,
     hora:this.hora,
     dolencia:this.dolencia
  })
  this.fecha=""
  this.hora=""
  this.dolencia=""
  document.getElementById('select').value="defecto"
  this.$router.push('/');
 }
},
  
}
</script>
<style scoped>
.btn{
  margin-right: 20px;
}
</style>