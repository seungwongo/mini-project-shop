<template>
  <main class="mt-3">
    <div class="container">
      <div class="row mb-2">
        <div class="col-12">
          <select class="form-select">
            <option selected></option>
            <option value="1">노트북</option>
            <option value="2">모니터</option>
            <option value="3">마우스/키보드</option>
          </select>
        </div>
      </div>
      <div class="row">
        <div class="col-xl-3 col-lg-4 col-md-6" :key="i" v-for="(product,i) in productList">
          <div class="card" style="width: 18rem;">
            <a @click="goToDetail(product.id);" style="cursor:pointer;"><img :src="`/download/${product.id}/${product.path}`" class="card-img-top" alt="..."></a>
            <div class="card-body">
              <h5 class="card-title">{{product.product_name}}</h5>
              <p class="card-text">
                <span class="badge bg-dark text-white me-1">{{product.category1}}</span>
                <span class="badge bg-dark text-white me-1">{{product.category2}}</span>
                <span class="badge bg-dark text-white">{{product.category3}}</span>
              </p>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group" role="group">
                  <button type="button" class="btn btn-sm btn-outline-secondary">장바구니 담기</button>
                  <button type="button" class="btn btn-sm btn-outline-secondary">주문하기</button>
                </div>
                <small class="text-dark">{{product.product_price}}원</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      productList: []
    };
  },
  created() {
    this.getProductList();
  },
  methods: {
    async getProductList() {
      this.productList = await this.$api("/api/productList",{});
      console.log(this.productList);
    },
    goToDetail(product_id) {
     this.$router.push({path:'/detail', query:{product_id:product_id}}); 
    }
  }
}
</script>