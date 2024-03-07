<template>
  <header>
    <div class="logo" @click="goToCustomer">
      <img class="logo-img" src="/logo.png" />
      <div class="logo-content">Tuyết Như</div>
    </div>

    <div class="flex">
      <div class="info-admin1">
          <h3 id="username1">Admin</h3>
          <div class="header__cart-list">
            <h4 class="header__cart-heading">Quản lý</h4>
            <ul class="header__cart-list-item">
              <li class="header__cart-item">
                <a class="header__cart-item-info">Thông tin của bạn</a>
              </li>
    
              <li class="header__cart-item">
                <a class="header__cart-item-info">Đăng xuất</a>
              </li>
            </ul>
          </div>
        </div>
      <!-- <div class="username">
        {{ user.name }}
      </div> -->
      <!-- <div class="logout" @click="logout">
        <i class="fa fa-arrow-right-from-bracket"></i>
      </div> -->
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      user: {
        name: "Admin",
      },
    };
  },

  methods: {
    goToCustomer() {
      this.$router.push({ name: "Customer" });
    },
    logout() {
      // this.$router.push({ name: "Customer" });
    },
  },
};
</script>
