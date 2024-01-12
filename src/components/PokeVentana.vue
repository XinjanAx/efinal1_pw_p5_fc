<template>
    <div class="pantalla">
    <img :src="imagen" alt="no img" />
    <h2>{{nombre}}</h2>
  </div>
</template>

<script>
export default {
    props: {
        imagen:String,
        nombre:String
    }
}
</script>

<style scoped>
.pantalla {
    width: 33%;
    height: 90%;
    display: flex;
    align-items: center;
    flex-direction: column;
}
img {
  width: 200px;
  height: 250px;
}
</style>