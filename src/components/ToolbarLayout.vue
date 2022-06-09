<template>
  <div class="full-width">
    <q-toolbar class="text-danger bg-orange-4">
      <img src="../assets/logo.png" class="img_logo" />

      <q-toolbar-title class="text-red-10">UNIRIDE</q-toolbar-title>

      <q-btn
        :flat="view != 'dashboard'"
        class="text-red-10"
        icon="dashboard"
        @click="changeView('dashboard')"
      >
        <q-tooltip>Dashboard</q-tooltip>
      </q-btn>

      <q-btn
        :flat="view != 'cars'"
        class="text-red-10"
        icon="directions_car"
        @click="changeView('cars')"
      >
        <q-tooltip>Carros</q-tooltip>
      </q-btn>

      <q-btn
        :flat="view != 'ride'"
        class="text-red-10"
        icon="commute"
        @click="changeView('ride')"
      >
        <q-tooltip>Corridas</q-tooltip>
      </q-btn>

      <q-btn
        :flat="view != 'users'"
        class="text-red-10"
        icon="supervisor_account"
        @click="changeView('users')"
      >
        <q-tooltip>Usuários</q-tooltip>
      </q-btn>

      <q-btn
        flat
        class="text-red-10 q-ml-xl"
        icon="account_circle"
        @click="changeView('profile')"
      >
        <q-tooltip>Perfil</q-tooltip>
      </q-btn>

      <q-btn
        flat
        class="text-red-10"
        icon="notifications"
        @click="changeView()"
      >
        <q-tooltip>Notificações</q-tooltip>
      </q-btn>
    </q-toolbar>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    user_id: {
      type: String,
      required: true,
    },
    view: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      user: {},
    };
  },

  mounted() {
    this.getUser();
  },

  methods: {
    getUser() {
      axios({
        method: "GET",
        url: "http://localhost:8081/users?id=" + this.user_id,
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      })
        .then((response) => {
          if (response.data) this.user = response.data;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally({});
    },
    changeView(view) {
      this.$emit("onChangeView", view);
    },
  },
};
</script>

<style scoped>
.img_logo {
  width: 43px;
  height: 43px;
  padding: 5px;
}

.my-chart {
  width: 50px;
  height: 50px;
}
</style>
