<template>
  <div id="app" class="app">

    <div class="header">

      <h1>Sistemas Reservaciones Online</h1>
      <nav>
        <button v-on:click="init" v-if="is_auth" > Datos registrados </button>
        <button v-on:click="getBalance" v-if="is_auth" > Funcion 2 </button>
        <button v-on:click="doTransaction" v-if="is_auth" > Registrar cliente </button>
        <button v-on:click="logOut" v-if="is_auth" >Salir</button>
      </nav>
    </div>
    
    

    <div class="main-component">
      <router-view  v-on:log-in="logIn" ></router-view>
    </div>
    


    <div class="footer">
        <h2>Consola de administración - MisiónMinTIC2022 (c) 2020</h2>
    </div>


  </div>
</template>









<script>


import vueRouter from 'vue-router'

export default {
  name: 'App',

  data: function(){
      return{ 
        is_auth: localStorage.getItem('isAuth') || false
      

        
      }    
  },

  components: {
  },

  methods:{
    updateAuth: function(){
      var self = this
      self.is_auth  = localStorage.getItem('isAuth') || false

      if(self.is_auth == false)
        self.$router.push({name: "user_auth"})

      else{
        let username = localStorage.getItem("current_username")
        this.$router.push({ name: "user", params: { userData: JSON.parse(username) } })
      }  
    },

    logIn: function(username,id){
      localStorage.setItem('current_username', username)
      //localStorage.setItem('current_id', username)
      localStorage.setItem('isAuth', true)
      this.updateAuth()
    },

    logOut: function(){
      localStorage.removeItem('isAuth')
      localStorage.removeItem('current_username')
      this.updateAuth()
    },

    init: function(){
      if(this.$route.name != "user"){
        let username = localStorage.getItem("current_username")
        this.$router.push({name: "user", params:{ userData: JSON.parse(username) }})
      }
      
    },

    getBalance: function(){
      if(this.$route.name != "user_balance"){
        let username = localStorage.getItem("current_username")
        this.$router.push({name: "user_balance", params:{ username: username }})
      }
    },


    doTransaction: function(){
      
        let username = localStorage.getItem("current_username")
        this.$router.push({name: "user_transaction", params:{ username: username }})
    }
    
  },

  created: function(){
    //this.$router.push({name: "root"})
    this.updateAuth()
  }
  

}
</script>









<style>

  body{
    margin: 0 0 0 0;
  }

  .header{
    margin: 0%;
    padding: 0;
    width: 100%;
    height: 10vh; 
    min-height: 100px;

    background-color: #283747 ;
    color:#E5E7E9  ;

    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header h1{
    width: 40%;
    text-align: center;
  }

  .header nav {
    height: 100%;
    width: 60%;

    display: flex;
    justify-content: space-around;
    align-items: center;

    font-size: 20px;
  }

  .header nav button{
    color: #E5E7E9;
    background: #283747;
    border: 1px solid #E5E7E9;

    border-radius: 5px;
    padding: 10px 20px;
  }

  .header nav button:hover{
    color: #283747;
    background: #E5E7E9;
    border: 1px solid #E5E7E9;
  }

  
  .main-component{
    height: 75vh;
    margin: 0%;
    padding: 0%;

    background: #FDFEFE ;
  }

 
  .footer{
    margin: 0;
    padding: 0;
    width: 100%;
    height: 10vh;
    min-height: 100px; 

    background-color: #283747;
    color: #E5E7E9;

  }

  .footer h2{
    width: 100%;
    height: 100%;
    
    display: flex;
    justify-content: center;
    align-items: center;
  }

</style>


