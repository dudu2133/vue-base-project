<script setup>
import { ref } from 'vue'
import LoginForm from './components/LoginForm.vue'
import HelloWorld from './components/HelloWorld.vue'

const isLoggedIn = ref(!!localStorage.getItem('token'))

const handleLoginSuccess = () => {
  isLoggedIn.value = true
}

const handleLogout = () => {
  localStorage.removeItem('token')
  localStorage.removeItem('username')
  isLoggedIn.value = false
}
</script>

<template>
  <LoginForm v-if="!isLoggedIn" @login-success="handleLoginSuccess" />
  <div v-else>
    <div class="header">
      <span>欢迎，{{ localStorage.getItem('username') }}</span>
      <button @click="handleLogout" class="logout-btn">退出登录</button>
    </div>
    <HelloWorld />
  </div>
</template>

<style>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background: #f5f5f5;
  border-bottom: 1px solid #e0e0e0;
}

.logout-btn {
  background: #ff4444;
  color: white;
  border: none;
  padding: 8px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s;
}

.logout-btn:hover {
  background: #cc0000;
  transform: translateY(-1px);
}
</style>
