<template>
<div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">Otto Klaus</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item" v-if="$route.path!='/home'">
                    <a class="nav-link" href="/">Volver a lista de juguetes <span class="sr-only">(current)</span></a>
                </li>
            </ul>
            <div class="form-inline my-2 my-lg-0">
                <button class="btn btn-outline-success my-2 my-sm-0" type="button" @click="logOut" v-if="user">Cerrar Sesión</button>
            </div>
        </div>
    </nav>
    <router-view />
</div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/app";
import "firebase/auth";

export default {
    name: "app",
    data() {
        return {
            user: null
        }
    },
    mounted(){
      var that = this;
      firebase.auth().onAuthStateChanged( (user) => {
        that.user=user;
    })
    },
    methods: {
        logOut() {
            firebase
                .auth()
                .signOut()
                .then(() => {
                    this.$router.replace('/')
                })
        }
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
</style>
