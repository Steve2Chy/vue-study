<!-- 1模板：html结构 -->
<template>
  <div id="home">
		<app_header v-on:msgChange="updateMsg($event)" v-bind:msg="msg"></app_header>
		<users v-bind:users="users"></users>
		<users v-bind:users="users"></users>
		<app_footer v-bind:msg="msg"></app_footer>
  </div>
</template>

<!-- 2行为：处理操作 -->
<script>

import Users from './Users.vue'
import Header from './Header.vue'
import Footer from './Footer.vue'

export default {
  name: 'home',
	data(){ //data:function(){
		return {
			msg:"这是传值：string number boolean",
			users:[]
		}
	},
	methods:{
		updateMsg(msg){
			this.msg = msg;
		}
	},
  components: {
		users : Users,
		app_header: Header,
		app_footer: Footer
  },
	created(){
		this.$http.get("http://jsonplaceholder.typicode.com/users")
		.then((data)=>{
			console.log(data);
			this.users = data.body;
		})
	}
}
</script>

<!-- 3样式：解决样式 -->
<style scoped>
h1{
	color: cadetblue;
}
</style>
