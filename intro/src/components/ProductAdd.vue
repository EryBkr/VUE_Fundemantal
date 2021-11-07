<template>
  <div>
      <!-- Ürün ekleme formu -->
    <!-- vue içerisinde submit te bir event tır. submit.prevent ise vue içerisinde kullanılan refresh yapmayan submit türüdür -->
    <form @submit.prevent="handleAdd" id="addForm">
      <div class="form-group">
        <label for="id">Id</label>
        <input v-model="product.id" type="text" class="form-control" id="id" />
      </div>
      <div class="form-group">
        <label for="categoryId">categoryId</label>
        <input
          v-model="product.categoryId"
          type="text"
          class="form-control"
          id="categoryId"
        />
      </div>
      <div class="form-group">
        <label for="productName">productName</label>
        <input
          v-model="product.productName"
          type="text"
          class="form-control"
          id="productName"
        />
      </div>
      <div class="form-group">
        <label for="quantityPerUnit">quantityPerUnit</label>
        <input
          v-model="product.quantityPerUnit"
          type="text"
          class="form-control"
          id="quantityPerUnit"
        />
      </div>
      <div class="form-group">
        <label for="unitPrice">unitPrice</label>
        <input
          v-model="product.unitPrice"
          type="text"
          class="form-control"
          id="unitPrice"
        />
      </div>
      <div class="form-group">
        <label for="unitsInStock">unitsInStock</label>
        <input
          v-model="product.unitsInStock"
          type="text"
          class="form-control"
          id="unitsInStock"
        />
      </div>
      <button type="submit" class="btn btn-primary">Ekle</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "product-add",
  data() {
    return {
      //Boş product objesi oluşturduk form ile dolduracağız
      product: {
        id: "",
        categoryId: "",
        productName: "",
        quantityPerUnit: "",
        unitPrice: "",
        unitsInStock: "",
      },
    };
  },
  methods:{
      //form post işlemiyle product objemizi doldurmuştuk zaten.Onu emit ile App componentine gönderiyoruz
      handleAdd(){
          this.$emit("add:product",this.product);
      }
  }
};
</script>

<!--sadece bu componentte çalışacak stil özellikleri -->
<style scoped>
 #addForm{
   margin:100px;
 }
</style>