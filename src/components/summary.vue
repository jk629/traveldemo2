<template>
  <div>
    <a-button-group>
    <a-button @click="userChange('admin')">admin </a-button>
    <a-button @click="userChange('branch')">branch </a-button>
    </a-button-group>
    <admin v-if="usertype == 'admin'" />
    <branch v-if="usertype == 'branch'" />
  </div>
</template>
<script>
import admin from "./admin"
import branch from "./branch";
export default {
  name: "summary_vue",
  components: {
    admin,
    branch,
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
.island {
  margin-bottom: 10px;
  border-bottom: 1px solid black;
}
</style>