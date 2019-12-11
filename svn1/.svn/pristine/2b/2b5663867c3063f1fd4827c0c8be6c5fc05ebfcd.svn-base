<template>
	<div class="wrapper">
		<el-tabs v-model="activeName" @tab-click="handleClick">
			<el-tab-pane label="登录" name="first">
				<div class="login-container">
					<!-- ref 表单被引入的名称 rules表单验证规则  model数据对象-->
					<el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on"
					 label-position="left">
						<div class="title-container">
							<h3 class="title">用户登录</h3>
						</div>
						<el-form-item prop="username">
							<span class="svg-container">
								<svg-icon icon-class="user" />
							</span>
							<el-input ref="username" v-model="loginForm.username" placeholder="请输入帐号" name="username" type="text" tabindex="1"
							 auto-complete="on" />
						</el-form-item>
						<el-form-item prop="password">
							<span class="svg-container">
								<svg-icon icon-class="password" />
							</span>
							<el-input :key="passwordType" ref="password" v-model="loginForm.password" :type="passwordType" placeholder="请输入密码"
							 name="password" tabindex="2" auto-complete="on" @keyup.enter.native="handleLogin" />
							<span class="show-pwd" @click="showPwd">
								<svg-icon :icon-class="passwordType === 'password' ? 'eye' : 'eye-open'" />
							</span>
						</el-form-item>
						<div class="tips">
							<a style="float:right;color: #A9A9AB;margin-top:-10px;width: 100px;">忘记密码？</a>
							<el-button :loading="loading" @click.native.prevent="handleLogin" style="margin:5px 150px;display:inline-block;width:100px;text-align:center;font-size:18px;text-decoration:none;outline:0;padding:8px 0;">登录</el-button>
						</div>
					</el-form>
				</div>
			</el-tab-pane>
			<el-tab-pane label="注册" name="second">
				<div class="login-container">
					<!-- ref 表单被引入的名称 rules表单验证规则  model数据对象-->
					<el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on"
					 label-position="left">
						<div class="title-container">
							<h3 class="title">用户注册</h3>
						</div>
						<el-form-item prop="fullName1">
							<span class="svg-container">
								<svg-icon icon-class="user" />
							</span>
							 	<el-cascader v-model="loginForm.fullName1" @change="handleItemChange" :options="options" :props="{checkStrictly: true}" clearable></el-cascader>
						</el-form-item>
						
						<el-form-item prop="mobile">
							<span class="svg-container">
								<svg-icon icon-class="user" />
							</span>
							<el-input rel="mobile" v-model="loginForm.mobile" placeholder="手机号码" name="mobile" type="text" tabindex="3"
							 auto-complete="on" />
						</el-form-item>
						<el-form-item prop="username">
							<span class="svg-container">
								<svg-icon icon-class="user" />
							</span>
							<el-input ref="username" v-model="loginForm.username" placeholder="请输入帐号" name="username" type="text" tabindex="4"
							 auto-complete="on" />
						</el-form-item>
						<el-form-item prop="password">
							<span class="svg-container">
								<svg-icon icon-class="password" />
							</span>
							<el-input :key="passwordType" ref="password" v-model="loginForm.password" :type="passwordType" placeholder="请输入密码"
							 name="password" tabindex="5" auto-complete="on" @keyup.enter.native="handleLogin" />
							<span class="show-pwd" @click="showPwd">
								<svg-icon :icon-class="passwordType === 'password' ? 'eye' : 'eye-open'" />
							</span>
						</el-form-item>
						<div class="tips">
							<a style="float:right;color: #A9A9AB;margin-top:-10px;width: 100px;">忘记密码？</a></br>
							<el-button :loading="loading" @click.native.prevent="registerLogin" style="margin:5px 150px;display:inline-block;width:100px;text-align:center;font-size:18px;text-decoration:none;outline:0;padding:8px 0;">注册</el-button>
						</div>
					</el-form>
				</div>
			</el-tab-pane>
		</el-tabs>
	</div>
</template>

