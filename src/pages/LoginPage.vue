<template>
  <div class="col-12 window-height">
    <div class="row full-height">
      <div class="col-6">
        <div class="ball_1"></div>
        <div class="ball_2"></div>
        <img src="../assets/logo.png" class="img_logo" />
        <div class="title">
          <h1 id="title_name">UNIRIDE</h1>
        </div>
      </div>
      <div class="col-6 q-pa-xl d-grid">
        <q-card class="q-pa-lg rounded-borders">
          <q-input
            class="q-ma-md"
            color="orange-10"
            :error="error.login"
            outlined
            rounded
            v-model="form.login"
            @update:modelValue="clearError('login')"
            label="E-mail ou CPF"
          ></q-input>
          <q-input
            class="q-ma-md"
            color="orange-10"
            :error="error.password"
            type="password"
            outlined
            rounded
            v-model="form.password"
            @update:modelValue="clearError('password')"
            label="Senha"
          ></q-input>
          <div class="text-center q-ma-md">
            <q-btn color="negative" rounded @click="onLogIn()">Entrar</q-btn>
          </div>
        </q-card>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import axios from "axios";
import Loading from "quasar";
import { useQuasar } from "quasar";
import { Dark } from "quasar";

const alerts = [
  {
    color: "negative",
    message: "Preencha todos os dados.",
    icon: "report_problem",
  },
];

export default defineComponent({
  name: "IndexPage",

  data() {
    return {
      form: {
        login: null,
        password: null,
      },
      error: {
        login: false,
        password: false,
      },
    };
  },

  setup() {
    const $q = useQuasar();

    return {
      showNotify(type, message) {
        $q.notify({
          type: type,
          position: "top-right",
          message: message,
          timeout: 3000,
        });
      },
      showLoading(message) {
        $q.loading.show({
          message: message,
          spinnerColor: "orange",
          spinnerSize: 140,
          backgroundColor: "green",
          messageColor: "black",
        });

        // hiding in 3s
        let timer = setTimeout(() => {
          $q.loading.hide();
          timer = void 0;
        }, 3000);
      },
    };
  },

  methods: {
    onLogIn() {
      if (this.validateForm()) {
        this.showNotify("negative", "Preencha todos os campos");
        return;
      }

      axios({
        method: "POST",
        url: "http://localhost:8081/users/login",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
        data: {
          login: this.form.login,
          password: this.form.password,
        },
      })
        .then((response) => {
          if (response.data) {
            this.showLoading(
              "Estamos redirecionando você para a página principal."
            );

            let user = response.data;

            setTimeout(() => {
              this.$router.push({
                name: "Home",
                params: {
                  user_id: user["id"],
                },
              });
            }, 1500);

            return;
          }

          this.showNotify(
            "negative",
            "Nenhum usuário foi encontrado com essas credenciais."
          );

          //TODO: Fazer toda a tratativa de redirect, sessão...
        })
        .catch((error) => {
          console.log(error);
        })
        .finally({});
    },

    clearError(key = "") {
      if (key.length) {
        this.error[key] = false;
        return;
      }

      this.error.login = false;
      this.error.password = false;
    },

    validateForm() {
      if ([null, undefined, ""].includes(this.form.login))
        this.error.login = true;

      if ([null, undefined, ""].includes(this.form.password))
        this.error.password = true;

      let has_error = this.error.password || this.error.login;

      return has_error;
    },
  },
});
</script>

<style>
.d-grid {
  display: grid;
  align-items: center;
}

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
</style>
