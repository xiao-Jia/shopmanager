<template>
  <div class="login-wrap">
    <el-form class="login-from" label-position="top" label-width="80px" :model="formdata">
      <h2>用户登录</h2>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formdata.password"></el-input>
      </el-form-item>
      <el-button
      @click.prevent='handleLogin'
      class="login-btn" type="success">登陆</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      formdata: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async handleLogin () {
      const res = await this.$http.post(`login`, this.formdata)
      if (res.data.data === null) {
        this.$message.error(res.data.meta.msg)
      }
      const {data: {data: {token}, meta: {msg, status}}} = res
      // console.log(res)
      if (status === 200) {
        localStorage.setItem('token', token)
        this.$router.push({
          name: 'home'
        })
      } else {
        this.$message.error(msg)
      }
      // this.$http.post(`login`, this.formdata).then(res => {
      //   console.log(res)
      //   const{data:{data,meta:{msg,status}}}= res
      //   if (status === 200){
      //     this.$router.push({
      //       name:'home',
      //     })
      //   } else {
      //     this.$message.error(msg);
      //   }
      // })
      // .catch(err=>{
      //   console.log(err)
      // })
    }
  }
}
</script>

<style>
.login-wrap {
  background: #324152;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-from {
    background: #fff;
    width: 400px;
    border-radius: 5px;
    padding: 30px;
}
.login-btn{
    width: 100%;
}
</style>
