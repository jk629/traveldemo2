<template>
  <div id="app">
    <a-button-group>
    <a-button @click="userChange('admin')">admin </a-button>
    <a-button @click="userChange('branch')">branch </a-button>
    <a-button @click="userChange('employee')">employee </a-button>
    </a-button-group>
    <div v-if="usertype == 'admin'"><admin/></div>
    <div v-else-if="usertype == 'branch'"><branch/></div>
    <div v-else-if="usertype == 'employee'"><employee/></div>
  </div>
</template>

<script>
import admin from "./components/admin.vue";
import branch from "./components/branch.vue";
import employee from "./components/employee.vue";
export default {
  name: "App",
  components: {
    admin,
    branch,
    employee
  },
  data() {
    return {
      usertype :"admin"
    }
  },
  methods:{
    userChange : function(val) {
         this.usertype = val;
    }
  }
};
</script>

<style>
body {
  margin: 100px 100px;
}
table {
  border: black 1px solid;
  width: 100%;
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
}
.island {
  border-bottom: black 1px solid;
  margin-bottom: 20px;
}
table input,
select {
  width: 50%;
}
.search {
  display: flex;
  justify-content: space-between;
}
.search input {
  width: 100%;
  margin: 20px 150px;
  padding: 10px 100px;
}
tr > th {
  border: black 1px solid;
}
tr > td {
  border: gray 1px solid;
  padding: 10px;
}
</style>
