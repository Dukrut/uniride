<template>
  <div class="full-width window-height no-scroll">
    <toolbar-layout />
    <dashboard-layout />
  </div>
</template>

<script>
import axios from "axios";
import ToolbarLayout from "../components/ToolbarLayout.vue";
import DashboardLayout from "../components/DashboardLayout.vue";

export default {
  components: { ToolbarLayout, DashboardLayout },
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
