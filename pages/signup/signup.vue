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
          <text class="subtitle">Minimal • Fresh • Refined</text>
        </view>

        <!-- 表单区 -->
        <view class="form-wrap">
          <view class="input-glass">
            <text class="input-label">用户名</text>
            <input
              v-model="form.username"
              class="input"
              type="text"
              placeholder="请输入用户名"
              placeholder-class="placeholder"
            />
          </view>

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

          <button class="signup-btn" @click="handleSignup">
            <text class="signup-text">Sign up</text>
            <text class="signup-arrow">→</text>
          </button>
        </view>

        <!-- 分隔区 -->
        <view class="divider-wrap">
          <view class="divider-line"></view>
          <text class="divider-text">—————— 其他方式登录 ——————</text>
          <view class="divider-line"></view>
        </view>

       <!-- 第三方登录 -->
       <view class="social-wrap">
         <view class="social-item social-item-1" @click="handleSocialLogin('QQ')">
           <image class="social-icon" src="/static/qq.png" mode="aspectFit"></image>
         </view>
       
         <view class="social-item social-item-2" @click="handleSocialLogin('微信')">
           <image class="social-icon" src="/static/weixin.png" mode="aspectFit"></image>
         </view>
       
         <view class="social-item social-item-3" @click="handleSocialLogin('抖音')">
           <image class="social-icon" src="/static/douyin.png" mode="aspectFit"></image>
         </view>
       </view>

        <view class="login-wrap">
          <text class="login-tip">已有账户？</text>
          <view class="login-link-wrap" @click="goLogin">
            <text class="login-link">直接登录</text>
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
        username: '',
        account: '',
        password: ''
      }
    }
  },
  methods: {
    handleSignup() {
      const { username, account, password } = this.form

      if (!username.trim()) {
        uni.showToast({
          title: '请输入用户名',
          icon: 'none'
        })
        return
      }

      if (!account.trim()) {
        uni.showToast({
          title: '请输入手机号或邮箱',
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
        title: '注册成功（演示）',
        icon: 'success'
      })
    },

    handleSocialLogin(type) {
      uni.showToast({
        title: type + ' 登录开发中',
        icon: 'none'
      })
    },

    goLogin() {
      uni.navigateTo({
        url: '/pages/login/login'
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
  position: relative;
  padding: 48rpx 34rpx 40rpx;
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
  margin-bottom: 42rpx;
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
  font-size: 22rpx;
  color: rgba(46, 61, 28, 0.6);
}

.form-wrap {
  display: flex;
  flex-direction: column;
  gap: 22rpx;
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

.signup-btn {
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

.signup-btn::after {
  border: none;
}

.signup-text {
  font-size: 30rpx;
  font-weight: 700;
  letter-spacing: 1rpx;
}

.signup-arrow {
  margin-left: 10rpx;
  font-size: 30rpx;
  font-weight: 700;
}

.divider-wrap {
  margin: 36rpx 0 24rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.divider-line {
  flex: 1;
  height: 2rpx;
  background: rgba(58, 79, 31, 0.14);
}

.divider-text {
  padding: 0 18rpx;
  font-size: 22rpx;
  color: rgba(46, 61, 28, 0.56);
}

/* 三方登录：强制一行 */
.social-wrap {
  width: 100%;
  margin-top: 6rpx;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
}

.social-item {
  width: 88rpx;
  height: 88rpx;
  border-radius: 24rpx;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.32);
  border: 1rpx solid rgba(255, 255, 255, 0.60);
  box-shadow: 0 8rpx 20rpx rgba(138, 162, 90, 0.10);
  backdrop-filter: blur(12rpx);
  -webkit-backdrop-filter: blur(12rpx);
}

/* 不用 gap，直接手动加右边距 */
.social-item-1,
.social-item-2 {
  margin-right: 22rpx;
}

.social-icon {
  width: 42rpx;
  height: 42rpx;
}

.login-wrap {
  margin-top: 50rpx;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
}

.login-tip {
  font-size: 22rpx;
  line-height: 1;
  color: rgba(46, 61, 28, 0.56);
}

.login-link-wrap {
  margin-left: 6rpx;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
}

.login-link {
  font-size: 22rpx;
  line-height: 1;
  color: #4d7f1d;
  font-weight: 600;
  text-decoration: underline;
  white-space: nowrap;
}

/* 底部英文：一粗一细，更高级 */
.footer-copy {
  margin-top: 45rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rpx;
}

.footer-line {
  text-align: center;
}

.footer-line-main {
  font-size: 23rpx;
  font-weight: 650;
  color: rgba(46, 61, 28, 0.60);
  text-transform: none;
}

.footer-line-sub {
  font-size: 13rpx;
  font-weight: 350;
  color: rgba(46, 61, 28, 0.34);
}
</style>