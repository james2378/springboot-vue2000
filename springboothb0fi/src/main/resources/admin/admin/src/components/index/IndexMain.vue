<template>
	<div style="height: 100%;">
		<index-aside v-if="'vertical' == 'vertical'" :style='{"boxShadow":"0px 4px 10px 0px rgba(0,0,0,0.3)","padding":"10px 0 0","overflow":"hidden","top":"60px","left":"0","background":"#fff","bottom":"0","width":"210px","fontSize":"0px","position":"fixed","height":"calc(100% - 60px)","zIndex":"1001"}'></index-aside>
		<el-main :style='"vertical" == "vertical" ? {"minHeight":"100%","width":"100%","padding":"0","margin":"0","position":"relative","display":"block"} : {"minHeight":"100%","margin":"0","position":"relative"}'>
			<index-header :style='{"boxShadow":"0px 4px 10px 0px rgba(0,0,0,0.3020)","padding":"8px 20px","alignItems":"center","background":"#C2CDE4","display":"flex","width":"100%","position":"relative","justifyContent":"center","zIndex":"1002"}'></index-header>
			<index-aside v-if="'vertical' == 'horizontal'" :style='{"width":"100%","borderColor":"#efefef","borderStyle":"solid","background":"#304156","borderWidth":"0 0 1px 0","height":"auto"}'></index-aside>
			<bread-crumbs :title="title" :style='{"padding":"0 20px","margin":"10px auto 10px 240px","borderColor":"#eee","alignItems":"center","borderWidth":"0","background":"#98A3A9","display":"flex","width":"calc(100% - 270px)","borderStyle":"solid","height":"40px"}' class="bread-crumbs"></bread-crumbs>
			<router-view :style='{"padding":"30px 30px 30px 240px","backgroundAttachment":"fixed","background":"url(http://codegen.caihongy.cn/20220805/374e8be049744915a5cf28e9bad51d62.png)","backgroundSize":"cover","backgroundPosition":"center center","backgroundRepeat":"no-repeat","height":"calc(100vh - 120px)"}' class="router-view" style="height:auto;background: transparent;"></router-view>
		</el-main>
	</div>
</template>

<script>
	import IndexAside from '@/components/index/IndexAsideStatic'
	import IndexHeader from '@/components/index/IndexHeader'
	import menu from "@/utils/menu";
	export default {
		components: {
			IndexAside,
			IndexHeader
		},
		data() {
			return {
				menuList: [],
				role: "",
				currentIndex: -2,
				itemMenu: [],
				title: '',
			};
		},
		mounted() {
			let menus = menu.list();
			this.menuList = menus;
			this.role = this.$storage.get("role");
		},
		created() {
			this.init();
		},
		methods: {
			init(){
				this.$nextTick(()=>{
					
				})
			},
			menuHandler(menu) {
				this.$router.push({
					name: menu.tableName
				});
				this.title = menu.menu;
			},
			titleChange(index, menus) {
				this.currentIndex = index
				this.itemMenu = menus;
				console.log(menus);
			},
			homeChange(index) {
				this.itemMenu = [];
				this.title = ""
				this.currentIndex = index
				this.$router.push({
					name: 'home'
				});
			},
			centerChange(index) {
				this.itemMenu = [{
					"buttons": ["新增", "查看", "修改", "删除"],
					"menu": "修改密码",
					"tableName": "updatePassword"
				}, {
					"buttons": ["新增", "查看", "修改", "删除"],
					"menu": "个人信息",
					"tableName": "center"
				}];
				this.title = ""
				this.currentIndex = index
				this.$router.push({
					name: 'home'
				});
				
			}
		}
	};
</script>
<style lang="scss" scoped>
	a {
		text-decoration: none;
		color: #555;
	}

	a:hover {
		background: #00c292;
	}
	
	.el-main {
		padding: 0;
		display: block;
	}

	.nav-list {
		width: 100%;
		margin: 0 auto;
		text-align: left;
		margin-top: 20px;

		.nav-title {
			display: inline-block;
			font-size: 15px;
			color: #333;
			padding: 15px 25px;
			border: none;
		}

		.nav-title.active {
			color: #555;
			cursor: default;
			background-color: #fff;
		}
	}

	.nav-item {
		margin-top: 20px;
		background: #FFFFFF;
		padding: 15px 0;

		.menu {
			padding: 15px 25px;
		}
	}
	
	.detail-form-content {
	    background: transparent;
	}
</style>
