<template>
  <div class="user-card-container">
    <ProfileCard
      v-for="employee in displayedEmployees"
      :key="employee.id"
      :employee="employee"
    />
    <div v-if="isLoading">Loading...</div>
    <div v-if="error">{{ error }}</div>
  </div>
  <div class="pagination-nav">
    <button @click="previousPage" :disabled="currentPage === 1">
      Previous
    </button>
    <div class="current-page">
      <span>{{ currentPage }}</span>
    </div>
    <button @click="nextPage">Next</button>
  </div>
</template>

<script>
import { ref, onMounted, computed } from "vue";
import useFetch from "../composables/useFetch";

import ProfileCard from "./ProfileCard.vue";

const URL_Page1 = "https://reqres.in/api/users?page";
const URL_Page2 = "https://reqres.in/api/users?page=2";

export default {
  components: {
    ProfileCard,
  },
  setup() {
    // pagination, starts with page 1
    const currentPage = ref(1);
    const employeesPerPage = 6;

    // fetch data for page1
    const {
      data: employeesPage1,
      error: errorPage1,
      isLoading: isLoadingPage1,
      fetchData: fetchDataPage1,
    } = useFetch(URL_Page1);

    // fetch data for page2
    const {
      data: employeesPage2,
      error: errorPage2,
      isLoading: isLoadingPage2,
      fetchData: fetchDataPage2,
    } = useFetch(URL_Page2);

    // combine users/employees from both pages
    const employees = computed(() => [
      ...employeesPage1.value,
      ...employeesPage2.value,
    ]);

    // delay this console.log to first fetch (asynchronously) data through useFetch composable 
    // otherwise you get an empty arr
    setTimeout(() => {
      console.log("all employees => ", employees.value);
    }, 2000);

    // calculate the total number of pages based on the number of employees
    const totalPages = computed(
      () => Math.ceil(employees.value.length / employeesPerPage) // 12 / 6 = 2
      // Math.ceil to round up the result to the nearest whole number in case it is a decimal
    );

    // compute the currently displayed employees based on the current page
    const displayedEmployees = computed(() => {
      const startIndex = (currentPage.value - 1) * employeesPerPage; // (1 - 1) * 6 = 0
      const endIndex = startIndex + employeesPerPage; // 0 + 6 = 6 
      return employees.value.slice(startIndex, endIndex); // extract the start and end of array(0, 6)
    });

    const previousPage = () => {
      if (currentPage.value > 1) {
        currentPage.value--;
      }
    };
    const nextPage = () => {
      if (currentPage.value < totalPages.value) {
        currentPage.value++;
      }
    };

    // ensure the fetchData is called on component mount
    onMounted(() => {
      fetchDataPage1();
      fetchDataPage2();
    });

    return {
      currentPage,
      employees,
      displayedEmployees,
      totalPages,
      error: errorPage1.value || errorPage2.value,
      isLoading: isLoadingPage1.value || isLoadingPage2.value,
      previousPage,
      nextPage,
    };
  },
};
</script>

<style scoped>
.user-card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.pagination-nav {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin: 2rem auto;
}

.current-page span{
  background-color: rgb(201, 198, 198);
  border-radius: 3px;
  padding: 0 2px;
}
</style>
