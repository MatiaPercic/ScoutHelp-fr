<template>
    <div class="home">
      
      <h1 class="title">Pregled aktivnosti </h1>
      
      <table>
        <thead>
            <tr>
                <th>Datum</th>
                <th>Opis</th>
                <th>Oblici rada</th>
                <th>Volonteri</th>
                <th>Administratori</th>
                <th>Broj sati</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="akt in aktivnosti" :key="akt._id">
                <td>{{ akt.datum }}</td>
                <td>{{ akt.opis }}</td>
                <td>{{ formatArray( akt.oblik_rada)}}</td>
                <td>{{ formatArray(akt.volonteri) }}</td>
                <td>{{ formatArray(akt.admin) }}</td>
                <td>{{ akt.sati }}</td>
            </tr>
        </tbody>
      </table>

      <pagination
      :records="totalItems"
      :per-page="perPage"
      v-model="currentPage"
      @paginate="promjeneStr"
    />
  
    </div>
    
  </template>

  <script>
import axios from 'axios';
import Pagination from 'vue-pagination-2';


export default{
    name:"aktivnosti",
    components:{
        Pagination,
    },
    data(){
        return{
            totalItems:0,
            aktivnosti:[],
            perPage:3,
            currentPage:1

        };
    },
    created(){
        this.findAktivnosti();
    },
    methods:{
       async findAktivnosti(page=1){
           const response= await axios.post("http://localhost:3001/aktivnostiAll",{
            
            page: this.currentPage,
            limit: this.perPage,
          });
        this.aktivnosti=response.data;
        this.totalItems=response.data.length;
        console.log(this.perPage)
        console.log(this.aktivnosti.length)
    },

    promjeneStr(page) {
      this.currentPage = page;
      this.findAktivnosti();
    },
    formatArray(array) {
      return array.length > 0 ? array.join(', ') : '-';
    },
    
},

}

</script>

<style scoped>

h1 {
  margin-top: 30px;
}



</style>