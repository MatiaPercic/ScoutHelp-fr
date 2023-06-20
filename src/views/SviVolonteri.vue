<template>

    <div class="container">
        <h1>Prikaz informacija svih volontera</h1>

        <div class="custom-checkbox">

        <input class="form-check-input" type="checkbox" id="inputAll" v-model="checkAll" @change="checkStatusAll()">
        <label class="form-check-label" for="inputAll" >Prikaži sve volontere</label>

        <input class="form-check-input" type="checkbox" id="inputOver" v-model="checkOver" @change="checkStatusOver()">
        <label class="form-check-label" for="inputOver" >Prikaži samo punoljetne volontere</label>

        <input class="form-check-input" type="checkbox" id="inputUnder" v-model="checkUnder" @change="checkStatusUnder()">
        <label class="form-check-label" for="inputUnder" >Prikaži samo maloljetne volontere</label>
      </div>

        <table class="table table-striped table-bordered table-outlined">
      <thead>
        <tr>
          <th class="custom col1">Ime</th>
          <th class="custom col2">Prezime</th>
          <th class="custom col3">Godine</th>
          <th class="custom col4">email adresa</th>
          <th class="custom col5">Dobne skupine rada</th>
          <th class="custom col6">Ukupan broj sati</th>
          <th class="custom col6">Broj sati prošle godine</th>
          <th class="custom col6">Broj sati ove godine</th>
        </tr>
      </thead>

      <tbody v-if="checkAll">
        <tr v-for="volEach in volonterLista" :key="volEach._id" v-if="volEach">
          <td class="col1">{{ volEach.ime }}</td>
          <td class="col2">{{ volEach.prezime }}</td>
          <td class="col2">{{ volEach.godine }}</td>
          <td class="col2">{{ volEach.email }}</td>
          <td class="col3">{{ formatArray(volEach.dobne_skupine_rada) }}</td>
          <td class="col4">{{ volEach.broj_volonterskih_sati }}</td>
          <td class="col5">{{ volEach.broj_sati_prosle }}</td>
          <td class="col6">{{ volEach.broj_sati_ove }}</td>
        </tr>
      </tbody>

      <tbody v-if="checkOver">
        <tr v-for="volEach in volonterLista" :key="volEach._id" v-if="volEach && volEach.godine>=18">
          <td class="col1">{{ volEach.ime }}</td>
          <td class="col2">{{ volEach.prezime }}</td>
          <td class="col2">{{ volEach.godine }}</td>
          <td class="col2">{{ volEach.email }}</td>
          <td class="col3">{{ formatArray(volEach.dobne_skupine_rada) }}</td>
          <td class="col4">{{ volEach.broj_volonterskih_sati }}</td>
          <td class="col5">{{ volEach.broj_sati_prosle }}</td>
          <td class="col6">{{ volEach.broj_sati_ove }}</td>
        </tr>
      </tbody>

      <tbody v-if="checkUnder">
        <tr v-for="volEach in volonterLista" :key="volEach._id" v-if="volEach && volEach.godine<18">
          <td class="col1">{{ volEach.ime }}</td>
          <td class="col2">{{ volEach.prezime }}</td>
          <td class="col2">{{ volEach.godine }}</td>
          <td class="col2">{{ volEach.email }}</td>
          <td class="col3">{{ formatArray(volEach.dobne_skupine_rada) }}</td>
          <td class="col4">{{ volEach.broj_volonterskih_sati }}</td>
          <td class="col5">{{ volEach.broj_sati_prosle }}</td>
          <td class="col6">{{ volEach.broj_sati_ove }}</td>
        </tr>
      </tbody>
    </table>


    </div>
</template>

<script>
import axios from "axios";

export default{

    name:"sviVolonteri",

    data(){
        return{
        volonterLista:[],
 
      checkOver:false,
      checkUnder:false,
      checkAll:true
        };

    },
    created(){
        this.getVolonteri();
    },

    methods: {

        getVolonteri(){
            axios
            .get("http://localhost:3001/sviVolonteri")
            .then((response)=>{
                this.volonterLista=response.data;
                 for(let i = 0; i < this.volonterLista.length; i++){
                    let vol=this.volonterLista[i];
                    axios.post("http://localhost:3001/volonterCurrentYear", vol)
                    .then((response)=>{
                        vol.broj_sati_ove=response.data.broj_volonterskih_sati;
                    });

                    axios.post("http://localhost:3001/volonterLastYear", vol)
                    .then((response)=>{
                        vol.broj_sati_prosle=response.data.broj_volonterskih_sati;
                    });

                    axios.post("http://localhost:3001/dobneVolontera", vol)
                    .then((response)=>{
                        vol.dobne_skupine_rada=response.data.dobne_skupine_rada;
                    });
                 }
                 console.log(this.volonterLista);
            });
        },

        formatArray(array) {
            return array.length > 0 ? array.join(", ") : "-";
    },
    checkStatusAll(){
         if(this.checkAll){
            this.checkOver=false;
            this.checkUnder=false;
            console.log("check All");
        }
    },
    checkStatusOver(){
         if(this.checkOver){
            this.checkAll=false;
            this.checkUnder=false;
            console.log("check Over");
        }

        if(!this.checkOver && !this.checkUnder)
            this.checkAll=true;
    },

    checkStatusUnder(){
         if(this.checkUnder){
            this.checkAll=false;
            this.checkOver=false;
            console.log("check Over");
        }

        if(!this.checkOver && !this.checkUnder)
            this.checkAll=true;
    },



    },

    };



</script>

<style scoped>

h1{
    margin-top: 30px;
}

.container{
    overflow-y: hidden;
}

.custom-pagination ::v-deep nav{
    padding: 20px;
}

</style>