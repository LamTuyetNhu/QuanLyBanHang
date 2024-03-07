<template>
  <div class="main">
    <form class="form" id="form-2" submit="handleSubmit">
      <h3 class="heading">Admin</h3>
      <p class="desc">Quản lý bán hoa</p>

      <div class="spacer"></div>

      <div class="form-group">
        <label for="email" class="form-label">Email</label>
        <input
          id="email"
          name="email"
          type="text"
          placeholder="VD: email@domain.com"
          class="form-control"
          v-model="email"
        />
        <span class="form-message"></span>
      </div>

      <div class="form-group">
        <label for="password" class="form-label">Mật khẩu</label>
        <input
          id="password"
          name="password"
          type="password"
          placeholder="Nhập mật khẩu"
          class="form-control"
          v-model="password"
        />
        <span class="form-message"></span>
      </div>

      <button class="form-submit">Đăng nhập</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async handleSubmit(e) {
      e.preventDefault()
      try {
        const data = {
          email: this.email,
          password: this.password

        }
        console.log(data)
        await axios.post("/api/dang_nhap_admin", data).then((res) => {

          console.log(res)
          if (res.status === 200) {
            localStorage.setItem('admin', JSON.stringify(res.data.admin))
            alert("Đăng nhập thành công!")
            this.$router.push('/customer')
          }

        })

      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>