<template>
  <div class="menu-item">
    <div class="img-box">
      <img :src="item.image" :alt="item.name" class="item-image" />
      <input
        type="checkbox"
        name="checked"
        @click="item.checked = !item.checked"
        :id="`checked-${item.id}`"
      />
    </div>
    <div class="item-info">
      <h3 class="item-info-name">{{ item.name }}</h3>
      <p class="item-info-description">{{ item.description }}</p>
      <p class="item-info-price">${{ item.price.toFixed(2) }}</p>
      <div class="quantity-selector">
        <label :for="`quantity-${item.id}`">Quantity</label>
        <select v-model="item.quantity" :id="`quantity-${item.id}`">
          <option v-for="n in 10" :key="n" :value="n">{{ n }}</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item"],
};
</script>

<style lang="scss" scoped>
.menu-item {
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
  width: calc(33.333% - 18px);
  display: flex;
  flex-direction: column;
  align-items: center;
  .img-box {
    position: relative;
    width: 100%;
    input {
      position: absolute;
      top: 12px;
      left: 12px;
      cursor: pointer;
      height: 22px;
      width: 22px;
    }
    .item-image {
      max-width: 100%;
      width: 100%;
      height: auto;
      max-height: 200px;
      object-fit: cover;
      border-bottom: 1px solid #eee;
    }
  }

  .item-info {
    padding: 12px;
    .item-info-name {
      font-size: 20px;
      font-weight: 600;
      color: rgb(64, 64, 74);
    }
    .item-info-description {
      font-size: 16px;
      font-weight: 500;
      padding: 10px 0 6px;
      color: rgb(169, 168, 173);
    }
    .item-info-price {
      color: rgb(92, 122, 191);
      font-weight: bold;
    }

    .quantity-selector {
      padding: 24px 0 0;
      label {
        display: block;
        color: rgb(119, 127, 135);
        cursor: pointer;
        font-size: 14px;
        font-weight: 500;
        margin-bottom: 6px;
      }
      select {
        padding: 8px;
        color: rgb(119, 127, 135);
        border-color: rgb(119, 127, 135);
        border-radius: 4px;
        font-size: 17px;
      }
    }
  }
}
@media (max-width: 768px) {
  .menu-item {
    width: calc(50% - 18px);
  }
}

@media (max-width: 480px) {
  .menu-item {
    width: 100%;
  }
}
</style>
