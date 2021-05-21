<template>
  <div style="height:100vh" class="d-flex align-center" >
      <v-col  cols="6" class="mx-auto " >
          <v-card class="cyan lighten-4">
             <v-card-title ><h3 class="mx-auto blue-grey--text" >Login</h3>
             <v-card-text>
                 <v-form >
                     <v-text-field type="number" prepend-icon="fa-user-circle" label="MobileNumber" v-model="mobile"></v-text-field>
                     <v-text-field :type="showPassword ? 'text' : 'password'" prepend-icon="fa-lock" append-icon="fa-eye-slash" label="Password"
                     v-model="password" 
                     @click:append="showPassword=!showPassword"></v-text-field>
                 </v-form>
             </v-card-text>
             <v-divider></v-divider>
             <v-card-actions>
                 <v-btn color="success" class="ml-8" @click="sendData">Log In</v-btn>
             </v-card-actions>
             </v-card-title>
          </v-card>
      </v-col>
      <v-snackbar
      v-model="errorShow.snackbar"
      :timeout="3000"
        top
      rounded="pill"
      centered
    >
      {{ errorShow.text }}
    </v-snackbar> 
  </div>
</template>

<script>
export default {
   layout:'log-layout',
data(){
    return{
showPassword:false,
mobile:'',
password:'',
errorShow:{
 snackbar: false,
      text: 'Incorrect mobile or password'
}
    }
},
methods:{
    sendData(){
        console.log(this.mobile)
        this.$axios.post("/alaapi/login", {
            mobile:this.mobile,
           password:this.password
           },
           {
                 validateStatus() {
                      return true
                    }
           
        }).then(({data}) => {
            console.log(data)
              if (data.errors) {
                  console.log('error')
                    this.errorShow.snackbar = true
                    return false;}
                    this.$router.push('/profile')
        }
        )
        .catch(err => console.log(err))
    }
}
}
</script>

<style>

</style>