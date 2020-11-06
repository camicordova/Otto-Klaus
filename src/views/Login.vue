<template>
  <div class="login">
<button @click="socialLogin">Login con Google</button>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/app";
import "firebase/auth";

export default {
  name: 'Login',
  components: {
  },
  data(){
    return{
      email: '',
      password: ''
    }
  },
  methods:{
    logIn() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
          .then( () =>  {
            this.$router.replace('home')
          })
          .catch(function(error) {
            console.log(error.message)
            alert(error.message)
          });
    },
    socialLogin(){
      const provider = new firebase.auth.GoogleAuthProvider();
      firebase.auth().signInWithPopup(provider).then((result)=>{
      this.$router.replace('home');
      }).catch((err)=>{
        alert(err.message)
      });      
    }
  }
}
</script>