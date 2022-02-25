<script>
import axios from 'axios'



export default{
  data() {
    return {
      etat: true,
      info: null,
      
    }
  },
  props: {
   
    AppareilStatut: Boolean 
  }
}
</script>

<template>
         
    <li id="id" class="list-group-item" v-bind:class="{'list-group-item-success' : AppareilStatut, 'list-group-item-danger': !AppareilStatut}">                    
      <h4 v-if="AppareilStatut" style='color : green'>  Appareil : {{appareil.name}} -- Statut : Allumé</h4>  
      <h4 v-else style='color : red'>  Appareil : {{appareil.name}} -- Statut : Eteint</h4> 
      <button class='btn btn-inline btn-sm' v-bind:class="{'btn-danger' : AppareilStatut, 'btn-success': !AppareilStatut}" @click="AppareilStatut = !AppareilStatut"><span v-if="AppareilStatut">Eteindre</span><span v-else>Allumer</span></button>
    </li>                   
  
</template>

