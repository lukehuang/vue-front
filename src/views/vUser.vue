<template>
  <form role="userDetail" name="userForm" @submit.prevent="save" novalidate>
    <input type="text" name="userName" v-model="userDetail.userName" placeholder="用户名" required autofocus>
    <input type="email" name="email" v-model="userDetail.email" placeholder="邮箱">
    <button type="submit">保 存</button>
    <button type="button" @click="delete">删除</button>
    <button type="button" @click="goLogin">登录</button>
  </form>
</template>

<script>
import { getUser, saveUser, deleteUser } from '../action/action'

export default {
  vuex: {
    getters: {
      userDetail: ({userDetail}) => userDetail.item
    },
    actions: {
      getUser,
      saveUser,
      deleteUser
    }
  },
  route: {
    data ({ to: { params: { id }}}) {
      this.getUser(id)
    }
  },
  methods: {
    save() {
      this.saveUser(this.userDetail)
    },
    delete() {
      this.deleteUser({'id': this.$route.params.id})
    },
    goLogin() {
      this.$route.router.go('/login')
    }
  }
}
</script>
