<template>
<div>
  <div class="max-w-full mx-auto">
      <div class="flex justify-between items-center border-b-2 border-gray-100 py-6 md:justify-start md:space-x-10">
        <googlechart />
      </div>
  </div>
</div>
</template>
<script>
import googlechart from '@/components/googlechart.vue'
export default {
  components: {
      googlechart,
  },
}
</script>