<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3 v-if="user"> Signed In User : {{user}}</h3>
    <br>
    <div class="signGout" v-if="isSignedIn">
      <button  @click="handleSignOut">logout</button>
    </div>

    <h3>Check this out</h3>
<!-- google Signin -->
    <div class="container">
      <div class="googleSignIn">
        <h2>Google Signin</h2>
        <button @click="handleSignInGoogle">login</button>
      </div>
<!-- twitter signin -->
      <div class="twitterSignIn">
        <h2>Twitter Signin</h2>
        <button @click="handleSignInTwitter">login</button>
      </div>
<!-- facebook signin -->
      <div class="facebookSignIn">
        <h2>Facebook Signin</h2>
        <button @click="handleSignInFacebook">login</button>
      </div>
    </div>
  </div>
</template>

<script>
import firebaseConfig from '../firebaseConfig'
import { getAuth, signInWithPopup,signOut ,  GoogleAuthProvider } from "firebase/auth";

const provider = new GoogleAuthProvider();
const auth = getAuth();

firebaseConfig

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
      return {
        user: '',
        isSignedIn: false,
      }
    },
  methods: {
    handleSignInGoogle(){
      signInWithPopup(auth, provider)
        .then((result) => {

          // console.log(result.user.displayName);
          this.user = result.user.displayName;
          this.isSignedIn = true;
        }).catch((error) => {
          console.log(error)
        });
    },

    handleSignOut(){
      signOut(auth).then(() => {
        this.user = '';
        this.isSignedIn = false;
      }).catch((error) => {
          console.log(error)
      });
    }
  }

}

  
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
