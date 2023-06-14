<template>
  <div class=" d-flex w-100 h-100 p-3 flex-column">
    <div class="button-level-style">
            <Button v-bind:class="{ 'p-button-danger': Servo_speed == 0 }" @click="insertvalue('fan_level', 1)">Açık</Button>
            <span>&nbsp;</span>
            <span>&nbsp;</span>
            <span>&nbsp;</span>
            <Button v-bind:class="{ 'p-button-danger': Servo_speed == 1 }" @click="insertvalue('fan_level', 0)">Kapalı</Button>
         
    </div>
  
  </div>
</template>

<script>


import Slider from 'primevue/slider';
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';
import Message from 'primevue/message';
import Button from 'primevue/button';
import { initializeApp } from 'firebase/app';
import { getDatabase, ref, onValue, set } from 'firebase/database';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    [DataTable.name]: DataTable,
    [Column.name]: Column,
    [Button.name]: Button,
    Slider,
    Message
  },
  watch: {
    

  },
  data() {
    return {
      
      firebaseConfig: {

        databaseURL: "https://trash-9498e-default-rtdb.firebaseio.com/",

      },
      app: null,
      database: null,
      gazvalue: 0,
      o2value: 0,
      isik_value: 0,
      doluluk: 0,
      light_level: null,
      fan_speed: null,
      Servo_speed: null,
      Email:null,
      o2showMessage: false,
      gazshowMessage: false,
      o2severity: "warn",
      o2uyari: "Düşük",
      gazseverity: "warn",
      gazuyari: "Düşük",
    
   
      msg: '',
      response: '',
      logs: '',
      logSeviyeITOS: {
        0: 'NOTSET',
        10: 'DEBUG',
        20: 'INFO',
        30: 'WARNING',
        40: 'ERROR',
        50: 'CRITICAL',
      },
      logSeviyeSTOI: {
        NOTSET: 0,
        DEBUG: 10,
        INFO: 20,
        WARNING: 30,
        ERROR: 40,
        CRITICAL: 50,
      },
      logList: [

      ]


    }
  },
  created() {
  

  },
  mounted() {


  },
  methods: {
    
  
  


  insertvalue(dbrefname, deger) {
    // Firebase referansını oluşturun
    const app = initializeApp(this.firebaseConfig);
    const database = getDatabase(app);
    const databaseRef = ref(database, '/' + dbrefname);
    // const databaseRef = ref(database, $`/{dbrefname}`);

    // Veriyi ekleyin
    set(databaseRef,
      deger
    )
      .then(() => {
        console.log('Veri eklendi');
      })
      .catch((error) => {
        console.error('Veri eklenirken bir hata oluştu:', error);
      });
  },
 


}
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
} */



.button-level-style {
  display: flex;
  justify-content: space-between;
  align-items: stretch;
  align-content: stretch;
}

.button-level-style>button {
  display: flex;
  /* align-items: stretch; */
  align-content: stretch;
  width: 100%;
  border-radius: 10px;
  margin-top: 2%;
}</style>
