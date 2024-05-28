<script setup lang="ts">
import { ref } from 'vue'
import type { RecommendStatus } from '../types'
import { restaurantStatusList } from '../constants'

interface Dish {
  name?: string
  diet?: Diet
  status?: RecommendStatus
}

type Diet =
  | 'vegetarian'
  | 'vegan'
  | 'gluten-free'
  | 'pescatarian'
  | 'lactose-free'
  | 'other'

const dishList = ref<Dish[]>([])
const newDish = ref<Dish>({
  status: 'Want To Try',
})

function addDish() {
  dishList.value.push({
    name: newDish.value.name,
    status: newDish.value.status,
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newDish }}
    </pre>
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" v-model="newDish.name" type="text" />
      </div>
      <div>
        <label for="dish-status">Dish Status</label>
        <select name="dish-status" id="dish-status" v-model="newDish.status">
          <option
            v-for="status in restaurantStatusList"
            :value="status"
            :key="status"
          >
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Dish</button>
    </form>
    <li v-for="restaurant in dishList" :key="restaurant.name">
      {{ restaurant.name }} - {{ restaurant.status }}
    </li>
  </main>
</template>
