<script>
import ContactService from "@/services/contact.service";
export default {
  // emits: ["delete:khachhang"],
  props: {
    Product: { type: Array, default: [] },
  },
  methods: {
    
    formatCurrency(amount) {
      // Sử dụng Intl.NumberFormat để định dạng số với dấu phẩy
      
      return new Intl.NumberFormat("vi-VN").format(amount);
    },
    async retrieveContacts() {
      try {
        this.Product = await ContactService.getAllSP();
      } catch (error) {
        console.log(error);
      }
    },
    refreshList() {
      this.retrieveContacts();
      this.activeIndex = -1;
    },
    async deleteProduct(customerId) {
      if (confirm("Bạn muốn xóa sản phẩm này?")) {
        try {
          await ContactService.deleteSP(customerId);
          this.refreshList();
          // this.$router.go(0);
        } catch (error) {
          console.log(error);
        }
      }
      await this.retrieveContacts();
      // Làm mới trang
      this.$router.go(0);
    },
  },
};
</script>


<template>
  <div class="container-fluid container1">
    <div class="allcustomer">
      <table class="table table-striped table-allcustomer">
        <thead>
          <tr>
            <th>STT</th>
            <th>Ảnh</th>
            <th>Tên sản phẩm</th>
            <th>Giá</th>
            <th>Số lượng</th>
            <!-- <th>Mô tả</th>
            <th>Ghi chú</th> -->
          </tr>
        </thead>
        <tbody id="myTable">
          <tr v-for="(product, index) in Product">
            <td class="allcus-title table-number">{{ index + 1 }}</td>
            <td class="allcus-title"><img class="img_product" :src="'http://localhost:3000/images/' + product.ten_anh" /></td>
            <td class="allcus-title">{{ product.TenHH }}</td>
            <td class="allcus-title">{{ formatCurrency(product.Gia) }}</td>
            <td class="allcus-title">{{ product.SoLuongHang }}</td>
            <!-- <td class="allcus-title">{{ product.MoTaHH }}</td>
            <td class="allcus-title">{{ product.GhiChu }}</td> -->
            <td class="allcus-title">
              <div class="allcus-form">
                <router-link
                  :to="{
                    name: 'product.updateProduct',
                    params: { id: product._id },
                  }"
                >
                  <button class="allcus-button" type="submit"><i class="fa-regular fa-pen-to-square"></i></button>
                </router-link>

                <button
                  class="allcus-button"
                  data-toggle="modal"
                  data-target="#myModal1"
                  type="submit"
                  v-if="product._id"
                  @click="deleteProduct(product._id)"
                >
                <i class="fa-solid fa-trash"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

