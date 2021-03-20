<template>
  <div class="detail">
      <p>character {{person}}</p>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Detail',
  props:['person']
}
</script>
<style scoped></style>
