<template>
    <div class="menu-container">
      <ul>
        <li v-for="(item, index) in menu" :key="index" v-if="!isPrime(index)">
          <router-link :to="item.path">{{ item.label }}</router-link>
        </li>
      </ul>
      <button @click="reverseMenu">Revertir Menú</button>
    </div>
  </template>
  
  <script>
import { MenuItem } from '@/interfaces/MenuInterface';
import { menuData } from '@/data/menuData';
  
  export default {
    data() {
      return {
        menu: menuData,
      };
    },
    methods: {
      isPrime(num) {
        for (let i = 2; i < num; i++) {
          if (num % i === 0) return false;
        }
        return num !== 1;
      },
      reverseMenu() {
        this.menu.reverse();
      },
    },
  };
  </script>
  
  <style scoped>
  .menu-container {
    margin-top: 20px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 5px 0;
  }
  
  button {
    margin-top: 10px;
  }
  </style>
  