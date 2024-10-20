<template>
  <Home />
</template>
<script>
import Home from "../Pages/Home.vue";
export default {
  components: {
    Home,
  },
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap");
p,
ul,
h1,
h2,
h3,
h4,
h5,
h6 {
  margin: unset;
}
a {
  text-decoration: none;
  &:hover {
    text-decoration: none;
  }
}

ul {
  padding: 0;
  list-style: none;
}

body {
  margin: 0;
  padding: 0;
  font-family: "Inter", sans-serif;
  background-color: rgb(237, 238, 242);
}
</style>
