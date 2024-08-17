<script setup>
import { ref } from 'vue'

// 暫存
const tempEdit = ref({
  id: '',
  name: '',
  describe: '',
  price: ''
})

// 列表陣列
const arrList = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    describe: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    isEditor: false
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    describe: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18,
    isEditor: false
  },
  {
    id: 3,
    name: '翡翠檸檬',
    describe: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34,
    isEditor: false
  },
  {
    id: 4,
    name: '四季春茶',
    describe: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
    isEditor: false
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    describe: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
    isEditor: false
  }
])

// 庫存 +
const addStock = (item) => {
  item.stock++
}

// 庫存 -
const minusStock = (item) => {
  if (item.stock > 0) {
    item.stock--
  } else {
    alert('庫存不可小於0!')
  }
}

// 編輯拷貝
const editName = (item) => {
  tempEdit.value = { ...item }
}

// 修改
const confirmEdit = () => {
  const index = arrList.value.findIndex((item) => item.id === tempEdit.value.id)
  arrList.value[index] = tempEdit.value
  tempEdit.value = {}
}
</script>

<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in arrList" :key="item.id">
          <td class="name">
            {{ item.name }}
          </td>
          <td>
            <small>{{ item.describe }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button type="button" @click="minusStock(item)">-</button>
            {{ item.stock }}
            <button type="button" @click="addStock(item)">+</button>
          </td>
          <td>
            <button type="button" @click="editName(item)">編輯</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="edit-txt" v-if="tempEdit.id">
      <div class="edit-ti">編輯區</div>
      品名：<input type="text" v-model="tempEdit.name" /><br />
      描述：<input type="text" v-model="tempEdit.describe" /><br />
      價格：<input type="text" v-model="tempEdit.price" /><br />
      <button type="button" @click="confirmEdit(item)">修改</button>
      <button type="button" @click="tempEdit = {}">取消</button>
    </div>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}
#app {
  display: block;
}
.table {
  margin: 0 auto;
  width: 900px;
  text-align: center;
  table-layout: fixed;
  border-collapse: collapse;
}
.table thead th {
  padding: 12px 10px;
  border-bottom: #ccc solid 3px;
  background-color: #f5f5f5;
}
.table tbody td {
  padding: 8px 10px;
  border-bottom: #ddd solid 1px;
}

.edit-txt {
  margin-top: 30px;
  line-height: 1;
}
.edit-txt .edit-ti {
  margin-bottom: 10px;
  padding-bottom: 10px;
  font-size: 18px;
  color: #000;
  font-weight: bold;
  border-bottom: #333 solid 1px;
}
.edit-txt input {
  display: block;
  margin: 5px 0;
}

@media (min-width: 1024px) {
  body {
    padding-top: max(3.5vw, 50px);
    place-items: unset;
  }
}
</style>
