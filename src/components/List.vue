<template>
  <div class="wrap">
    <div class="product-list">
      <div class="card" v-for="list in products" :key="list.id">
        <img :src="list.image" :alt="list.name">
        <p>{{ list.name }}</p>
        <p>가격: {{ list.price }}</p>
        <button @click="addToList(list)">장바구니 추가</button>
      </div>
    </div>
</div>
</template>

<script setup>
defineProps({
  products: Array,
  // addToCart: Function
});

const emit = defineEmits(['add-to-cart']);

const addToList = (list) => {
  emit('add-to-cart', list);
}
</script>

<style lang="scss" scoped>
  .wrap{
    // background-color: #fff;
    // background-color: rgb(255, 235, 148);
    padding: 50px 0;
    width: 80%;
    margin: 0 auto;
  }
  .product-list{
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    justify-content: center;
    .card{
      width: 200px;
      text-align: center;
      border: 1px solid orangered;
      border-radius: 20px;
      padding: 20px;
      img{
        width: 100%;
        height: 200px;
        object-fit: cover;
        border-radius: 5px;
      }
      p{
        margin: 10px 0;
      }
      button{
        margin-top: 10px;
      }
    }
  }
</style>