<template>
  <div class="accordion-box">
    <div class="accordion-box-header" @click="this.isOpen = !this.isOpen">
      <h2 class="accordion-box-header-title">
        {{ category.category }}
      </h2>
      <div class="arrow-box" :class="{ isOpen: isOpen }">
        <img src="/arrow-top.svg" alt="arrow-top" />
      </div>
    </div>
    <div v-if="isOpen" class="menu-items">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: ["category"],
  data() {
    return {
      isOpen: this.category.isOpen,
    };
  },
};
</script>

<style lang="scss">
.accordion-box {
  .accordion-box-header {
    width: 100%;
    cursor: pointer;
    font-weight: bold;
    border-bottom: 1px solid rgb(222, 222, 222);

    padding: 20px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;

    .accordion-box-header-title {
      font-size: 18px;
      font-weight: 700;
      color: rgb(49, 53, 56);
    }
    .arrow-box {
      height: 24px;
      width: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 1px solid rgb(222, 222, 222);
      border-radius: 4px;
      &.isOpen {
        img {
          transform: rotate(0);
        }
      }
      img {
        transform: rotate(180deg);
        height: 16px;
      }
    }
  }

  .menu-items {
    display: flex;
    gap: 24px;
    flex-wrap: wrap;
    padding: 20px 0 0;
  }
}
</style>
