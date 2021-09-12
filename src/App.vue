<template>
<!--  <div>-->
<!--    <maintain-manage msg="Welcome to Your Vue.js App"/>-->
<!--  </div>-->
  <div>
    <!-- <supervision-manage/> -->
    <MaintainManage></MaintainManage>
  </div>
</template>

<script>
import MaintainManage from './components/maintain-manage.vue'
import AttendanceManage from './components/attendance-manage.vue'
import SupervisionManage from './components/supervision-manage'

export default {
  name: 'App',
  components: {
    MaintainManage,
    // AttendanceManage,
    // SupervisionManage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  padding: 0;
  margin: 0;
}
</style>
