<script setup>
import { ref, watch } from "vue";

const iconArray = ref([]);

async function fetchData() {
  const response = await fetch(
    "https://ddragon.leagueoflegends.com/cdn/14.21.1/data/en_US/profileicon.json"
  );
  const data = await response.json();

  iconArray.value = Object.values(data.data);
}

watch(iconArray, (a, b) => {
  console.log(a)
})

fetchData();
</script>

<template>
  <div class='container'>
    <a target="_blank" :href="`https://ddragon.leagueoflegends.com/cdn/14.21.1/img/profileicon/${item.id}.png`" class='iconsImg' v-for="(item, index) in iconArray" :key="index">
      <img :src="`https://ddragon.leagueoflegends.com/cdn/14.21.1/img/profileicon/${item.id}.png`">
      <p>ID: {{ item.id }}</p>
    </a>
  </div>
</template>

<style scoped>
  .container{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap:1rem;
  }

  .iconsImg{
    background-color: #90703b; 
    padding:0.2rem;
    cursor: pointer;
    text-decoration: none;
    color: #BDBDBD;
    transition: all 0.3s ease;
    border-radius: 4px;
  }

  .iconsImg:hover{
    background-color: #c1b696;
    color: #f2f2f2;
    transform: scale(1.1);
    opacity: 1;
  }

  .iconsImg:not(:hover) {
    opacity: 0.9;
  }

  .iconsImg img{
    width: 10rem;
    height: 10rem;
  }

  p{
    background-color: #070203;
    padding: 5px;
    margin: 0;
    border-radius: 4px;

  }
</style>
