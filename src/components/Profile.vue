<template>
  <div class='profile-container'>
    <div v-for='item in group' :key='item.name' class='avatar'>
      <img :src='item.photo'>
      {{ item.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Profile',
  props: ['group']
}
</script>

<style scoped>
.avatar {
  display: flex;
  flex-direction: column;
}
img {
  width: 100px;
}
</style>
