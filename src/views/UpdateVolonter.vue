<template>
  <div class="home">
    <h1 class="title">Izmijena osobnih podataka</h1>

    <div class="container">
      <form>
        <div class="row justify-content-center">
          <div class="col-md-2">
            <input
              type="name"
              v-model=volonter_new.new_ime
              class="form-control"
              id="imputName"
              :placeholder="volonter.ime"
              required
            />
          </div>
          <div class="col-md-2">
            <input
              type="surname"
              v-model=volonter_new.new_prezime
              class="form-control"
              id="imputSurname"
              :placeholder="volonter.prezime"
              required
            />
          </div>
          <div class="col-md-1">
            <input
              type="godine"
              v-model=volonter_new.new_godine
              class="form-control"
              id="imputAgge"
              :placeholder="volonter.godine"
              required
            />
          </div>
        </div>

        <div class="row justify-content-center">
          <div class="col-md-3 custom">
            <input
              type="text"
              v-model=volonter_new.new_password
              class="form-control"
              id="exampleInputPassword1"
              :placeholder="volonter.password"
              required
            />
          </div>
        </div>

        <button type="button" @click="update()" class="btn btn-primary">
          Izmijena
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import router from "@/router";
import axios from "axios";


export default {
    name: "updateVolonter",
    data() {
        return {
            volonter:{
                ime: "",
                prezime: "",
                godine: "",
                password: "",
            },

            volonter_new: {
                email:"",
                new_ime: "",
                new_prezime: "",
                new_godine: "",
                new_password: "",
            },
            response: false,
        };
    },
    created() {
        this.info();
    },
    methods: {
        info() {
            this.volonter.ime = localStorage.getItem("ime");
            this.volonter.prezime = localStorage.getItem("prezime");
            this.volonter.godine = localStorage.getItem("godine");
            this.volonter.password = localStorage.getItem("password");
            this.volonter_new.email=localStorage.getItem("email");
        },
        async set(){
            localStorage.setItem("ime", this.volonter_new.new_ime);
            localStorage.setItem("prezime", this.volonter_new.new_prezime);
            localStorage.setItem("godine", this.volonter_new.new_godine);
            localStorage.setItem("password",this.volonter_new.new_godine);
        },
        async update() {
            axios
                .put("http://localhost:3001/updateVolonter", this.volonter_new)
                .then((response) => {
                if (response) {
                    alert("Uspiješno izmijenjeni osobni podaci!");
                }
                else
                    alert("Greška pri izmijeni podataka");
                console.log(this.volonter_new);
                console.log(this.volonter);
            });
        },
    },
  
};
</script>

<style scooped>
h1 {
  margin-top: 30px;
}

.container {
  padding-left: 20px;
  padding-top: 50px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.form-control {
  text-align: justify;
  font-size: 18px;
  opacity: 65%;
  border-block-color: #a020f0;
  border-width: 2px;
  margin-bottom: 20px;
  margin-top: 30px;
}
</style>
