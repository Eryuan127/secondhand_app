<template>
  <view class="page">
    <!-- 弥散背景 -->
    <view class="bg bg-1"></view>
    <view class="bg bg-2"></view>
    <view class="bg bg-3"></view>
    <view class="noise"></view>

    <view class="safe-area">
      <view class="card">
        <!-- 顶部品牌区 -->
        <view class="brand-wrap">
          <view class="logo">
            <view class="logo-dot dot-1"></view>
            <view class="logo-dot dot-2"></view>
            <view class="logo-ring"></view>
          </view>
          <text class="title">SecondHand</text>
          <text class="subtitle">Welcome Back</text>
        </view>

        <!-- 登录表单 -->
        <view class="form-wrap">
          <view class="input-glass">
            <text class="input-label">手机号 / 邮箱</text>
            <input
              v-model="form.account"
              class="input"
              type="text"
              placeholder="请输入手机号或邮箱"
              placeholder-class="placeholder"
            />
          </view>

          <view class="input-glass">
            <text class="input-label">密码</text>
            <input
              v-model="form.password"
              class="input"
              type="password"
              placeholder="请输入密码"
              placeholder-class="placeholder"
            />
          </view>

          <button class="login-btn" @click="handleLogin">
            <text class="login-text">Log in</text>
            <text class="login-arrow">→</text>
          </button>
        </view>

        <!-- 跳转注册 -->
        <view class="signup-wrap">
          <text class="signup-tip">没有账户？</text>
          <view class="signup-link-wrap" @click="goSignup">
            <text class="signup-link">立即注册</text>
          </view>
        </view>

        
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      form: {
        account: '',
        password: ''
      }
    }
  },
  methods: {
    handleLogin() {
      const { account, password } = this.form

      if (!account.trim()) {
        uni.showToast({
          title: '请输入用户名或邮箱',
          icon: 'none'
        })
        return
      }

      if (!password.trim()) {
        uni.showToast({
          title: '请输入密码',
          icon: 'none'
        })
        return
      }

      uni.showToast({
        title: '登录成功（演示）',
        icon: 'success'
      })

      // 这里后续可以接你的登录接口
      // uni.request({
      //   url: '你的登录接口地址',
      //   method: 'POST',
      //   data: this.form,
      //   success: (res) => {}
      // })
	  // ✅ 保存用户名（给首页用）
	    uni.setStorageSync('username', account)
	  
	    // ✅ 提示
	    uni.showToast({
	      title: '登录成功',
	      icon: 'success'
	    })
	  
	    // ✅ 延迟跳转（让toast显示一下）
	    setTimeout(() => {
	      uni.reLaunch({
	        url: '/pages/home/home'
	      })
	    }, 800)
    },

    goSignup() {
      uni.navigateTo({
        url: '/pages/signup/signup'
      })
    }
  }
}
</script>

<style scoped>
.page {
  position: relative;
  min-height: 100vh;
  overflow: hidden;
  background: linear-gradient(180deg, #f7fbef 0%, #eef7d8 40%, #edf6d3 100%);
}

.safe-area {
  min-height: 100vh;
  padding: 88rpx 36rpx 44rpx;
  box-sizing: border-box;
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
}

.bg {
  position: absolute;
  border-radius: 50%;
  filter: blur(70rpx);
  opacity: 0.9;
}

.bg-1 {
  width: 520rpx;
  height: 520rpx;
  background: radial-gradient(circle, rgba(233, 245, 86, 0.72) 0%, rgba(233, 245, 86, 0.1) 70%, transparent 100%);
  top: -80rpx;
  left: -120rpx;
}

.bg-2 {
  width: 460rpx;
  height: 460rpx;
  background: radial-gradient(circle, rgba(166, 224, 113, 0.65) 0%, rgba(166, 224, 113, 0.08) 70%, transparent 100%);
  top: 220rpx;
  right: -100rpx;
}

.bg-3 {
  width: 420rpx;
  height: 420rpx;
  background: radial-gradient(circle, rgba(208, 245, 186, 0.8) 0%, rgba(208, 245, 186, 0.08) 70%, transparent 100%);
  bottom: -80rpx;
  left: 160rpx;
}

.noise {
  position: absolute;
  inset: 0;
  background: linear-gradient(rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.02));
  z-index: 1;
}

