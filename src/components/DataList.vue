<template>
    <div class="data-list-container">
      <ul>
        <li v-for="(item, index) in dataList" :key="index">
          <div>
            <span :style="{ color: item.textColor, background: item.bgColor }">{{ item.value }}</span>
            <button @click="changeColor(index)">Cambiar Color</button>
          </div>
        </li>
      </ul>
      <input v-model="newValue" @input="validateAndAdd" placeholder="Nuevo Valor" />
    </div>
  </template>
  
  <script>
  import { DataItem } from '@/interfaces/DataItemInterface';
  import { dataListData } from '@/data/dataListData';
  
  export default {
    data() {
      return {
        dataList: dataListData,
        newValue: '',
      };
    },
    methods: {
      validateAndAdd() {
        if (this.validateInput()) {
          const newItem = { value: this.newValue, textColor: 'black', bgColor: 'white' };
          if (!this.dataList.some(item => item.value === this.newValue)) {
            this.dataList.push(newItem);
            this.newValue = '';
          } else {
            alert('El valor ya existe en la lista.');
          }
        }
      },
      validateInput() {
        return this.newValue.trim().length > 0;
      },
      changeColor(index) {
        const textColor = prompt('Ingrese color de texto:');
        const bgColor = prompt('Ingrese color de fondo:');
        if (textColor && bgColor) {
          this.$set(this.dataList, index, { ...this.dataList[index], textColor, bgColor });
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .data-list-container {
    margin-top: 20px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 5px 0;
  }
  
  span {
    padding: 5px;
    margin-right: 10px;
    border: 1px solid #ccc;
  }
  
  button {
    cursor: pointer;
  }
  </style>
  