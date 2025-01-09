<script setup>
defineProps({
  item: Object,
  gridView: {
    type: Boolean,
    default: true,
  },
});
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div :class="gridView ? 'p-4' : ' p-4 flex'">
      <img
        :src="item.image"
        alt="image"
        :class="gridView ? 'w-full h-[200px]' : 'w-1/2 h-auto md:mr-12 mr-3'"
      />
      <div>
        <div class="md:mb-6 mb-3">
          <h3 class="text-xl font-bold mt-3">{{ item.name }}</h3>
        </div>

        <div class="mb-5">
          <span class="font-bold">Location: </span>{{ item.location }}
        </div>

        <h3 class="text-green-500 mb-2">
          <span class="font-bold">Price: </span>€{{ item.price }}
        </h3>

        <h3 class="text-md font-bold mt-3">Key Features</h3>
        <ul>
          <li v-for="items in item.key_features">- {{ items }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>
