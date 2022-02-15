<template>
<div>
  <div class="max-w-full mx-auto">
    <div class="flex justify-between items-center border-b-2 border-gray-100 py-6 md:justify-start md:space-x-10">
        <highcharts />
      </div>
      <div class="flex justify-between items-center border-b-2 border-gray-100 py-6 md:justify-start md:space-x-10">
        <WeeklyLineage />
      </div>
      <div class="flex justify-between items-center border-b-2 border-gray-100 py-6 md:justify-start md:space-x-10">
        <WeeklyStackedbar />
      </div>
  </div>
</div>
</template>
<script>
import highcharts from '@/components/highcharts.vue'
import StackedBar from '@/components/stackBar.vue'
import WeeklyStackedbar from '@/components/weeklyLineages.vue'
import WeeklyLineage from '@/components/weeklyStackedbar.vue'
export default {
  components: {
    StackedBar, WeeklyStackedbar, WeeklyLineage, highcharts
  },

}
</script>