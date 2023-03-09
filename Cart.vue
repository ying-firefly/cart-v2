<template>
  <div class="cart">
    <h1>Cart</h1>
    <div class="cart-product">
      <table>
        <thead class="cart-product-title">
          <tr>
            <th class="td-check"><input type="checkbox" @click="moneyTotal()" :checked="checkAll"> 全选</th>
            <th class="td-product">Name</th>
            <th class="td-price">(Standard)Price(USD)</th>
            <th class="td-qty">Quantity</th>
            <th class="td-total">Sub-total(USD)</th>
            <th class="td-do">操作</th>
          </tr>
        </thead>
        <tbody class="cart-product-body">
          <tr v-for="(item, index) in productList" :key="index">
            <td class="td-check"><input type="checkbox" @click="select(item)" :checked="item.choose"></td>
            <td class="td-product">{{ item.name }}</td>
            <td class="td-price">{{ item.price }}</td>
            <td class="td-qty">
              <span @click="minus(item)">-</span>
              {{ item.qty }}
              <span @click="add(item)">+</span>
            </td>
            <td class="td-total">{{ item.price * item.qty }}</td>
            <td class="td-do" @click="del(item, index)">del</td>
          </tr>
        </tbody>
      </table>
      <p>总价：{{ sum }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      sum: 0,
      checkAll: false,
      productList: [
        { id: 1, name: 'Chicken Wing', category: 'Food', qty: 3, price: 10 },
        { id: 2, name: 'Pizza', category: 'Food', qty: 1, price: 50 },
        { id: 3, name: 'Hamburger', category: 'Food', qty: 1, price: 12 },
        { id: 4, name: 'Coca Cola', category: 'Drink', qty: 2, price: 5 },
        { id: 5, name: 'Orange Juice', category: 'Drink', qty: 1, price: 15 },
        { id: 6, name: 'Potato Chips', category: 'Snack', qty: 1, price: 8 }
      ]
    }
  },
  methods: {
    // 全选
    moneyTotal () {
      this.checkAll = !this.checkAll
      if (this.checkAll) {
        this.sum = 0
        this.productList.forEach(item => {
          item.choose = true
          this.sum += item.price * item.qty
        })
      } else {
        this.productList.forEach(item => {
          item.choose = false
        })
        this.sum = 0
      }
    },
    // 选中
    select (item) {
      item.choose = !item.choose
      if (item.choose) {
        this.sum += item.price * item.qty
      } else {
        this.sum -= item.price * item.qty
      }
    },
    // 数量减少
    minus (item) {
      if (item.qty === 1) {
        alert('数量不能小于1')
      } else {
        item.qty--
      }
    },
    // 数量增加
    add (item) {
      if (item.qty === 1) {
        alert('数量不能小于1')
      } else {
        item.qty++
      }
    },
    // 删除
    del (item, index) {
      if (item.choose) {
        item.choose = false
        this.sum -= item.price * item.count
      }
      this.productList.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.cart-product {
  .td-check {
    width: 100px;
  }
  .td-product, .td-price, .td-qty, .td-total, .td-do {
    width: 150px;
  }
  .cart-product-title {
    height: 40px;
  }
  .cart-product-body tr {
    height: 30px;
  }
  p {
    text-align: right;
    margin-right: 50px;
  }
}
</style>
