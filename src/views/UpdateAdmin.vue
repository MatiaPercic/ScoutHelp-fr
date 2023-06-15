<template>
  <div class="home">
    <h1 class="title">Izmijena osobnih podataka</h1>

    <div class="container">
      <form>
        <div class="row justify-content-center">
          <div class="col-md-2">
            <input
              type="name"
              v-model="admin_new.new_ime"
              class="form-control"
              id="imputName"
              :placeholder="admin.ime"
              required
            />
          </div>
          <div class="col-md-2">
            <input
              type="surname"
              v-model="admin_new.new_prezime"
              class="form-control"
              id="imputSurname"
              :placeholder="admin.prezime"
              required
            />
          </div>
          <div class="col-md-1">
            <input
              type="godine"
              v-model="admin_new.new_godine"
              class="form-control"
              id="imputAgge"
              :placeholder="admin.godine"
              required
            />
          </div>
        </div>

        <div class="row justify-content-center">
          <div class="col-md-5 custom">
            <input
              type="text"
              v-model="admin_new.new_pozicija"
              class="form-control"
              id="exampleInputPassword1"
              :placeholder="admin.pozicija"
              required
            />
          </div>
        </div>

        <div class="row justify-content-center">
          <div class="col-md-3 custom">
            <input
              type="text"
              v-model="admin_new.new_password"
              class="form-control"
              id="exampleInputPassword1"
              :placeholder="admin.password"
              required
            />
          </div>
        </div>

        <button type="button" @click.prevent="update()" class="btn btn-primary">
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
  name: "updateAdmin",
  data() {
    return {
      admin: {
        ime: "",
        prezime: "",
        godine: "",
        password: "",
        pozicija: "",
      },

      admin_new: {
        email: "",
        new_ime: "",
        new_prezime: "",
        new_godine: "",
        new_password: "",
        new_pozicija: "",
      },
      response: false,
    };
  },
  created() {
    this.info();
  },
  methods: {
    info() {
      this.admin.ime = localStorage.getItem("ime");
      this.admin.prezime = localStorage.getItem("prezime");
      this.admin.godine = localStorage.getItem("godine");
      this.admin.password = localStorage.getItem("password");
      this.admin_new.email = localStorage.getItem("email");
      this.admin.pozicija = localStorage.getItem("pozicija");
    },

    async set() {
      localStorage.setItem("ime", this.admin_new.new_ime);
      localStorage.setItem("prezime", this.admin_new.new_prezime);
      localStorage.setItem("godine", this.admin_new.new_godine);
      localStorage.setItem("password", this.admin_new.new_password);
      localStorage.setItem("pozicija", this.admin_new.new_pozicija);
    },
    async update() {
        if (
        !this.admin_new.new_ime ||
        !this.admin_new.new_prezime ||
        !this.admin_new.new_godine ||
        !this.admin_new.new_pozicija ||
        !this.admin_new.new_password 
      )
        alert("Sva polja moraju biti upisana!");
    else{

      axios
        .put("http://localhost:3001/updateAdmin", this.admin_new)
        .then((response) => {
          if (response) {
            alert("Uspiješno izmijenjeni osobni podaci!");
            this.set();
            this.$router.push({
              name: "profilAdmin",
            });
          } else alert("Greška pri izmijeni podataka");
          console.log(this.admin_new);
          console.log(this.admin);
        });
    }
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
