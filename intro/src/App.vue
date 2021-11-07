<template>
  <!-- ProductAdd componenti tarafından tetiklenecek fonksiyonu handle edeceğiz -->
  <ProductAdd @add:product="addProduct"/>

  <!-- elimde ki products arrayıni ProductList componentine props olarak gönderiyorum -->
  <!-- ProductList componentinden gelen aksiyon ile bind işlemi gerçekleştirdik -->
  <ProductList
    @delete:product="deleteProduct"
    @update:product="updateProduct"
    :products="products"
  />
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ProductAdd from "./components/ProductAdd.vue";
export default {
  name: "App",
  components: {
    ProductList,
    ProductAdd,
  },
  //App componentimiz bizim merkezi componentimiz.Componentler arası data taşıma işi ya merkezi bir component ile
  //ya da Vuex ile gerçekleşir.Biz proda merkezi component aracılığıyla data taşıyacağız
  data() {
    return {
      //bu componente ait data lar.Props veya event emitter ile componentler arası taşınabilir
      products: [
        {
          id: 1,
          categoryId: 2,
          productName: "Chai",
          quantityPerUnit: "Good",
          unitPrice: 44,
          unitsInStock: 5,
        },
        {
          id: 2,
          categoryId: 2,
          productName: "Samsung",
          quantityPerUnit: "Good",
          unitPrice: 5000,
          unitsInStock: 50,
        },
        {
          id: 3,
          categoryId: 2,
          productName: "Iphone",
          quantityPerUnit: "Good",
          unitPrice: 6500,
          unitsInStock: 35,
        },
        {
          id: 4,
          categoryId: 2,
          productName: "MSI Notebook",
          quantityPerUnit: "Good",
          unitPrice: 6000,
          unitsInStock: 8,
        },
        {
          id: 5,
          categoryId: 2,
          productName: "Bosh",
          quantityPerUnit: "Good",
          unitPrice: 2300,
          unitsInStock: 19,
        },
      ],
    };
  },
  methods: {
    //ProductList componentinden gelen fonksiyonu temsil ediyor aslında
    deleteProduct(product) {
      //Gelen product ın id değerine eşit olmayan productları product dizimize tanıttık
      this.products = this.products.filter(
        (productToFilter) => productToFilter.id !== product.id
      );
    },
    //alt komponentin tetikleyeceği fonksiyon
    updateProduct(product) {
      alert(`Güncellenecek ürünün adı: ${product.productName}`);
    },
    addProduct(product){
      //Product ı new ledik
      const newProduct={...product};
      //array'in yeni bir instance ı alıp ürünü  ekledik
      this.products=[...this.products,newProduct];
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
