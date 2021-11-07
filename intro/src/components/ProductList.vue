<template>
  <div>
    <!-- ürün adedi 0 ise uyarı gösteriyoruz -->
    <p v-if="products.length == 0">Ürün Listesi Boş</p>

    <!-- Üstteki if geçerli değil ise v-else sayesinde gösterilecek -->
    <table v-else class="table">
      <thead>
        <tr>
          <th>Id</th>
          <th>Ürün adı</th>
          <th>Kategori</th>
          <th>Açıklama</th>
          <th>Birim Fiyatı</th>
          <th>Stok Adedi</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <!-- products array i içerisinde for ile dönüyorum -->
        <tr v-for="product in products" :key="product.id">
          <!-- updateId , product id e eşitse input a çevirecek -->
          <td v-if="updateId === product.id">
            <input
              v-model="product.id"
              type="text"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.id }}</td>

          <td v-if="updateId === product.id">
            <input
              v-model="product.productName"
              type="text"
              class="form-control"
              id="productName"
            />
          </td>
          <td v-else>{{ product.productName }}</td>

          <td v-if="updateId === product.id">
            <input
              v-model="product.categoryId"
              type="text"
              class="form-control"
              id="categoryId"
            />
          </td>
          <td v-else>{{ product.categoryId }}</td>

          <td v-if="updateId === product.id">
            <input
              v-model="product.quantityPerUnit"
              type="text"
              class="form-control"
              id="quantityPerUnit"
            />
          </td>
          <td v-else>{{ product.quantityPerUnit }}</td>

          <td v-if="updateId === product.id">
            <input
              v-model="product.unitPrice"
              type="text"
              class="form-control"
              id="unitPrice"
            />
          </td>
          <td v-else>{{ product.unitPrice }}</td>

          <td v-if="updateId === product.id">
            <input
              v-model="product.unitsInStock"
              type="text"
              class="form-control"
              id="unitsInStock"
            />
          </td>
          <td v-else>{{ product.unitsInStock }}</td>
          <!-- click eventine fonksiyon bind ettik  -->
          <!-- O an satırda güncelleme işlemi yok ise if ile çıkacak butonları kontrol ediyoruz -->
          <td v-if="updateId !== product.id">
            <button
              class="btn btn-sm btn-primary"
              @click="handleUpdate(product)"
            >
              Güncelle
            </button>
            <button
              class="btn btn-sm btn-danger"
              @click="handleDelete(product)"
            >
              Sil
            </button>
          </td>
          <!-- o satırda güncelleme işlemi var ise farklı butonlar gözükecek -->
          <td v-else>
            <button
              class="btn btn-sm btn-primary"
              @click="handleSave(product)"
            >
              Kaydet
            </button>
            <!-- updateId i null yaparsam listede ilk halini alacaktır -->
            <button
              class="btn btn-sm btn-danger"
              @click="updateId=null"
            >
              İptal
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  //Componentimizin ismi
  name: "product-list",
  //component datalarını obje şeklinde return eden vue ye özdü yapı
  data() {
    return {
      //güncellecek datanın id si ile listeyi karşılaştırarak liste elemenlarının
      //input olup olmamasına karar verebilmek için eklediğimiz değişken
      updateId: null,
    };
  },
  //bütün props dataları burada handle edilir,products array bizlere App.vue componentinden geldi
  props: {
    products: Array,
  },
  methods: {
    //butona click edildiğinde fonksiyon tetiklenecek
    handleDelete(product) {
      //event emitter alt komponentten üst komponente data göndermek için kullanılır
      this.$emit("delete:product", product);
    },
    //Güncelleme butonuna tıklanınca tetiklenecek fonksiyon
    handleUpdate(product) {
      //butona her bastığımızda satırdaki product ın id değerini alıp değişkenimize set ediyoruz
      this.updateId = product.id;
    },
    //Yapılan güncellemeleri uygulayacak fonksiyon
    handleSave(product){
      //üst komponente güncellenmiş product objemizi göndererek dizi içerisinde değişiklik yapacağız 
      this.$emit("update:product",product);
      //güncelleme işleminden sonra seçili satırın değişmesi için yaptık
      this.updateId=null;
    }
  },
};
</script>


<style scoped>

</style>