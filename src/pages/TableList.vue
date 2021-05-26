<template>
 
  <form>
  <div class="form-group">
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
        <option>Service 1</option>
        <option>Service 2</option>
        <option>Service 3</option>
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
  <button type="submit" class="btn btn-primary">submit</button>
</form>
  
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
     sdata=null,
    
    };
  },

  mounted() {
    db.collection('Bank').get().then((querySnapshot) => {
      
          querySnapshot.forEach((doc) => {
            // console.log(doc)
         
            var i;
            var l=[]
            for(i in doc.data()){
              // console.log(doc.data()[i])
              if(i.includes("user")){
                 this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
               this.postList.push(this.sdata)
              console.log(i)
              }
             
              this.load=false
              
            }
            // this.sdata=doc.data()
            // console.log(this.sdata)

            
      
          })
        })
  },

};
</script>
