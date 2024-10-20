<template>
  <div class="toaster-box" v-if="itemsCheck.checkedItems.length > 0">
    <h3 class="title">Total Price</h3>
    <ul class="list">
      <li v-for="item in itemsCheck.checkedItems" :key="item.id">
        <h5 class="item-name">{{ item.name }}</h5>
        <div class="details-box">
          <span class="quantity">{{ item.quantity }} * {{ item.price }}</span>
          <span class="total">{{
            calculateTotalQuantity(item.quantity, item.price)
          }}</span>
        </div>
      </li>
    </ul>
    <div class="total-box">
      <h5 class="name">Total:</h5>
      <h6 class="price">{{ itemsCheck.totalPrice }}</h6>
    </div>
  </div>
</template>

<script>
export default {
  props: ["itemsCheck"],
  methods: {
    calculateTotalQuantity(quantity, price) {
      return quantity * price;
    },
  },
};
</script>

<style lang="scss" scoped>
.toaster-box {
  position: fixed;
  top: 40px;
  left: 0;
  padding: 24px;
  background-color: #fff;
  z-index: 9999;
  box-shadow: 0 0 8px #00000030;
  border-end-end-radius: 4px;
  border-start-end-radius: 4px;
  max-width: 200px;
  width: 200px;
  .title {
    font-size: 22px;
    font-weight: 700;
    color: #000;
    margin-bottom: 24px;
  }
  .list {
    list-style: none;
    li {
      padding-bottom: 12px;
      margin-bottom: 12px;
      border-bottom: 1px solid #ddd;
      .item-name {
        font-size: 20px;
        font-weight: 500;
        padding-bottom: 8px;
        color: #303030;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
      .details-box {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 12px;
        .quantity {
          font-size: 16px;
          font-weight: 500;
          color: #0000006e;
        }
        .total {
          font-size: 18px;
          font-weight: 700;
          color: #000000;
        }
      }
    }
  }
  .total-box {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    .name {
      font-size: 18px;
      font-weight: 500;
      color: #00000083;
    }
    .price {
      font-size: 22px;
      font-weight: 700;
      color: #000000;
    }
  }
}
</style>
