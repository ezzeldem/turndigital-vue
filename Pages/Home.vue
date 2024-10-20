<template>
  <div class="menu-page">
    <Header
      @addText="addText"
      @selectedCategoryEmit="selectedCategoryHandler"
      :categories="categories"
    />
    <Accordion
      v-for="category in filteredMenu"
      :key="category.category"
      :category="category"
    >
      <Box v-for="item in category.items" :key="item.id" :item="item" />
    </Accordion>
    <Toaster :itemsCheck="itemsCheck" />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import Header from "../src/components/Header/index.vue";
import Accordion from "../src/components/Accordion/index.vue";
import Box from "../src/components/Box/index.vue";
import Toaster from "../src/components/Toaster/index.vue";

const menuData = ref([
  {
    isOpen: true,
    category: "Appetizers",
    items: [
      {
        id: 1,
        checked: false,
        name: "Crispy Onion Rings",
        description:
          "Deep fried vidalia onion rings served with a tangy dipping sauce",
        price: 6.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 2,
        checked: false,
        name: "Thai Spring Rolls",
        description:
          "Crispy Thai spring rolls filled with vegetables and served with sweet and sour dipping sauce",
        price: 7.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 3,
        checked: false,
        name: "Thai Spring Rolls",
        description:
          "Crispy Thai spring rolls filled with vegetables and served with sweet and sour dipping sauce",
        price: 7.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 4,
        checked: false,
        name: "Mozzarella Sticks",
        description:
          "Crispy fried mozzarella sticks served with marinara sauce",
        price: 6.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 5,
        checked: false,
        name: "Chicken Wings",
        description:
          "Spicy buffalo wings served with blue cheese dipping sauce",
        price: 9.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 6,
        checked: false,
        name: "Stuffed Mushrooms",
        description:
          "Mushrooms stuffed with cheese and garlic, baked to perfection",
        price: 8.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 7,
        checked: false,
        name: "Bruschetta",
        description:
          "Toasted bread topped with diced tomatoes, garlic, and basil",
        price: 5.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 8,
        checked: false,
        name: "Potato Skins",
        description:
          "Crispy potato skins filled with cheese, bacon, and green onions",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 9,
        checked: false,
        name: "Nachos Supreme",
        description:
          "Tortilla chips topped with cheese, jalapenos, sour cream, and guacamole",
        price: 8.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 10,
        checked: false,
        name: "Nachos Supreme",
        description:
          "Tortilla chips topped with cheese, jalapenos, sour cream, and guacamole",
        price: 8.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
    ],
  },
  {
    isOpen: false,
    category: "Soups",
    items: [
      {
        id: 11,
        checked: false,
        name: "Tomato Basil Soup",
        description:
          "Creamy tomato soup with a hint of basil and topped with croutons",
        price: 5.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 12,
        checked: false,
        name: "Chicken Noodle Soup",
        description:
          "Classic chicken noodle soup with carrots, celery, and noodles",
        price: 6.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 13,
        checked: false,
        name: "Minestrone Soup",
        description: "Italian vegetable soup with beans, pasta, and tomatoes",
        price: 6.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 14,
        checked: false,
        name: "French Onion Soup",
        description:
          "Rich beef broth with caramelized onions and melted cheese on top",
        price: 7.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 15,
        checked: false,
        name: "Clam Chowder",
        description:
          "Creamy New England-style clam chowder with potatoes and clams",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 16,
        checked: false,
        name: "Broccoli Cheddar Soup",
        description: "Rich and creamy broccoli soup with cheddar cheese",
        price: 6.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 17,
        checked: false,
        name: "Lentil Soup",
        description: "Hearty lentil soup with carrots, celery, and onions",
        price: 5.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 18,
        checked: false,
        name: "Corn Chowder",
        description: "Creamy corn chowder with potatoes and bacon",
        price: 6.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 19,
        checked: false,
        name: "Pumpkin Soup",
        description: "Seasonal pumpkin soup with a hint of cinnamon and nutmeg",
        price: 5.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 20,
        checked: false,
        name: "Hot and Sour Soup",
        description:
          "Chinese-style soup with tofu, mushrooms, and bamboo shoots",
        price: 6.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
    ],
  },
  {
    isOpen: false,
    category: "Salads",
    items: [
      {
        id: 21,
        checked: false,
        name: "Caesar Salad",
        description:
          "Classic Caesar salad with romaine lettuce, parmesan, croutons, and Caesar dressing",
        price: 8.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 22,
        checked: false,
        name: "Greek Salad",
        description:
          "Fresh salad with cucumbers, tomatoes, olives, and feta cheese",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 23,
        checked: false,
        name: "Cobb Salad",
        description:
          "Salad with chicken, avocado, bacon, eggs, and blue cheese",
        price: 9.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 24,
        checked: false,
        name: "Spinach Salad",
        description: "Fresh spinach with goat cheese, walnuts, and cranberries",
        price: 8.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 25,
        checked: false,
        name: "Quinoa Salad",
        description:
          "Quinoa with black beans, corn, avocado, and lime dressing",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 26,
        checked: false,
        name: "Caprese Salad",
        description: "Sliced tomatoes, mozzarella, and basil with olive oil",
        price: 7.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 27,
        checked: false,
        name: "Kale Salad",
        description: "Fresh kale with lemon vinaigrette, almonds, and parmesan",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 28,
        checked: false,
        name: "Avocado Salad",
        description: "Sliced avocado with mixed greens and citrus vinaigrette",
        price: 8.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 29,
        checked: false,
        name: "Waldorf Salad",
        description: "Fresh apples, walnuts, and grapes in a creamy dressing",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 30,
        checked: false,
        name: "Taco Salad",
        description:
          "Taco-seasoned beef with lettuce, tomatoes, cheese, and sour cream",
        price: 9.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
    ],
  },
  {
    isOpen: false,
    category: "Sandwiches",
    items: [
      {
        id: 31,
        checked: false,
        name: "Grilled Chicken Sandwich",
        description:
          "Grilled chicken breast with lettuce, tomato, and mayo on a toasted bun",
        price: 9.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 32,
        checked: false,
        name: "BLT Sandwich",
        description: "Bacon, lettuce, and tomato with mayo on toasted bread",
        price: 8.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 33,
        checked: false,
        name: "Philly Cheesesteak",
        description:
          "Thinly sliced steak with melted cheese, onions, and peppers on a hoagie roll",
        price: 10.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 34,
        checked: false,
        name: "Tuna Melt",
        description: "Tuna salad with melted cheese on toasted bread",
        price: 7.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 35,
        checked: false,
        name: "Turkey Club",
        description:
          "Triple-decker sandwich with turkey, bacon, lettuce, and tomato",
        price: 9.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 36,
        checked: false,
        name: "Pulled Pork Sandwich",
        description: "Slow-cooked pulled pork with BBQ sauce on a bun",
        price: 8.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 37,
        checked: false,
        name: "Grilled Cheese Sandwich",
        description:
          "Classic grilled cheese sandwich with cheddar cheese on toasted bread",
        price: 6.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 38,
        checked: false,
        name: "Reuben Sandwich",
        description:
          "Corned beef, sauerkraut, Swiss cheese, and Russian dressing on rye bread",
        price: 9.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 39,
        checked: false,
        name: "Meatball Sub",
        description:
          "Italian-style meatballs with marinara sauce and melted cheese on a hoagie roll",
        price: 8.5,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
      {
        id: 40,
        checked: false,
        name: "Egg Salad Sandwich",
        description: "Creamy egg salad with lettuce on whole grain bread",
        price: 7.0,
        image: "https://placehold.co/600x400",
        quantity: 1,
      },
    ],
  },
]);

const selectedCategory = ref("All");
const searchTerm = ref("");

const categories = computed(() =>
  menuData.value.map((category) => category.category)
);

const itemsCheck = computed(() => {
  const checkedItems = menuData.value.reduce((acc, category) => {
    const items = category.items.filter((item) => item.checked);
    return acc.concat(items);
  }, []);

  const totalPrice = checkedItems.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  return { checkedItems, totalPrice };
});

const filteredMenu = computed(() => {
  return menuData.value
    .map((category) => ({
      ...category,
      items: category.items.filter((item) =>
        item.name.toLowerCase().includes(searchTerm.value.toLowerCase())
      ),
    }))
    .filter(
      (category) =>
        selectedCategory.value === "All" ||
        category.category === selectedCategory.value
    );
});

const addText = (text) => {
  searchTerm.value = text;
};

const selectedCategoryHandler = (category) => {
  selectedCategory.value = category;
};
</script>

<style lang="scss" scoped>
.menu-page {
  background-color: rgb(255, 255, 255);
  max-width: 1200px;
  margin: auto;
  padding: 20px;
  box-shadow: 0 0 8px #00000030;
}
</style>
