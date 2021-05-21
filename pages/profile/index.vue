<template>
  <div>
    <v-card color="#80D8FF">
      <div class="d-flex">
        <v-card-title>Profile</v-card-title>
        <v-spacer></v-spacer>
        <v-card-title class="black--text subtitle-1" @click="logout"
          >Log out
        </v-card-title>
      </div>
      <v-card-text>
        <v-form ref="form">
          <v-text-field
            :rules="[v => !!v || 'Name is required']"
            label="First Name"
            v-model="firstName"
          ></v-text-field>
          <v-text-field
            :rules="[v => !!v || 'last Name is required']"
            label="Last Name"
            v-model="lastName"
          ></v-text-field>
          <v-text-field
            :rules="emailRules"
            label="E-mail"
            v-model="email"
          ></v-text-field>
          <v-select
            label="State"
            :items="stateItem"
            item-text="title"
            item-value="id"
            v-model="ostan"
            required
          ></v-select>
          <v-select label="City" :items="shahrha" item-text="title" item-value="id" required></v-select>
          <v-select label="Gender" :items="genderItem" item-text="title" item-value="id" required></v-select>
          <v-select label="Grade" :items="gradesItem" item-text="title" item-value="id"  required></v-select>
          <v-select label="Major" :items="majorItem" item-text="title" item-value="id"  required></v-select>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-btn color="success" @click="sendData">submit</v-btn>
        <v-btn @click="reset">clear</v-btn>
      </v-card-actions>
    </v-card>
          <v-snackbar
      v-model="sucssSendData.snackbar"
      :timeout="3000"
        top
        color="success"
        content-class="text-center"
      rounded="pill"
      centered
    >
      {{ sucssSendData.text }}
    </v-snackbar> 
     <v-snackbar
      v-model="erorrData.snackbar"
      :timeout="3000"
        top
        color="red"
        content-class="text-center"
      rounded="pill"
      centered
    >
      {{ erorrData.text }}
    </v-snackbar> 
  </div>
</template>

<script>
export default {
  data() {
    return {
      sucssSendData:{
      snackbar: false,
      text: 'Your data was saved successfully'
},    erorrData:{
      snackbar: false,
      text: 'Fill all fields '
},
      ostan: null,
      shahrhas: [],
      firstName: null,
      lastName:null,
      email: null,
      stateItem: [""],
      cityItem: [""],
      genderItem: [""],
      gradesItem: [""],
      majorItem: [""],
      data: null,
      error: null,
      emailRules: [
        v => !!v || "E-mail is required",
        v => /.+@.+\..+/.test(v) || "E-mail must be valid"
      ],
    };
  },
  mounted() {
    this.loadDatas();
  },
  computed: {
    shahrha(){
      return this.shahrhas.filter(({province}) => province.id === this.ostan)
    }
  },
  methods: {
    logout() {
      this.$router.push("/");
    },
    reset() {
      this.$refs.form.reset();
    },

    async loadDatas() {
      //  try{
      await this.$axios.get("/alaapi/megaroute/getUserFormData").then(datas => {
        console.log(datas);
        this.stateItem = datas.data.data.provinces
        this.shahrhas = datas.data.data.cities
        this.genderItem = datas.data.data.genders
        this.gradesItem = datas.data.data.grades
        this.majorItem = datas.data.data.majors
      });
      //    } catch (error) {
      //   this.data = null;
      //   this.error = error;
      // }
    },
    sendData(){
      if(this.firstName!=null&&this.lastName!=null&&this.email!=null){
        this.sucssSendData.snackbar = true

      }
      else {
         this.erorrData.snackbar = true
      }
    }
  }
};
</script>

<style lang="scss">
.v-card__title.black--text:hover {
  color: #ff0606 !important;
  cursor: pointer;
  transition: all 0.5s ease;
}
</style>
