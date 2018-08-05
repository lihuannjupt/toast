<template>
  <div id="app">
    <button class="button" @click="showDialog "  >点我</button>
     <Toast v-model='isToastShow'  :time="time" :msg="message" :type="type" @function1="closeToast"></Toast>
  </div>
</template>

<script>
import Toast from '../Index.vue'
export default {
  name: "App",
  data() {
    return {
      // alert数据
      isToastShow: false,
      message: '正在加载中',
      type: 'load',
      time:'5000'
    }
  },   
  methods: { 
    closeToast() {
      console.log("我藏起来喽");
    },
    showDialog() {
     this.isToastShow=true;
    },
  },
  components: {
    Toast
  }
}

</script>

<style lang="scss" scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #fff;
}
* {
  margin: 0px;
  padding: 0px;
  /* background-color: #f1f2f6 */
}
.button {
  background-color: #ff4433;
  width: 80px;
  height: 40px;
  margin: 50px;
}

</style>