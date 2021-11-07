<template>
   <div class="alert alert-success">{{msg}}</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    //üst componentimden msg isminde string tipte bir data gelecek ve ben bu datayı burada handle ediyorum
    msg: String
  }
}
</script>

<!-- scope sayesinde bu style sadece bu component te uygulanacak -->
<style scoped>
</style>
