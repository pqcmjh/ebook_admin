<template>
	<Layout style="height: 100%" class="main">
		<Sider hide-trigger collapsible :width="256" :collapsed-width="64" v-model="collapsed" class="left-sider" :style="{overflow: 'hidden'}">
			<sidebar v-show="!collapsed"></sidebar>
			<collapsed-side v-show="collapsed"></collapsed-side>
		</Sider>

		<Layout>
			<Header class="header-con">
				<header-bar :collapsed="collapsed">
					<user :message-unread-count="unreadCount" :user-avator="userAvator"/>
				</header-bar>
			</Header>

			<Content class="main-content-con">
				<Layout class="main-layout-con">
					<Content class="content-wrapper">
						<transition name="fade-transform" mode="out-in">
							<router-view :key="key"/>
						</transition>
						<!--<ABackTop :height="100" :bottom="80" :right="50" container=".content-wrapper"></ABackTop>-->
					</Content>
				</Layout>
			</Content>
		</Layout>

		<!--<section class="app-main">-->
		<!--<transition name="fade-transform" mode="out-in">-->
		<!--<router-view :key="key"/>-->
		<!--</transition>-->
		<!--</section>-->
	</Layout>
</template>

<script>
	import HeaderBar from './components/header-bar/index'
	import User from './components/user/user'
	import sidebar from './components/side-bar/sidebar'
	import collapsedSide from './components/collapsed-side/collapsed-side'
	import Cookies from 'js-cookie'

	export default {
		name: "layout",
		components: {
			HeaderBar,
			User,
			sidebar,
			collapsedSide
		},
		data () {
			console.log(this.$store.state.app.sidebar.opened)
			return {
				collapsed: !this.$store.state.app.sidebar.opened,
			}
		},
		computed: {
			key() {
				return this.$route.fullPath
			},
			opened() {
				return this.$store.state.app.sidebar.opened
			},
			unreadCount () {
				return this.$store.state.user.unreadCount
			},
			userAvator () {
				return this.$store.state.user.avator
			},
		},

		watch: {
			opened(newVal, oldVal){
				this.collapsed = !newVal;
			}
		},

		methods: {

		}
	}
</script>

<style lang="scss">
	.app-main {
		/*50 = navbar  */
		min-height: calc(100vh - 50px);
		width: 100%;
		position: relative;
		overflow: hidden;
		padding: 20px 10px 40px 10px;
	}

	.main{
		.ivu-layout-sider{
			background: #001529;
		}
		.ivu-menu-dark{
			background: #001529;
		}
		.ivu-menu-dark.ivu-menu-vertical .ivu-menu-opened {
			background: #000c17;
		}
		.ivu-menu-dark.ivu-menu-vertical .ivu-menu-opened .ivu-menu-submenu-title {
			background: #001529;
		}
		.ivu-menu-dark.ivu-menu-vertical .ivu-menu-item:hover, .ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu-title:hover{
			background: transparent;
		}
		.logo-con{
			height: 64px;
			padding: 10px;
			img{
				height: 44px;
				width: auto;
				display: block;
				margin: 0 auto;
			}
		}
		.header-con{
			background: #fff;
			padding: 0 20px;
			width: 100%;
		}
		.main-layout-con{
			height: 100%;
			overflow: hidden;
		}
		.main-content-con{
			height: calc(100% - 60px);
			overflow: hidden;
		}
		.tag-nav-wrapper{
			padding: 0;
			height:40px;
			background:#F0F0F0;
		}
		.content-wrapper{
			padding: 18px;
			height: calc(100% - 80px);
			overflow: auto;
		}
		.left-sider{
			.ivu-layout-sider-children{
				overflow-y: scroll;
				margin-right: -18px;
			}
		}
	}
	.ivu-menu-item > i{
		margin-right: 12px !important;
	}
	.ivu-menu-submenu > .ivu-menu > .ivu-menu-item > i {
		margin-right: 8px !important;
	}
	.collased-menu-dropdown{
		width: 100%;
		margin: 0;
		line-height: normal;
		padding: 7px 0 6px 16px;
		clear: both;
		font-size: 12px !important;
		white-space: nowrap;
		list-style: none;
		cursor: pointer;
		transition: background 0.2s ease-in-out;
		&:hover{
			background: rgba(100, 100, 100, 0.1);
		}
		& * {
			color: #515a6e;
		}
		.ivu-menu-item > i{
			margin-right: 12px !important;
		}
		.ivu-menu-submenu > .ivu-menu > .ivu-menu-item > i {
			margin-right: 8px !important;
		}
	}

	.ivu-select-dropdown.ivu-dropdown-transfer{
		max-height: 400px;
	}
</style>