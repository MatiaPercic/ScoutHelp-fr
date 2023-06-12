<template>
  <div class="about">
    <h1>Registracija volontera</h1>


    <div class="container">
      <form>
        <div class="row justify-content-center">
          <div class="col-md-2">
            <input
              type="name"
              v-model="name"
              class="form-control"
              id="imputName"
              placeholder="Ime"
            />
          </div>
          <div class="col-md-2">
            <input
              type="surname"
              v-model="surname"
              class="form-control"
              id="imputSurname"
              placeholder="Prezime"
            />
          </div>
          <div class="col-md-1">
            <input
              type="godine"
              v-model="godine"
              class="form-control"
              id="imputAgge"
              placeholder="Godine"
            />
          </div>
        </div>
        <div class="row justify-content-center">
          <div class="col-md-5">
            <input
              type="email"
              v-model="email"
              class="form-control"
              id="exampleInputEmail1"
              placeholder="Enter email"
            />
          </div>
        </div>

        <div class="row justify-content-center ">
          <div class="col-md-3 custom">
            <input
              type="password"
              v-model="password"
              class="form-control"
              id="exampleInputPassword1"
              placeholder="Password"
            />
          </div>
          <div class="col-md-3  custom">
            <input
              type="password"
              v-model="repeatPassword"
              class="form-control"
              id="exampleInputPassword2"
              placeholder="Repeat password"
            />
          </div>
        </div>

        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>



</script>

<style scoped>
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
 .custom{

    width: 270px;
 
 }
 button {
/*   margin: 1em; */
margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;
  --bs-btn-hover-bg: #a020f0;
}
p{
  font-size: smaller;
  opacity: 60%;
  color: #a020f0;
}


</style>
