<template>
  <div class="full-width window-height">
    <toolbar-layout @onChangeView="changeView" :view="view" />
    <dashboard-layout v-if="view == 'dashboard'" />
    <profile-layout
      v-else-if="view == 'profile'"
      :user="user"
      @onGetUser="getUser"
    />
    <user-layout v-else-if="view == 'users'"></user-layout>
  </div>
</template>

<script>
import axios from "axios";
import ToolbarLayout from "../components/ToolbarLayout.vue";
import DashboardLayout from "../components/DashboardLayout.vue";
import ProfileLayout from "../components/ProfileLayout.vue";
import UserLayout from "../components/UserLayout.vue";

export default {
  components: { ToolbarLayout, DashboardLayout, ProfileLayout, UserLayout },
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
        });
    },
    changeView(view) {
      this.view = view;
    },
  },
};
</script>
