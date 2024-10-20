<template>
  <div class="menu-header">
    <h2>Menu</h2>
    <div class="filter-container">
      <select
        class="filter-container-select"
        v-model="selectedCategory"
        @change="filterCategory"
      >
        <option value="All">Categories: All</option>
        <option
          v-for="(category, index) in categories"
          :key="index"
          :value="category"
        >
          {{ category }}
        </option>
      </select>
      <div class="input-container">
        <input
          class="filter-container-input"
          type="text"
          id="search"
          v-model.trim="searchTerm"
          placeholder="Search"
          @input="searchText"
        />
        <label for="search"><img src="/search.svg" alt="search" /> </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["categories"],
  data() {
    return {
      searchTerm: "",
      selectedCategory: "All",
    };
  },
  methods: {
    searchText() {
      this.$emit("addText", this.searchTerm);
    },
    filterCategory() {
      this.$emit("selectedCategoryEmit", this.selectedCategory);
    },
  },
};
</script>

<style lang="scss" scoped>
.menu-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 24px;
  @media (max-width: 768px) {
    & {
      flex-direction: column;
    }
  }
  .filter-container {
    display: flex;
    gap: 10px;
    @media (max-width: 480px) {
      & {
        flex-direction: column;
      }
    }
    .input-container {
      display: flex;
      align-items: center;
      padding: 1px;
      border-radius: 4px;
      border: 1px solid rgb(119, 127, 135);
      .filter-container-input {
        border: 0;
        font-size: 16px;
        padding: 10px;
        &:focus {
          outline: 0;
          box-shadow: 0;
        }
      }
      label {
        transform: rotateZ(45deg);
        padding-inline-end: 10px;
        height: 20px;
        img {
          max-width: 100%;
          height: 20px;
        }
      }
    }
    .filter-container-select {
      padding: 10px;
      font-size: 16px;
      max-width: 100%;
      min-width: 180px;
      border-radius: 4px;
      border: 1px solid rgb(119, 127, 135);
      color: rgb(119, 127, 135);
    }
  }
}
</style>
