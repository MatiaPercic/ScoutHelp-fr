<template>
  <div class="about">
    <h1>Unos nove aktivnosti</h1>

    <div class="grupni">
      <div class="row row1">
        <div class="col-4 custom-date">
          <label for="example-datepicker" class="cal-label"
            >Odaberi datum</label
          >
          <b-form-datepicker
            id="example-datepicker"
            placeholder="Odaberi datum"
            v-model="value"
            class="mb-2"
            :start-weekday="1"
            :date-format-options="{
              year: 'numeric',
              month: 'numeric',
              day: 'numeric',
            }"
            menu-class="w-100"
            calendar-width="100%"
            locale="hr"
          ></b-form-datepicker>

          <p>Prikaz u tablici aktivnosti: '{{ value }}'</p>
        </div>

        <div class="col-md-5 custom-opis" style="align-self: center">
          <input
            class="opis-custom"
            v-model="odabirOpis"
            type="text"
            id="input-opis"
            placeholder="Unesi Opis"
          />
        </div>

        <div class="col-md-2 custom-sati">
          <label for="satiID"><b>Unesi broj sati</b></label>
          <input type="number" id="satiID" v-model="odabirSati" min="1" />
        </div>
      </div>

      <div class="row row2">
        <div class="col-md-4">
          <b-form-select
            v-model="odabirVolonter"
            @input="dodajVolonter"
            class="custom-volInput"
          >
            <option value="" disabled selected>Odaberi volontere</option>
            <option
              v-for="volonter in volonteriOpcije"
              :key="volonter"
              :value="volonter"
            >
              {{ volonter }}
            </option>
          </b-form-select>

          <button @click="volIzbrisi" class="cancelVol">Izbriši odabir</button>

          <b-form-select
            v-model="odabirAdmini"
            @input="dodajAdmin"
            class="custom-admInput"
          >
            <option value="" disabled selected>Odaberi administratore</option>
            <option v-for="adm in adminiOpcije" :key="adm" :value="adm">
              {{ adm }}
            </option>
          </b-form-select>

          <button class="cancelAdm" @click="admIzbrisi">Izbriši odabir</button>

          <b-form-select
            v-model="odabirOblici"
            @input="dodajOblik"
            class="custom-oblInput"
          >
            <option value="" disabled selected>Odaberi oblike rada</option>
            <option v-for="oblik in obliciOpcije" :key="oblik" :value="oblik">
              {{ oblik }}
            </option>
          </b-form-select>

          <button @click="oblIzbrisi" class="cancelObl">Izbriši odabir</button>
        </div>

        <div class="col-md-2 custom-volIspis">
          <p>Trenutan Odabir Volontera:</p>
          <b v-for="volonter in new_aktivnost.volonteri" :key="volonter">
            {{ volonter }}
            <br />
          </b>
        </div>

        <!--  -->
        <div class="col-md-3 custom-admIspis">
          <p>Trenutan Odabir administratora:</p>
          <b v-for="adm in new_aktivnost.admin" :key="adm">
            {{ adm }}
            <br />
          </b>
        </div>

        <div class="col-md-2 custom-oblIspis">
          <p>Trenutan Odabir oblika rada:</p>
          <b v-for="oblik in new_aktivnost.oblik_rada" :key="oblik">
            {{ oblik }}
            <br />
          </b>
        </div>
      </div>

      <div class="row row3 justify-content-center">
        <div class="col-2">
          <button class="profButton">Povratak na profil</button>
        </div>
        <div class="col-2">
        <button class="newaktButton">Unesi novu aktivnost</button>
      </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "novaAktivnost",

  data() {
    return {
      value: null,
      weekday: 1,
      hideHeader: true,

      odabirVolonter: "",
      volonteriOpcije: [],

      adminiOpcije: [],
      odabirAdmini: "",

      odabirOblici: "",
      obliciOpcije: [],

      odabirSati: 0,
      odabirOpis: "",

      new_aktivnost: {
        datum: "",
        opis: "",
        oblik_rada: [],
        volonteri: [],
        admin: [],
        sati: "",
      },
    };
  },
  created() {
    this.getVolonteriOpcije();
    this.getAdminiOpcije();
    this.getObliciOpcije();
  },

  methods: {
    getVolonteriOpcije() {
      axios.get("http://localhost:3001/volonteriEmail").then((response) => {
        for (let i = 0; i < response.data.length; i++)
          this.volonteriOpcije.push(response.data[i].email);
      });
    },
    dodajVolonter() {
      if (
        this.odabirVolonter &&
        !this.new_aktivnost.volonteri.includes(this.odabirVolonter)
      ) {
        this.new_aktivnost.volonteri.push(this.odabirVolonter);
        this.odabirVolonter = "";
      }

      console.log(this.new_aktivnost.volonteri);
    },
    volIzbrisi() {
      this.new_aktivnost.volonteri = [];
    },

    getAdminiOpcije() {
      axios.get("http://localhost:3001/adminiEmail").then((response) => {
        for (let i = 0; i < response.data.length; i++)
          this.adminiOpcije.push(response.data[i].email);
      });
    },
    dodajAdmin() {
      if (
        this.odabirAdmini &&
        !this.new_aktivnost.admin.includes(this.odabirAdmini)
      ) {
        this.new_aktivnost.admin.push(this.odabirAdmini);
        this.odabirAdmini = "";
      }
    },
    admIzbrisi() {
      this.new_aktivnost.admin = [];
    },

    getObliciOpcije() {
      axios.get("http://localhost:3001/obliciRada").then((response) => {
        for (let i = 0; i < response.data.length; i++)
          this.obliciOpcije.push(response.data[i].opis);
      });
    },
    dodajOblik() {
      if (
        this.odabirOblici &&
        !this.new_aktivnost.oblik_rada.includes(this.odabirOblici)
      ) {
        this.new_aktivnost.oblik_rada.push(this.odabirOblici);
        this.odabirOblici = "";
      }
    },
    oblIzbrisi() {
      this.new_aktivnost.oblik_rada = [];
    },
  },
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

.grupni {
  margin-left: 20px;
  margin-right: 20px;
}
.row1 .row2 {
  margin-top: 50px;
}
.cal-label {
  margin-left: 0%;
  text-align: left;
  font-size: 20px;
}

.opis-custom {
  width: 400px;
  text-align: justify;
  font-size: 18px;
  opacity: 65%;
  border-block-color: #a020f0;
  border-width: 2px;
}

select {
  width: 250px;
  height: 30px;
  font-size: 15px;
  margin-left: -30px;
  margin-bottom: 50px;
}

.custom-sati {
  margin-top: 30px;
}

.custom-date {
  margin-top: 20px;
}

button {
  margin: 5px;
}

.row3{
  margin-top: 20px;
}
.newaktButton .profButton{
  width: 100px;

}
</style>
