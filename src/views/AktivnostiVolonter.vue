<template>
  <div class="home">
    <h1 class="title">Pregled osobnih aktivnosti</h1>

    <h3 v-if="totalItems==0"> Ni jedna osobna aktivnosti nije evidentirana</h3>
    
    <table v-if="totalItems>0" class="table table-striped table-bordered table-outlined">
      <thead>
        <tr>
          <th class="custom col1">Datum</th>
          <th class="custom col2">Opis</th>
          <th class="custom col3">Oblici rada</th>
          <th class="custom col4">Volonteri</th>
          <th class="custom col5">Administratori</th>
          <th class="custom col6">Broj sati</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="akt in records" :key="akt._id" v-if="akt">
          <td class="col1">{{ akt.datum }}</td>
          <td class="col2">{{ akt.opis }}</td>
          <td class="col3">{{ formatArray(akt.oblik_rada) }}</td>
          <td class="col4">{{ formatArray(akt.volonteri) }}</td>
          <td class="col5">{{ formatArray(akt.admin) }}</td>
          <td class="col6">{{ akt.sati }}</td>
        </tr>
      </tbody>
    </table>

    <pagination
      :records="totalItems"
      :per-page="perPage"
      v-model="currentPage"
      @paginate="promjeneStr"
      :options="paginationOptions"
    />

    <button type="button" @click="buttonProfil()" class="btn btn-primary">
          Povratak na profil
       </button>
  </div>
</template>

<script>
import axios from "axios";
import Pagination from "vue-pagination-2";

export default {
  name: "aktivnostiVolonter",
  components: {
    Pagination,
  },
  data() {
    return {
      volonter:{
        email:localStorage.getItem("email")
      },
      totalItems: 0,
      aktivnosti: [],
      perPage: 5,
      currentPage: 1,
      records: [],
      paginationOptions: {
        texts: {
          count: "",
        },
      },
    };
  },
  created() {
    this.findAktivnostiVolonter();
  },
  computed: {
    totalPages() {
      return Math.ceil(this.aktivnosti.length / this.perPage);
    },
  },

  methods: {
    findAktivnostiVolonter() {
      axios
      .post("https://scouthelp-f893.onrender.com/aktivnostiVolonter", this.volonter)
      .then((response) => {
        this.aktivnosti = response.data;
        this.totalItems = response.data.length;
        this.promjeneStr(this.currentPage);
        console.log(this.totalItems);
        console.log(this.currentPage);
      });
    },

    promjeneStr: function (currentPage) {
      console.log(this.currentPage);
      this.records = [];
      let start = this.perPage * (this.currentPage - 1);
      let end = start + this.perPage - 1;
      for (let i = start; i <= end; i++) {
        if (this.aktivnosti[i]) this.records[i] = this.aktivnosti[i];
      }
      console.log(this.records);
    },

    formatArray(array) {
      return array.length > 0 ? array.join(", ") : "-";
    },
    buttonProfil(){
      this.$router.push({
        name:"profilVolonter"
      });
    },


  },
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

.table{
  margin-top: 40px;
}
.custom {
  text-align: center;
  color: white;
  background-color: #a020f0;
}

.col2 {
  width: 200px;
}
.col3 {
  width: 200px;
}

.col4 {
  width: 450px;
}

.col5 {
  width: 300px;
}

.col6 {
  width: 100px;
}

button {
  margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;
  margin-left: 10px;
}

.btn:hover {
  background-color: #a020f0;
  color: #fff;
}
</style>
