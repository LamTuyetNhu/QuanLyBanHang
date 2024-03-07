<template>
  <div v-if="showLogin" class="modal1 js-modal1">
    <div class="wrapper1 js-wrapper">
      <span class="icon-close" @click="showLogin = false">
        <i class="fa-solid fa-xmark"></i>
      </span>

      <div class="form-box login">
        <h2>Đăng nhập</h2>
        <form action="#" method="get">
          <div class="input-box">
            <span class="icon">
              <i class="fa-solid fa-envelope"></i>
            </span>
            <input
              class="login-sodt"
              type="email"
              name="email"
              required
              v-model="email"
            />
            <label>Email</label>
          </div>
          <div class="input-box">
            <span class="icon">
              <i class="fa-solid fa-lock"></i>
            </span>
            <input
              class="login-pass"
              type="password"
              name="password"
              required
              v-model="password"
            />
            <label>Password</label>
          </div>
          <button type="submit" class="btn-submit-login">Login</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",

      showLogin: false,
    };
  },

  methods: {
    async handleSubmit(e) {
      e.preventDefault();
      try {
        const data = {
          email: this.email,
          password: this.password,
        };
        console.log(data);
        await axios.post("/api/dang_nhap_khach_hang", data).then((res) => {
          console.log(res);
          if (res.status === 200) {
            localStorage.setItem("user", JSON.stringify(res.data.khachhang));
            this.$router.push("/KhachHang");
          }
        });
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
