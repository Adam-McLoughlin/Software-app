<template>
  <!--Page for registering an account-->

  <div class="container">
    <h1>Create An Account</h1>
    <div class="form-group">
      <br />
      <label for="InputEmail">Email Address</label>
      <input
        type="contact"
        v-model="email"
        class="form-control"
        id="InputEmail"
        aria-describedby="emailHelp"
        placeholder="Enter Email"
      />
    </div>
    <br>
    <div class="form-group">
      <label for="exampleInputPassword1">Password</label>
      <input
        type="password"
        v-model="password"
        class="form-control"
        id="InputPassword"
        placeholder="Password"
      />
      <small id="emailHelp" class="form-text text-muted">We'll never share your email or password with anyone else.</small>
    </div>
    <br />
    <!--Button adds new user to database-->
    <button @click="register" class="btn btn-primary">Create Account</button>
  </div>
</template>

<script>
import app from "../api/firebase";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
import {
  getFunctions,
  httpsCallable,
  connectFunctionsEmulator,
} from "firebase/functions";
export default {
  name: "Register",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    register() {
      // firebase function that gets authorisation information
      const auth = getAuth(app);
      // firebase function to add new user to our authentication database
      createUserWithEmailAndPassword(auth, this.email, this.password)
        .then((userCredential) => {
          // Signed in
          const user = userCredential.user;
          console.log(user);
          // Redirects to home page
          this.$router.push("/");
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          console.log(errorCode);
          console.log(errorMessage);
        });
    },
  },
};
</script>

<style scoped>

  h1{
    line-height:100px;
  }

  input{
    width:25%;
    margin-left: auto;
    margin-right: auto;
  }

</style>
