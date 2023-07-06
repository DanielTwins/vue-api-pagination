<template>
<!--   <EmployeeListPage_CompositionStyle /> -->
  <!-- <EmployeeList /> -->
  <Home />
</template>

<script>
import EmployeeListPage_CompositionStyle from "./components/EmployeeListPage_CompositionStyle.vue";
import EmployeeList from "./components/EmployeeList.vue";
import Home from "./views/Home.vue";

export default {
  components: {
    EmployeeListPage_CompositionStyle,
    EmployeeList,
    Home,
  },
};
</script>

<style scoped></style>
