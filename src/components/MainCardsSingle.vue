<script setup>
  import { ref } from 'vue'
  import { faker } from '@faker-js/faker'

  import useAPI from '@/composables/useAPI'
  const { getDepartment } = useAPI()

  const selectCard = () => {
    console.log(`${props.employee.name} selected`)
  }

  const props = defineProps({
    employee: {
      type: Object,
      required: true,
      default: () => {
        return {
          createdAt: '2022-11-11',
          departmentId: '123',
          email: 'TheBombEmployee@yahoo.com',
          employeeId: '123',
          name: 'TheBomb Employee',
          quote: 'I am a good employee',
          title: 'Some Position',
          updaatedAt: '2022-11-11',
        }
      },
    },
  })

  const departmentResponse = await getDepartment(props.employee.departmentId)
  const department = ref(departmentResponse)
</script>

<template>
  <div class="card" @click="selectCard">
    <div class="card-image">
      <img :src="faker.internet.avatar()" alt="" srcset="" />
    </div>
    <div class="card-details">
      <p class="card-details-name">{{ props.employee.name }}</p>
      <p class="card-details-job">{{ props.employee.title }}, {{ department.name }}</p>
      <p class="card-details-quote">"{{ props.employee.quote }}"</p>
    </div>
  </div>
</template>

<style scoped lang="postcss">
  .card {
    @apply cursor-pointer overflow-hidden rounded-xl bg-slate-100 p-8 shadow-md transition-transform duration-200 hover:scale-110 hover:shadow-2xl hover:shadow-gray-500;
    &-image {
      img {
        @apply mx-auto rounded-full object-contain;
      }
    }
    &-details {
      @apply flex flex-col gap-2 pt-6 text-center;
      &-name {
        @apply text-3xl font-bold text-black;
      }
      &-job {
        @apply -mt-3 text-sm font-semibold text-green-700;
      }
      &-email {
        @apply text-slate-900;
      }
      &-quote {
        @apply pt-2 text-lg italic text-slate-400;
      }
    }
  }
</style>
