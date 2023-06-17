<template>
    <div class="home">
      
      <h1 class="title">Pregled aktivnosti </h1>
      
      <table class="table table-striped">
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
            <tr  v-for="akt in records" :key="akt._id" v-if="akt">
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
            currentPage:1,
            records:[]

        };
    },
    created(){
        this.findAktivnosti()        
    },
    computed: {
  totalPages() {
    return Math.ceil(this.aktivnosti.length / this.perPage);
  }
},

    methods:{
       findAktivnosti(){
            axios
            .post("http://localhost:3001/aktivnostiAll")
            .then((response)=>{
                this.aktivnosti=response.data;
                this.totalItems=response.data.length;
                this.promjeneStr(this.currentPage);
                console.log(this.totalItems);
                console.log(this.currentPage);
            })
    },

    promjeneStr: function(currentPage) {
      console.log(this.currentPage);
      this.records=[];
      let start=this.perPage*(this.currentPage-1);
        let end=start+this.perPage-1;
        for(let i=start;i<=end;i++){
            if(this.aktivnosti[i])
                this.records[i]=this.aktivnosti[i];
        };
        console.log(this.records);
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