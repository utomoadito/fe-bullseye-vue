<template>
  <div class="home">
    <div class="col-md-12">
      <div class="col-md-12 col-xs-12 bg-primary" style="padding: 10px 15px;">
        <span class="pull-left" style="font-size: 20px;">Women's top</span>
        <select v-model="model.filter" class="form-control filter">
          <option>Filter by size</option>
          <option>XS</option>
          <option>S</option>
          <option>M</option>
          <option>L</option>
          <option>XL</option>
        </select>
      </div>
      <div class="col-md-12 col-xs-12">
        <div class="row">
          <div v-for="(product, index) in productsFilter" :key="index">
            <div
              :class="productsFilter.length === 3 ? 'col-md-4' : 'col-md-3' "
              style="border: 0.5px solid #ddd;"
            >
              <img :src="require(`../assets/${product.productImage}`)" style="width: 200px;" />
              <div class="row">
                <div class="col-md-12">
                  <div
                    v-if="product.isSale"
                    class="pull-left"
                    style="padding: 10px;margin-bottom: 20px;background:red;color:white;"
                  >Sale</div>
                  <div
                    v-if="product.isExclusive"
                    class="pull-left"
                    style="padding: 10px;margin-bottom: 20px;background:green;color:white;"
                  >Excluessive</div>
                  <div
                    v-if="!product.isSale || !product.isExclusive"
                    class="pull-left"
                    style="padding: 10px;margin-bottom: 40px;"
                  ></div>
                </div>
                <div class="col-md-12">
                  <h6 class="pull-left product-name">
                    <b>{{ product.productName }}</b>
                  </h6>
                  <h5 class="pull-right">
                    <b>{{ product.price }}</b>
                  </h5>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import productsJson from "../../products.json";

export default {
  name: "home",
  data() {
    return {
      products: productsJson,
      model: {
        filter: "Filter by size"
      }
    };
  },
  computed: {
    productsFilter() {
      let products = this.products;
      if (this.model.filter && this.model.filter !== "Filter by size") {
        return products.filter(product => {
          let sizes = product.size.findIndex(size => {
            return size === this.model.filter;
          });
          return sizes !== -1;
        });
      } else {
        return products;
      }
    }
  }
};
</script>

<style>
select.filter {
  width: 15%;
  float: right;
}
.product-name {
  font-size: 1vw;
}
@media screen and (max-width: 768px) {
  select.filter {
    width: 30% !important;
  }
  .product-name {
    font-size: 4vw;
  }
}
</style>
