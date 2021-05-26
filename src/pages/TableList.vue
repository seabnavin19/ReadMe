<template>
<div>
  <div class="row m-3">
   <h2> Service and Product Recommendation</h2>
   
  </div>

  
  <div class="alert alert-success" v-if="success">
            <button @click="cancel()" type="button" aria-hidden="true" class="close">×</button>
            <span>
              <b> Success - </b> This is a regular notification made with ".alert-success"</span>
          </div>
  <form class="mb-2">
  <div class="form-group ">
      <label>Description</label>
      <textarea name="description" id="description" rows="3"></textarea>
    </div>
  <div class="form-row">
    <div class="form-group col-md-6">
      <label for="inputEmail4">Age</label>
      <input type="number" class="form-control" id="inputEmail4" placeholder="Age" max="100" min="18">
    </div>
    <div class="form-group col-md-6">
      <label for="inputState">Group</label>
      <select id="inputState" class="form-control">
        <option selected>Choose...</option>
        <option>Group 1</option>
        <option>Group 2</option>
        <option>Group 3</option>
      </select>
    </div>
  </div>
  <div class="form-row">
    <div class="form-group col-md-6">
      <label for="inputState">Services</label>
      <select id="inputState" class="form-control">
        <option selected>Choose...</option>
        <option>Personal Loan</option>
        <option>Home Loan</option>
        <option>Personal Cheque</option>
      </select>
    </div>
    <div class="form-group col-md-2">
      <label for="inputState">Gender</label>
      <select id="inputState" class="form-control">
        <option selected>Choose...</option>
        <option>Male</option>
        <option>Female</option>
        <option>Other</option>
      </select>
    </div>
    <div class="form-group col-md-4">
      <label for="inputCity">Fee</label>
      <input type="number" class="form-control" id="inputFee" placeholder="$" >
    </div>
  </div>
 
</form>
<div class="row">
<div class="col-4"></div>
 <button class=" col-3 btn btn-primary" @click="searchCus">submit</button></div>
<div class="row mb-3">
  <div class="col-10">
  </div>
  <div class="col">
    <button class="btn btn-success" @click="give()">Recommend</button>
  </div>
</div>
<table class="table table-success table-striped h-25 ">
  <thead >
    <tr >
      <th scope="col" >Account Number</th>
      <th scope="col">Name</th>
      <!-- <th scope="col">Last</th>
      <th scope="col">Handle</th> -->
    </tr>
  </thead>
  
  <tbody>
   
       
    <tr v-for="(post,index) in postList" v-if="index<=5">
  
      <th scope="row">{{post.id}}</th>
      <td>{{post.name}}</td>

      <td><button class="btn btn-dark"> <router-link :to="{ name: 'stats', params: { id:post.id,name:post.name } }">View</router-link></button></td>

      <!-- <td>Otto</td>
      <td>@mdo</td> -->
    </tr>
    <!-- <tr v-if=""></tr> -->
       
  </tbody>
</table>


</div>


  
</template>
<style>
*{
  margin: 0;
  padding: 0;
}
form{
  background-color:rgb(241, 236, 236);
  padding: 5%;
  box-shadow: rgb(201, 198, 198) 1px 1px 5px;
}
table{
  width: 100%;
}
textarea{
  width: 100%;
  border: medium none;
  border-radius: 4px;
  font-size: 14px;
  padding: 7px 18px;
  background-color: #fffcf5;
}

</style>
<script>

import db from '../components/firebaseInit';

class Post {
  constructor(id, name) {
    this.id = id;
    this.name = name
    // this. = author;
    // this.img = img;
  }
}

export default {
  data() {
    return {
      sdata:null,
      success:false,
      postList:[],
    }
  },

  mounted() {
    
  },
  methods: {
    give(){
      this.success=true
    },
    cancel(){
      this.success=false
    },
    searchCus(){
      db.collection('Bank').get().then((querySnapshot) => {
      
          querySnapshot.forEach((doc) => {
            // console.log(doc)
         
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              if(i.includes("user")){
                
                var cus=doc.data()[i]
                // console.log(cus);
                if (cus.Group==1 && cus.Gender=="Female"){
                  console.log(cus)
                  this.sdata=new Post(cus.AccountId,cus.name)
                  this.postList.push(this.sdata)
                }
                
              
                // console.log(cus)
              }
             
           
              
            }
            // this.sdata=doc.data()
            // console.log(this.sdata)

            
      
          })
        })

    }
  },

};
</script>
