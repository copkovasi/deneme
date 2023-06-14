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

.container {
  display: flex;
  flex-direction: column;
}

.bilgiler-kamera-kalman {
  display: flex;
  margin-left: 10px;
  margin-right: 10px;
}

.bilgiler {
  display: flex;
  flex-direction: column;
  margin-right: 10px;
}

.bilgiler>* {
  border: solid 1px;
}

.satir-1 {
  display: flex;
}

.sunucu-bilgileri {
  display: flex;
  flex-direction: column;
}

.bilgi-satir {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  max-height: 40px;
}

.kamera-ibreler-kalman {
  display: flex;
  flex-direction: column;
}

.kamera-kalman {
  display: flex;
}

.kamera-kalman>* {
  border: solid 1px black;
}

.ibreler {
  display: flex;
  justify-content: center;
  background-color: black;
  border: 5px solid gray;
  border-bottom-right-radius: 50px;
  border-bottom-left-radius: 50px;
}

.ibreler>* {
  margin-right: 10px;
}

.kalman-harita {
  /* background-color: green; */
  border: solid 1px black;
  width: 40%;
}

/* #kamera-ibreler-canvas {
  width: 33%;
} */

.hizli-komutlar-satir {
  display: flex;
  flex-direction: column;
}

.hizli-komutlar {
  display: flex;
  justify-content: center;
}

.yki-komut {
  display: flex;
  justify-content: center;
}

.log-satir {
  display: flex;
  flex-direction: row;
}

.log-kayitlari {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 0.5%;
  margin: 0.5%;
  width: 100%;
}

#logtextarea {
  width: 100%;
  min-height: 250%;
}

#logtable tr {
  font-size: 13px;
  height: 30px;
}

body {
  font-family: Roboto Mono;
  background-color: #121212;
}

.text-green {
  color: #94bc2f !important;
}


.btn-outline-success {
  --bs-btn-color: #94bc2f;
  --bs-btn-border-color: #94bc2f;
  --bs-btn-hover-color: #fff;
  --bs-btn-hover-bg: #94bc2f;
  --bs-btn-hover-border-color: #94bc2f;
  --bs-btn-focus-shadow-rgb: 25, 135, 84;
  --bs-btn-active-color: #fff;
  --bs-btn-active-bg: #94bc2f;
  --bs-btn-active-border-color: #94bc2f;
  --bs-btn-active-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  --bs-btn-disabled-color: #94bc2f;
  --bs-btn-disabled-bg: transparent;
  --bs-btn-disabled-border-color: #94bc2f;
  --bs-gradient: none;
}

.btn-success {
  --bs-btn-color: #fff;
  --bs-btn-bg: #94bc2f;
  --bs-btn-border-color: #94bc2f;
  --bs-btn-hover-color: #fff;
  --bs-btn-hover-bg: #648121;
  --bs-btn-hover-border-color: #648121;
  --bs-btn-focus-shadow-rgb: 60, 153, 110;
  --bs-btn-active-color: #fff;
  --bs-btn-active-bg: #648121;
  --bs-btn-active-border-color: #13653f;
  --bs-btn-active-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  --bs-btn-disabled-color: #fff;
  --bs-btn-disabled-bg: #94bc2f;
  --bs-btn-disabled-border-color: #94bc2f;
}

.camera-button {
  font-size: 600px;
  width: 100%;
  height: 100px;
  margin-bottom: 0.5rem;
  margin-top: 1%;
}

.pi pi-camera {
  font-size: large;
  margin-left: 10px;
}

.text-class {

  margin-left: 50px;
  text-align: center;

}

.Gaz-Tittle {
  color: white;
  position: relative;
}

.slider-container {
  width: 300px;
  height: 30px;
}

.tooltip-style {
  background-color: #f1f1f1;
  color: #333;

  padding: 16px;

  /* padding-right: 50%;
  padding-left: 50%; */
  font-size: x-large;

}

.tooltip-icon {
  margin-right: 10px;


}

.sliderTitle {
  margin: 10%;
  margin-left: 1%;
  margin-right: 1%;

}

.tool-tip {
  display: flex;
  justify-content: center;
  background-color: #f1f1f1;
  border: 1px solid #ccc;
  border-radius: 16px;
}

.goruntu-gaz {
  display: flex;
  flex-direction: column;
}

.goruntu-gaz>h2 {
  color: black;
  background-color: #f1f1f1;
  border-radius: 5%;
}

.ana-baslik {
  color: white;
  display: flex;
  justify-content: center;
  margin-bottom: 1%;

}

.no-padding {
  padding: 0px !important;
  padding-top: 1% !important;
}

img+button {
  margin-bottom: 10%;
}

.row-gaz {
  display: flex;
}

#kamera {
  width: 100%;
  height: 320px;

}

.camera-div {
  display: flex;
  justify-content: center;
}

.tool-tip-div p {

  color: white;
}

.baglanti-bilgisi-div .card-body {
  display: flex;

  flex-direction: column;
  justify-content: space-between;
  align-content: space-between;

}


.card-body>div {
  display: flex;
  align-content: stretch;
}

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
