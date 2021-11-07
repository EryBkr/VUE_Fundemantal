<template>
  <!-- ProductAdd componenti tarafından tetiklenecek fonksiyonu handle edeceğiz -->
  <ProductAdd @add:product="addProduct" />

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
      products: [],
    };
  },
  //component yüklendikten sonra çalışacak
  mounted() {
    this.getProducts();
  },
  methods: {
    //ürünleri apiden çekecek olan fonksiyon
    async getProducts() {
      const result = await fetch("http://localhost:3000/products");
      const data = await result.json();
      this.products = data;
    },
    //ProductList componentinden gelen fonksiyonu temsil ediyor aslında
    async deleteProduct(product) {
      //gelen product ın api tarafından silinme işlemini gerçekleştiriyorum
      await fetch("http://localhost:3000/products/" + product.id, {
        method: "DELETE",
      });

      //listenin güncellenmesi için getProducts i çağıracağım
      this.getProducts();
    },
    //alt komponentin tetikleyeceği fonksiyon
    async updateProduct(product) {
      //PUT işlemi yapacağız
      const result = await fetch("http://localhost:3000/products/"+product.id, {
        method: "PUT",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });

       //Product ı resulttan okuduk
      const updatedProduct = await result.json();

        //array içerisinden  component içerisindeki datamızı güncelliyorum
      this.products = this.products.map(p=>p.id===updatedProduct.id?updatedProduct:product);
    },
    async addProduct(product) {
      //POST işlemi yapacağız
      const result = await fetch("http://localhost:3000/products", {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });

      //Product ı resulttan okuduk
      const newProduct = await result.json();

      //array'in yeni bir instance ı alıp ürünü  ekledik
      this.products = [...this.products, newProduct];
    },
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
