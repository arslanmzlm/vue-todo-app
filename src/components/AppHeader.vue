<template>
  <div class="header">
    <span class="title">TODO</span>
    <button @click="$emit('toggle-theme')" class="theme-toggler">
      <img v-if="theme == 'dark'" src="../assets/images/icon-sun.svg" alt="Sun Icon" />
      <img v-else src="../assets/images/icon-moon.svg" alt="Moon Icon" />
    </button>
  </div>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    theme: String,
  },
};
</script>

<style lang="scss">
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 40px;
}

.title {
  line-height: 1;
  letter-spacing: 15px;
  font-size: 30px;
  font-weight: 700;
}

.theme-toggler {
  margin: 0;
  border: none;
  background-color: transparent;
  padding: 0;
  line-height: 1;
  color: #fff;
}
</style>
