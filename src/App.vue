<template>
  <div id="app">
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" v-bind:key="index">
          <td><input type="checkbox" :value="item" v-model="selectedItems" /></td>
          <td>{{ item.Name }}</td>
          <td>{{ item.Price }}</td>
        </tr>
      </tbody>
    </table>
    <label><input type="checkbox" v-model="isAllSelected" @click="changeAllSelected()" /> 全选</label>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator';
import { Goods } from './types/Goods';

@Component({})
export default class App extends Vue {
  items: Goods[] = [
    {
      Name: 'Milk',
      Price: 100,
    },
    {
      Name: 'Cola',
      Price: 110,
    },
    {
      Name: 'Tapioca',
      Price: 120,
    },
  ];
  selectedItems: Goods[] = [];
  isAllSelected = false;

  @Watch('selectedItems')
  changeSelectedItem() {
    this.isAllSelected = this.items.length == this.selectedItems.length;
  }

  changeAllSelected() {
    if (this.isAllSelected) {
      this.selectedItems = [];
    } else {
      this.selectedItems = this.items;
    }
  }
}
</script>
