<template>
<div class="register">
        <h1>Registracija</h1>

<div class="container">

 <form>

 <div class="form-row ">
    <div class="col-md-4 mb-3">
        <label for="imputName" class="plain">Ime</label>

    <div class="col-sm"></div>

    <input 
    type="name" 
    v-model="name"
    class="form-control"
    id="imputName" 
    placeholder="Ime" />
    </div>
    
    <br>

    <div class="col-md-4 mb-3">
        
    <label for="imputSurname" class="plain">Prezime</label>

        <div class="col-sm"></div>

    <input 
    type="surname" 
    v-model="surname"
    class="form-control"
    id="imputSurname" 
    placeholder="Prezime" />

    </div>
    
</div>
<br>
<div class="form-group">

 <label for="exampleInputEmail1" class="plain">Email address</label>

 <div class="col-sm"></div>

    <input 
    type="email" 
    v-model="username"
    class="form-control"
    id="exampleInputEmail1" 
    placeholder="Enter email" />

 </div>

 <br>

 <div class="form-group">

 <label for="exampleInputPassword1" class="plain">Password</label>

 <div class="col-sm"></div>

 <input 
    type="password" 
    v-model="password" 
    class="form-control"
    id="exampleInputPassword1" 
    placeholder="Password" />

 </div>

 <br>

 <div class="form-group">

 <label for="exampleInputPassword1" class="plain">Repeat password</label>

 <div class="col-sm"></div>

 <input 
    type="password" 
    v-model='repeatPassword' 
    class="form-control"
    id="exampleInputPassword2" 
    placeholder="Password" />
 </div>

 <br>

 <div class="form-group">        
      <div class="col-sm-offset-2 col-sm-10">

 <button type="button" class="btn btn-primary"
 style="
        margin: 2em;
        font-weight: bold;
        font-size: large;
        font-family: Arial;
        color: #A020F0;
        background-color: #fff;
        border-color: #A020F0;
        
      "
      >Submit</button>
      </div>
 </div>
 </form>
 </div>
 <div class="col-sm"></div>
</div>

    
</template>

<style scoped>

.plain {
    text-align: justify;
    font-size: 20px;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bold;
    row-gap: 5;
    
}

.form-control  {
    text-align: justify; 
    font-size: 20px;
    font-weight: unset;
    border-block-color: #A020F0;
}
</style>