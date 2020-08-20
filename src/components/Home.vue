<template>
  <div>
    <Navbar/>
    <br>
      <div class="row">
        <div class="col m4"></div>
        <div class="col m4"><h3>Citas Médicas</h3></div>
        <div class="input-field col m3">
          <i class="material-icons prefix">search</i>
          <input id="icon_prefix" v-model="buscador" type="text" class="validate">
          <label for="icon_prefix">buscador</label>
        </div>
      </div>
    <table class="centered">
      <thead>
        <tr>
          <th>Fecha</th>
          <th>Hora</th>
          <th>Nombre Paciente</th>
           <th>Dolencia</th>
           <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cita in Buscador" :key="cita.id">
        <td>{{cita.fecha}}</td>
        <td>{{cita.hora}}</td>
        <td>{{cita.paciente.nombre}}</td>
        <td>{{cita.dolencia}}</td>
        <td v-if="user.id==cita.paciente.id"><button  v-on:click="eliminar(cita.id)" class="btn">Cancelar</button></td>
        <td v-else>Ninguna</td>
      </tr>
      </tbody>
    </table>
    <br><br>
   <router-link :to="{path:'/cita'}" class="btn"><i class="material-icons left">add</i>Nueva Cita</router-link>
  </div>
</template>
<script>
import { db } from '@/firebase';
import Navbar from '@/components/Nav.vue'
export default {
  name:'Home',
  data(){
    return{
      citas:[],
      buscador:""
    }
  },
  computed:{
    user(){
      return this.$store.state.user
    },
    Buscador(){
      return this.citas.filter((cita)=> cita.paciente.nombre.includes(this.buscador)||cita.dolencia.includes(this.buscador))
    }
  },
  components:{
    Navbar
  },
  firestore(){
    return {
     citas: db.collection("citas").orderBy('fecha','asc')
      }
  },
  methods: {
     eliminar(id){
      const pregunta=confirm(`Desea cancelar su cita?`)
      if(pregunta==true){
        db.collection("citas").doc(id).delete();
      }
    }
  },
}
</script>