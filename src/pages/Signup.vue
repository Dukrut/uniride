<template>
    <div class="screen">
      <div class="left_screen">
        <div class="ball_1"></div>
        <div class="ball_2"></div>
        <img src="../assets/logo.png" class="img_logo"/>
        <div class="title">
          <h1 id="title_name">UNIRIDE</h1>
        </div>
      </div>
      <div class="right_screen">
          <div class="text">
            <h3 class="text_sign">Sign<h3 class="text_up">Up</h3></h3>
            <div class="already_account">
              <h6 class="text_already_account">Already have an account? <h6 class="text_logIn">Log in</h6></h6>
            </div>
          </div>
          <div class="form_login">
            <p class="text_name">Name</p>
            <q-input color="red-10" outlined v-model="text" label="Your Name" />

            <p class="text_email">Email Address</p>
            <q-input color="red-10" outlined v-model="text" label="examples@gmail.com" />
            
            <p class="text_pass">Password</p>
            <q-input color="red-10" outlined class="input_pass" v-model="password"  type="password" label="Enter Password"/>
          </div>

            <div class="check_box">
                <div class="q-pa-md">
                    <div class="q-gutter-sm">
                        <q-checkbox  v-model="red" label="I agree to Platforms Terms of Service and Privacy Policy" color="red" />
                    </div>
                </div>
            </div>
          <div class="_or">
            <div class="line_1"></div>
            <div class="text_or">Or</div>
            <div class="line_2"></div>
          </div>

          <div class="buttons">
            <div class="q-pa-md q-gutter-sm">
              <q-btn icon="google" color="white" text-color="black" style="width: 75%; margin-left: 12.5%;">

                <img src="../assets/google.png" style="width: 20px; margin-right: 3%"/>
                <div class="ellipsis">
                  Sign with Google
                </div>
              </q-btn>
            </div>
            <div class="btn_login">
              <q-btn unelevated rounded color="red-10" label="Create account" style="width: 25%; margin-left: 37.5%; margin-top: 50px;"/>
            </div>
          </div>

        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'SignUpPage'
})
</script>

<style>
    *{
  padding: 0;
  margin: 0;
}

.screen{
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.left_screen{
  width: 50%;
  height: 100vh;
  background-color: #EEF1F4;
  float: left;
}

.right_screen{
  width: 50%;
  height: 100vh;
  float: left;
  
}


/* --------------------- LEFT SCREEN --------------------- */ 
.ball_1{
  width: 250px;
  height: 250px;
  border-radius: 125px;
  background-color: #AF1B3F;
  position: absolute;
  margin-left: -5%;
  margin-top: -2%;
  opacity: 0.5;
}

.ball_2{
  width: 250px;
  height: 250px;
  border-radius: 125px;
  background-color: #AF1B3F;
  position: absolute;
  
  margin-top: -5%;
  opacity: 0.5;
}

.img_logo{
  width: 25%;
  height: 30%;
  margin-left: 37.5%;
  margin-top: 20%;
}

.title{
  width: 100%;
  text-align: center;
  color: #AF1B3F;
  margin-top: 7%;
}

#title_name{
  font-family: Arial;
  font-weight: bold;
  font-size: 80px;
}

/* --------------------- LEFT SCREEN --------------------- */ 


/* --------------------- RIGHT SCREEN --------------------- */ 

.text{
  width: 75%;
  margin-top: 7%;
  margin-left: 12.5%;

}

.text_sign{
  float: left;
  font-weight: bold;
  margin-right: 15px;
}
.text_up{
  color: #AF1B3F;
  font-weight: bold;
}

.already_account{
  margin-top: 15px;
}

.text_already_account, .text_logIn{
  color: #000;
  font-size: 15px;
  margin-left: 5px;
  float: left;
}

.text_logIn{
    color: #AF1B3F;
}


.a_sign{
  text-align: right;
  float: right;
  color: #AF1B3F;
  font-size: 15px;
  margin-top: -25px;
}

.form_login{
  width: 75%;
  margin-left: 12.5%;
  margin-top: 7%;
}

.input_email{
  margin-top: 20px;
}

.text_pass{
  margin-top: 25px;
}

.text_email{
    margin-top: 20px;
}

.input_pass{
  margin-top: -5px;
}

.check_box{
    text-align: center;
}

._or{
  width: 75%;
  margin-left: 12.5%;
  display: inline;
  text-align: center;
}
.text_or{
  width: 15%;
  margin-top: 40px;
  margin-left: 0%;
  float: left;
}

.line_1{
  width: 30%;
  height: 1px;
  background-color: green;
  float: left;
  margin-top: 50px;
  margin-left: 12.5%;
  float: left;
}

.line_2{
  width: 30%;
  height: 1px;
  background-color: green;
  margin-top: 25px;
  margin-right: 12.5%;
  float: left;
}

.buttons{
  width: 100%;
  margin-top: 75px;
}
.btn_google{
  width: 75%;
  
}
/* --------------------- RIGHT SCREEN --------------------- */ 
</style>
