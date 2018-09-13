<template>
	<ul class="list">
		<li class="el-menu-item is-active" v-for="(msg,i) in msgs" :key="i">{{msg.name}}</li>
	</ul>
</template>

<script>
	export default {
		name: 'db-sidebar',
		data() {
			return {
				msgs: [
					{
						id: 1, name: '用户列表'
					},
					{
						id: 2, name: '管理员信息'
					},
				]
			}
		}
	}
</script>

<style>
	.list {
		list-style: none;
		margin: 0;
		padding: 0;
	}

	li {
		padding-left: 20px;
	}
</style>
