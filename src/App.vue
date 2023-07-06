<template>
<!--   <EmployeeListPage_CompositionStyle /> -->
  <EmployeeList />
</template>

<script>
import EmployeeListPage_CompositionStyle from "./components/EmployeeListPage_CompositionStyle.vue";
import EmployeeList from "./components/EmployeeList.vue";

export default {
  components: {
    EmployeeListPage_CompositionStyle,
    EmployeeList
  },
};
</script>

<style scoped></style>
