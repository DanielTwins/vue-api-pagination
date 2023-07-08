<template>
  <div>
    <h1>Hello employees</h1>

    <EmployeeList />
  </div>
</template>

<script>
import EmployeeList from "../components/EmployeeList.vue";

export default {
  components: {
    EmployeeList,
  },
};
</script>
