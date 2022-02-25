<script>
import axios from 'axios'

export default{
  data() {
    return {
      etat: true,
      info: null,
      appareils : [
        // {
        // name: 'Machine à laver',
        // status: 'éteint'
        // },
        // {
        // name: 'Frigo',
        // status: 'allumé'
        // },
        // {
        // name: 'Ordinateur',
        // status: 'éteint'
        // }
      ],
    }
  },
  methods: { 
    handleAllOff(){
      var appareils = this.appareils.map((a) => {
        a.status = 'éteint';
        return a;
      });
      this.appareils = appareils;
    },

    handleAllOn(){
      var appareils = this.appareils.map((a) => {
        a.status = 'allumé';
        return a;
      });
      this.appareils = appareils;
    }
  },
   mounted() {
            axios.get('/listAppareil.json').then( ({data}) => this.appareils = data.appareils)
        },
  props: {
   
  }
}
</script>

<template>
    <h2>Mes appareils</h2> 
    <ul class="list-group">      
        <li v-for="appareil in appareils" :key="appareil.name" id="id" class="list-group-item" v-bind:class="{'list-group-item-success' : appareil.status=='allumé', 'list-group-item-danger': appareil.status=='éteint'}">                    
            <h4 v-if="appareil.status=='allumé'" style='color : green'>  Appareil : {{appareil.name}} -- Statut : Allumé</h4>  
            <h4 v-else style='color : red'>  Appareil : {{appareil.name}} -- Statut : Eteint</h4> 
            <button v-if="appareil.status=='allumé'" class='btn btn-inline btn-sm btn-danger' @click="appareil.status='éteint'">Eteindre</button>
            <button v-else class='btn btn-inline btn-sm btn-success' @click="appareil.status='allumé'">Allumer</button>
        </li>  
    </ul>
    <div>          
        <button className="btn btn-success" @click="handleAllOn" >Tout allumer</button>                        
        <button className="btn btn-danger" @click="handleAllOff" >Tout éteindre</button>    
    </div>                  
  
</template>

