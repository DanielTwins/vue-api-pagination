<template>
  <div class="user-card-container">
    <ProfileCard
      v-for="employee in employees"
      :key="employee.id"
      :employee="employee"
    />
    <div v-if="isLoading">Loading...</div>
    <div v-if="error">{{ error }}</div>
  </div>
</template>

<script>
import ProfileCard from "./ProfileCard.vue";
import useFetch from "../composables/useFetch";
const URL_Page1 = "https://reqres.in/api/users?page";

export default {
  components: {
    ProfileCard,
  },
  setup() {
    const {
      data: employees,
      error,
      isLoading,
    } = useFetch(URL_Page1);

    return { employees, error, isLoading };
  },
};
</script>

<style scoped>
.user-card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}
</style>

<!-- <script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const users = ref([]);

    const fetchData = () => {
      axios
        .get("https://reqres.in/api/users")
        .then((response) => {
          console.log("response => ", response)
          users.value = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    };

    onMounted(fetchData);

    return {
      users,
    };
  },
};
</script>
 -->
