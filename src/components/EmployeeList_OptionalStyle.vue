<template>
  <div>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.first_name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      users: [],
    };
  },

  mounted() {
    this.fetchData();
  },

  methods: {
    fetchData() {
      axios
        .get("https://reqres.in/api/users")
        .then((response) => {
          this.users = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
