<template>
  <div>
    <q-toolbar class="text-primary">
      <q-btn flat round dense icon="assignment_ind">
        <q-tooltip> Minhas informações </q-tooltip>
      </q-btn>
      <q-toolbar-title> Toolbar </q-toolbar-title>
      <q-btn flat label="Relatórios" />
      <q-btn flat label="Caronas" />
      <q-btn flat label="Usuários" />
      <q-btn flat label="Avaliações" />
    </q-toolbar>

    HEADER
    {{ user_id }}
    {{ user }}
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

<style></style>
