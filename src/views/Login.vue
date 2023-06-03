<template>

    <div class="about">
        <h1>login page</h1>

 <div class="container">
 <form class="form-horizontal">
 <div class="form-group">

 <label for="exampleInputEmail1" class="plain" >Email address</label>

 <div class="col-sm-10">
 <input 
    type="email" 
    v-model="username"  
    class="form-control"
    id="exampleInputEmail1" 
    aria-describedby="emailHelp" 
    placeholder="Enter
email" />
</div>
</div>

<div class="form-group">
 
 <label for="exampleInputPassword1" class="plain">Password</label>

 <div class="col-sm-10">
 <input 
    type="password" 
    v-model="password"
    class="form-control"
    id="exampleInputPassword1" 
    placeholder="Password"/>
 </div>
</div>

<div class="row"></div>

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