<script>
	import {validUsername} from '@/utils/validate'

	export default {
		name: 'Login',
		data() {
			const validateUsername = (rule, value, callback) => {
				callback()
				// if (!validUsername(value)) {
				// 	callback(new Error('请输入用户名，用户名不能为空！'))
				// } else {
				// 	callback()
				// }
			}
			const validatePassword = (rule, value, callback) => {
				callback()
				// if (value.length < 6) {
				// 	callback(new Error('请输入密码，密码不能为空！'))
				// } else {
				// 	callback()
				// }
			}
			return {
				loginForm: {
					username: '',
					password: '',
					// fullName1:[{fullName:'',},{departmentId:'',}],
					fullName1:[],
					fullName:'',
					mobile:'',
					departmentId:''
				},
				loginRules: {
					username: [{required: true,message: '请输入用户名，用户名不能为空！',trigger: 'blur',validator: validateUsername}],
					password: [{required: true,message: '请输入密码，密码不能为空！',trigger: 'blur',validator: validatePassword}]
				},
				loading: false,
				passwordType: 'password',
				redirect: undefined,
				activeName: 'first',
				options:[{
					value:'qiye',
					label:'广州市粤行信息科技',
					children:[{
						value:1,
						label:'技术部'
					}]
				},{
					value:'qiye1',
					label:'粤行信息科技',
					children:[{
						value:2,
						label:'销售部'
					}]
				}]
			}
		},
		watch: {
			$route: {
				handler: function(route) {
					this.redirect = route.query && route.query.redirect
				},
				immediate: true
			}
		},
		methods: {
			 handleItemChange(val,opt) {
				 console.log(this.loginForm.fullName1,'aaaa')
				 // this.loginForm.departmentId=this.loginForm.fullName1[1]
				 this.loginForm.departmentId=this.loginForm.fullName1[1]
				 this.loginForm.fullName=this.loginForm.fullName1[0]
        },
			
			showPwd() {
				if (this.passwordType === 'password') {
					this.passwordType = ''
				} else {
					this.passwordType = 'password'
				}
				this.$nextTick(() => {
					this.$refs.password.focus()
				})
			},
			//登录
			handleLogin() {
				this.$refs.loginForm.validate(valid => {
					console.log(this.loginForm, '登录信息')
					if (valid) {
						this.loading = true
						this.$store.dispatch('user/login', this.loginForm).then(() => {
							this.$router.push({path: this.redirect || '/'})
							this.loading = false
						}).catch(() => {
							this.loading = false
						})
					} else {
						console.log('error submit!!')
						return false;
					}
				})
			},
			handleClick(tab, event) {
				console.log(tab, event);
			},
			//注册
			registerLogin() {
				this.$refs.loginForm.validate(valid => {
						 let arr = this.$refs.departmentId
					console.log(this.loginForm, '注册信息')
					if (valid) {
						this.loading = true
						this.$store.dispatch('user/addUser1', this.loginForm).then(() => {
							this.$router.push({path: this.redirect || '/'})
							this.loading = false
						}).catch(() => {
							this.loading = false
						})
					} else {
						console.log('error submit!!')
						return false;
					}
				})
			}
		},
	}
</script>

<style lang="scss">
	/* 修复input 背景不协调 和光标变色 */
	/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

	$bg:#F6FBFC;
	$light_gray:#000;
	$cursor: black;

	@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
		.login-container .el-input input {
			color: $cursor;
		}
	}

	/* reset element-ui css */
	.login-container {
		.el-input {
			display: inline-block;
			height: 47px;
			width: 90%;

			input {
				background: transparent;
				border: 0px;
				-webkit-appearance: none;
				border-radius: 0px;
				padding: 12px 5px 12px 15px;
				color: $light_gray;
				height: 47px;
				caret-color: $cursor;

				&:-webkit-autofill {
					box-shadow: 0 0 0px 1000px $bg inset !important;
					-webkit-text-fill-color: $cursor !important;
				}
			}
		}

		.el-form-item {
			border: 1px solid rgba(255, 255, 255, 0.1);
			background: rgba(170, 215, 225, 0.1);
			border-radius: 5px;
			color: #454545;
		}
	}

	.el-tabs__item {
		padding: 0 20px;
		height: 40px;
		-webkit-box-sizing: border-box;
		box-sizing: border-box;
		// line-height: 40px;
		display: inline-block;
		list-style: none;
		font-size: 18px;
		font-weight: 500;
		color: #303133;
		position: relative;
	}

	.el-tabs__nav {
		white-space: nowrap;
		position: relative;
		-webkit-transition: -webkit-transform .3s;
		transition: -webkit-transform .3s;
		transition: transform .3s;
		transition: transform .3s, -webkit-transform .3s;
		transition: transform .3s, -webkit-transform .3s;
		float: left;
		z-index: 2;
		left: 150px;
	}
	.el-form-item__content {
		line-height: 0px;
		position: relative;
		font-size: 14px;
	}
</style>

<style lang="scss" scoped>
	$bg:#ffffff;
	$dark_gray:#889aa4;
	$light_gray:black;

	.login-container {
		min-height: 100%;
		width: 100%;
		background-color: $bg;
		overflow: hidden;

		.login-form {
			position: relative;
			width: 520px;
			max-width: 100%;
			padding: 100px 50px 0;
			margin: 0 auto;
			overflow: hidden;
			border-radius: 10px;
			box-shadow: 0px 1px 10px 2px gainsboro;
		}

		.tips {
			font-size: 14px;
			color: #fff;
			margin-bottom: 10px;

			span {
				&:first-of-type {
					margin-right: 16px;
				}
			}
		}

		.svg-container {
			padding: 6px 5px 6px 15px;
			color: $dark_gray;
			vertical-align: middle;
			width: 30px;
			display: inline-block;
		}

		.title-container {
			position: relative;

			.title {
				font-size: 26px;
				color: $light_gray;
				margin: 0px auto 40px auto;
				text-align: center;
				font-weight: bold;
			}
		}

		.show-pwd {
			position: absolute;
			right: 40px;
			top: 16px;
			font-size: 16px;
			color: $dark_gray;
			cursor: pointer;
			user-select: none;
		}

	}
	.el-cascader {
		display: inline-block;
		position: relative;
		font-size: 14px;
		line-height: 40px;
		width: 90%;
	}
	.el-cascader__label {
		position: absolute;
		left: 0;
		top: 0;
		height: 100%;
		padding: 5px 25px 0px 25px;
		color: #606266;
		width: 100%;
		white-space: nowrap;
		text-overflow: ellipsis;
		overflow: hidden;
		-webkit-box-sizing: border-box;
		box-sizing: border-box;
		cursor: pointer;
		text-align: left;
		font-size: inherit;
	}

	.el-icon-arrow-down {
		font-size: 18px;
	}
	
</style>