.card {
  width: 100%;
  position: relative;
  padding: 52rpx 34rpx 42rpx;
  border-radius: 36rpx;
  background: rgba(255, 255, 255, 0.38);
  border: 1rpx solid rgba(255, 255, 255, 0.56);
  box-shadow: 0 18rpx 60rpx rgba(122, 146, 72, 0.12);
  backdrop-filter: blur(18rpx);
  -webkit-backdrop-filter: blur(18rpx);
}

.brand-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 44rpx;
}

.logo {
  width: 116rpx;
  height: 116rpx;
  position: relative;
  margin-bottom: 20rpx;
}

.logo-ring {
  position: absolute;
  inset: 12rpx;
  border-radius: 50%;
  border: 3rpx solid rgba(66, 92, 33, 0.65);
  background: rgba(255, 255, 255, 0.18);
}

.logo-dot {
  position: absolute;
  border-radius: 50%;
}

.dot-1 {
  width: 26rpx;
  height: 26rpx;
  background: #d8ec57;
  top: 20rpx;
  left: 12rpx;
  box-shadow: 0 0 20rpx rgba(216, 236, 87, 0.85);
}

.dot-2 {
  width: 32rpx;
  height: 32rpx;
  background: #9edb72;
  right: 8rpx;
  bottom: 18rpx;
  box-shadow: 0 0 24rpx rgba(158, 219, 114, 0.9);
}

.title {
  font-size: 46rpx;
  font-weight: 700;
  color: #2e3d1c;
  letter-spacing: 2rpx;
}

.subtitle {
  margin-top: 10rpx;
  font-size: 24rpx;
  color: rgba(46, 61, 28, 0.62);
  letter-spacing: 1rpx;
}

.form-wrap {
  display: flex;
  flex-direction: column;
  gap: 24rpx;
}

.input-glass {
  padding: 20rpx 24rpx;
  border-radius: 24rpx;
  background: rgba(255, 255, 255, 0.34);
  border: 1rpx solid rgba(255, 255, 255, 0.55);
  box-shadow: inset 0 1rpx 0 rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(14rpx);
  -webkit-backdrop-filter: blur(14rpx);
}

.input-label {
  display: block;
  margin-bottom: 12rpx;
  font-size: 22rpx;
  color: rgba(46, 61, 28, 0.72);
}

.input {
  height: 64rpx;
  font-size: 28rpx;
  color: #233114;
}

.placeholder {
  color: rgba(35, 49, 20, 0.34);
}

.login-btn {
  margin-top: 10rpx;
  height: 94rpx;
  border-radius: 999rpx;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(214, 236, 86, 0.95), rgba(146, 210, 109, 0.95));
  box-shadow: 0 14rpx 34rpx rgba(148, 180, 72, 0.28);
  color: #233114;
}

.login-btn::after {
  border: none;
}

.login-text {
  font-size: 30rpx;
  font-weight: 700;
  letter-spacing: 1rpx;
}

.login-arrow {
  margin-left: 10rpx;
  font-size: 30rpx;
  font-weight: 700;
}

.signup-wrap {
  margin-top: 30rpx;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
}

.signup-tip {
  font-size: 22rpx;
  line-height: 1;
  color: rgba(46, 61, 28, 0.56);
}

.signup-link-wrap {
  margin-left: 6rpx;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
}

.signup-link {
  font-size: 22rpx;
  line-height: 1;
  color: #4d7f1d;
  font-weight: 600;
  text-decoration: underline;
  white-space: nowrap;
}

.footer-copy {
  margin-top: 44rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8rpx;
}

.footer-line {
  text-align: center;
}

.footer-line-main {
  font-size: 28rpx;
  font-weight: 700;
  color: rgba(46, 61, 28, 0.60);
  letter-spacing: 3rpx;
}

.footer-line-sub {
  font-size: 18rpx;
  font-weight: 400;
  color: rgba(46, 61, 28, 0.34);
  letter-spacing: 2rpx;
}
</style>