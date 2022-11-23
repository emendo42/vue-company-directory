<script setup>
  import useAPI from '@/composables/useAPI'
  import MainCardsSingle from '@/components/MainCardsSingle.vue'
</script>

<template>
  <div class="sub-wrapper">
    <Suspense>
      <MainCardsSingle v-for="employee in employees" :key="employee.emmployeeId" :employee="eployee" />
      <template #fallback>
        <div>Loading . . .</div>
      </template>
    </Suspense>
  </div>
</template>

<style scoped lang="postcss">
  .sub-wrapper {
    @apply grid grid-cols-1  gap-4 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4;
  }
</style>
