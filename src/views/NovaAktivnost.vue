<template>
  <div class="about">
    <h1>Unos nove aktivnosti</h1>

    <div class="container">

      <div class="row">
      <div class="col-4">

      
        <label for="example-datepicker" class="cal-label">Odaberi datum</label>
      <b-form-datepicker 
    id="example-datepicker" 
    placeholder="Odaberi datum"
     v-model="value" class="mb-2" 
     :start-weekday=1
     :date-format-options="{ year: 'numeric', month: 'numeric', day: 'numeric' }"
     menu-class="w-100"
     calendar-width="100%"
     locale="hr"></b-form-datepicker>

    <p>Prikaz u tablici aktivnosti: '{{ value }}'</p>

  </div>

  <div class="col-md-7 ">
    <input
    class="opis-custom"
    type="text"
    id="input-opis"
    placeholder="Unesi Opis"/>
  </div>

</div>

<div class="row">

  <div class="col-md-2">
    <p>Trenutan Odabir:</p>
    <p v-for="volonter in new_aktivnost.volonteri" :key="volonter"> {{ volonter }}</p>
  </div>
  <div class="col-md-4">
    <b-form-select v-model="odabirVolonter" @input="dodajVolonter" class="custom-volInput" >
      <option value="" disabled selected>Odaberi volontere</option>
            <option v-for="volonter in volonteriOpcije" :key="volonter" :value="volonter">
              {{ volonter }}
            </option>
          </b-form-select>

          <button @click="volIzbrisi">Izbriši odabir</button>
          
  </div>

</div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';


export default {
  name: "novaAktivnost",

  data() {
    return {
      value: null,
      weekday: 1,
      hideHeader: true,
      odabirVolonter:"",
      volonteriOpcije:[],

      new_aktivnost:{
        datum:"",
        opis:"",
        oblik_rada:[],
        volonteri:[],
        admin:[],
        sati:""
      },
    };
  },
  created(){
    this.getVolonteriOpcije()
  },

  methods: {
    getVolonteriOpcije(){
        axios
        .get("http://localhost:3001/sviVolonteri")
        .then((response)=>{
            for(let i=0;i<response.data.length;i++)
              this.volonteriOpcije.push(response.data[i].email);

              console.log(this.volonteriOpcije);
        });

    },
    dodajVolonter(){
      if(this.odabirVolonter){
        this.new_aktivnost.volonteri.push(this.odabirVolonter);
        this.odabirVolonter="";
      }

      console.log(this.new_aktivnost.volonteri);
    },
    volIzbrisi(){
      this.new_aktivnost.volonteri=[];
    }
  },
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

.container{
  margin-left: 20px;
  margin-right: 20px;
}
.row{
  margin-bottom: 50px;
}
.cal-label{
  margin-left: 0%;
  text-align: left;
  font-size: 20px;
}

.opis-custom{
  margin-top: 35px;
  width: 600px;
  text-align: justify;
  font-size: 18px;
  opacity: 65%;
  border-block-color: #a020f0;
  border-width: 2px;
}

.custom-volInput{
  width: 300px;
  height: 30px;
  font-size: 15px;
  margin-left: -30px;

}
</style>
