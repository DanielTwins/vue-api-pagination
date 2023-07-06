<template>
  <div>
    <h1>Hello employees</h1>

    <EmployeeList :employee="renderedEmployees"/>
  </div>
</template>

<script>
import EmployeeList from '../components/EmployeeList.vue';
import {computed} from 'vue'

export default {
  components: {
    EmployeeList,
  },

}
</script>