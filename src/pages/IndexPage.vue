<template>
  <div class="screen">
    <div class="left_screen">
      <div class="ball_1"></div>
      <div class="ball_2"></div>
      <img src="../assets/logo.png" class="img_logo" />
      <div class="title">
        <h1 id="title_name">UNIRIDE</h1>
      </div>
    </div>
    <div class="right_screen">
      <div class="text">
        <h3 class="text_log">
          Log
          <h3 class="text_in">In</h3>
        </h3>
        <div class="cant_login">
          <h6 class="text_cant_login">Can't log in?</h6>
          <a href="#" class="a_sign">Sign up for account</a>
        </div>
      </div>
      <div class="form_login">
        <p class="text_email">Email Address</p>

        <q-input
          color="red-10"
          outlined
          v-model="form.cpf_mail"
          label="Enter Email Address"
        />

        <p class="text_pass">Password</p>
        <q-input
          color="red-10"
          outlined
          class="input_pass"
          v-model="form.password"
          type="password"
          label="Enter Password"
        />
      </div>

      <div class="_or">
        <div class="line_1"></div>
        <div class="text_or">Or</div>
        <div class="line_2"></div>
      </div>

      <div class="buttons">
        <div class="q-pa-md q-gutter-sm">
          <q-btn
            icon="google"
            color="white"
            text-color="black"
            style="width: 75%; margin-left: 12.5%"
          >
            <img
              src="../assets/google.png"
              style="width: 20px; margin-right: 3%"
            />
            <div class="ellipsis">Log in with Google</div>
          </q-btn>
        </div>
        <div class="btn_login">
          <q-btn
            @click="onLogIn()"
            unelevated
            rounded
            color="red-10"
            label="Log In"
            style="width: 25%; margin-left: 37.5%; margin-top: 50px"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import axios from "axios";
export default defineComponent({
  name: "IndexPage",

  data() {
    return {
      form: {
        cpf_mail: null,
        password: null,
      },
    };
  },

  methods: {
    onLogIn() {
      axios({
        method: "POST",
        url: "http://localhost:8081/users/login",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
        data: {
          cpf_mail: this.form.cpf_mail,
          password: this.form.password,
        },
      })
        .then((response) => {
          //TODO: Fazer toda a tratativa de redirect, sessão...
        })
        .catch((error) => {
          console.log(error);
        })
        .finally({});
    },
  },
});
</script>
<style>
* {
  padding: 0;
  margin: 0;
}

.screen {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.left_screen {
  width: 50%;
  height: 100vh;
  background-color: #eef1f4;
  float: left;
}

.right_screen {
  width: 50%;
  height: 100vh;
  float: left;
}

/* --------------------- LEFT SCREEN --------------------- */
.ball_1 {
  width: 250px;
  height: 250px;
  border-radius: 125px;
  background-color: #af1b3f;
  position: absolute;
  margin-left: -5%;
  margin-top: -2%;
  opacity: 0.5;
}

.ball_2 {
  width: 250px;
  height: 250px;
  border-radius: 125px;
  background-color: #af1b3f;
  position: absolute;

  margin-top: -5%;
  opacity: 0.5;
}

.img_logo {
  width: 25%;
  height: 30%;
  margin-left: 37.5%;
  margin-top: 20%;
}

.title {
  width: 100%;
  text-align: center;
  color: #af1b3f;
  margin-top: 7%;
}

#title_name {
  font-family: Arial;
  font-weight: bold;
  font-size: 80px;
}

/* --------------------- LEFT SCREEN --------------------- */

/* --------------------- RIGHT SCREEN --------------------- */

.text {
  width: 75%;
  margin-top: 15%;
  margin-left: 12.5%;
}

.text_log {
  float: left;
  font-weight: bold;
  margin-right: 15px;
}
.text_in {
  color: #af1b3f;
  font-weight: bold;
}

.cant_login {
  margin-top: 15px;
}

.text_cant_login {
  color: #af1b3f;
  font-size: 15px;
  margin-left: 5px;
}

.a_sign {
  text-align: right;
  float: right;
  color: #af1b3f;
  font-size: 15px;
  margin-top: -25px;
}

.form_login {
  width: 75%;
  margin-left: 12.5%;
  margin-top: 7%;
}

.input_email {
  margin-top: -20px;
}

.text_pass {
  margin-top: 25px;
}

.input_pass {
  margin-top: -5px;
}

._or {
  width: 75%;
  margin-left: 12.5%;
  display: inline;
  text-align: center;
}
.text_or {
  width: 15%;
  margin-top: 40px;
  margin-left: 0%;
  float: left;
}

.line_1 {
  width: 30%;
  height: 1px;
  background-color: green;
  float: left;
  margin-top: 50px;
  margin-left: 12.5%;
  float: left;
}

.line_2 {
  width: 30%;
  height: 1px;
  background-color: green;
  margin-top: 25px;
  margin-right: 12.5%;
  float: left;
}

.buttons {
  width: 100%;
  margin-top: 75px;
}
.btn_google {
  width: 75%;
}
/* --------------------- RIGHT SCREEN --------------------- */
</style>
