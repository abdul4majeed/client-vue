<template>
  <div>
    <div><top-header></top-header></div>
    <div><nuxt /></div>
  </div>
</template>

<script>
import header from '@/components/FrontLayout/header'
export default {
  components: {
    'top-header': header
  }
}
</script>

<style></style>
