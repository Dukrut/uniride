<template>
  <div class="full-width">
    <q-toolbar class="text-danger bg-orange-5">
      <img src="../assets/logo.png" class="img_logo" />

      <q-toolbar-title class="text-red-10">UNIRIDE</q-toolbar-title>

      <q-btn
        :flat="view != 'dashboard'"
        label="Dashboard"
        class="text-red-10"
        icon="dashboard"
        @click="view = 'dashboard'"
      />

      <q-btn
        :flat="view != 'cars'"
        label="Carros"
        class="text-red-10"
        icon="directions_car"
        @click="view = 'cars'"
      />

      <q-btn
        :flat="view != 'ride'"
        label="Corridas"
        class="text-red-10"
        icon="commute"
        @click="view = 'ride'"
      />

      <q-btn
        :flat="view != 'users'"
        label="Usuários"
        class="text-red-10"
        icon="supervisor_account"
        @click="view = 'users'"
      />

      <q-btn
        flat
        class="text-red-10"
        icon="account_circle"
        @click="view = 'users'"
      />

      <q-btn
        flat
        class="text-red-10"
        icon="notifications"
        @click="view = 'users'"
      />
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
  },

  data() {
    return {
      user: {},
      view: "dashboard",
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
