<template>
  <nav>
    <h1>맛있게 먹자</h1>
    <div class="router-link">
      <router-link to="/">상품목록</router-link>
      <router-link to="/cart">장바구니</router-link>
    </div>
    <ul>
      <li v-for="(list,idx) in categories" :key="idx" @click="selectedClick(list)">{{ list}}</li>
    </ul>
  </nav>
</template>

<script setup>
import { useRouter } from 'vue-router';

defineProps({
  categories: Array
});
const router = useRouter();
const emit = defineEmits(['selected']);
const selectedClick = (list) => {
  emit('selected',list);
  router.push('/');
}
</script>

<style lang="scss" scoped>
  nav{
    display: flex;
    justify-content: space-between;
    padding: 2rem 5rem;
    border-bottom: 2px solid orangered;
    // background-color: #fff;
    background-color: rgb(255, 235, 148);

    h1,.router-link{
      color: orangered;
    }
    ul{
      width: 450px;
      display: flex;
      justify-content: space-between;
      // gap: 3rem;
      li{
        cursor: pointer;
        &:hover{
          padding: 5px;
          background-color: rgba(255, 69, 0, 0.8);
          border-radius: 5px;
          color: #fff;
          font-weight: bolder;
        }
      }
    }
  }
</style>