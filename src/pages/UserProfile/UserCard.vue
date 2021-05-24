<template>
  <card class="card-user">
    <!-- <div slot="image">
      <img src="@/assets/img/background.jpg" alt="...">
    </div> -->
    <div>
      <div class="author">
        <img class="avatar border-white" src="@/assets/img/faces/face-1.jpg" alt="...">
        <h4 class="title">{{user.name}}
          <br>
          <a href="#">
            <small>@{{user.name}}</small>
          </a>
        </h4>
      </div>
      <!-- <p class="description text-center">
        "I like the way you work it
        <br> No diggity
        <br> I wanna bag it up"
      </p> -->
    </div>
    <hr>
    <div class="text-center">
      <div class="row">
        <div v-for="(info, index) in details" :key="index" :class="getClasses(index)">
          <h5>{{info.title}}
            <br>
            <small>{{info.subTitle}}</small>
          </h5>
        </div>
      </div>
    </div>
  </card>
</template>
<script>
import db from "../../components/firebaseInit"
class User{
  constructor(name,age,gender) {
    this.age = age;
    this.name = name;
    this.gender = gender;
    // this. = author;
    // this.img = img;
  }
}
export default {
  data() {
    return {
      user:null,
      details:[]
    
      // accountStatus: "Active",
      
    };
  },
  methods: {
    getClasses(index) {
      var remainder = index % 3;
      if (remainder === 0) {
        return "col-lg-3 offset-lg-1";
      } else if (remainder === 2) {
        return "col-lg-4";
      } else {
        return "col-lg-3";
      }
    }
  },

  mounted() {
    db.collection('Bank').get().then((querySnapshot) => {
            querySnapshot.forEach((doc) => {
            
              var i;
              for(i in doc.data()){
                // console.log(doc.data()[i])
                // this.sdata=new Post(doc.data()[i].AccountId,doc.data()[i].name)
                // this.postList.push(this.sdata)
                
                if(doc.data()[i].AccountId == this.$route.params.id){
                  var customer = doc.data()[i]
                  
                  this.user=new User(customer.name,customer.Age,customer.Gender)
                  this.details=[
                        {
                          title: this.user.age,
                          subTitle: "Age"
                        },
                        {
                          title: this.user.gender,
                          subTitle: "Gender"
                        },
                        {
                          title:"Active",
                          subTitle: "Status"
                        }
                      ]
                      break
                  
                }
              }      
            })
          })
   
    // console.log(this.user.name, this.user.age, this.user.gender)
    
      // console.log(this.details)
    // if(this.$route.params.id){
    //   this.user.accountNumber = this.$route.params.id;
    // }
      
    }
  };
</script>
<style>
</style>