<script setup>
import { ref } from "vue";
import Card from "./Card.vue";
import data from "@/data.json";

const heritageData = ref(data);
const viewToggleClass = ref(
  "grid grid-cols-1 grid-cols-2 md:grid-cols-3 gap-6"
);
const gridView = ref("true");
const min = ref();
const max = ref();
const propertyFilter = ref("");

function viewToggle() {
  gridView.value
    ? (viewToggleClass.value = "flex flex-col gap-3 m-3")
    : (viewToggleClass.value =
        "grid grid-cols-1 grid-cols-2 md:grid-cols-3 gap-6");
  gridView.value = !gridView.value;
}

function priceFilter() {
  if (min.value && !isNaN(min.value) && max.value && !isNaN(max.value)) {
    heritageData.value = data.filter(
      (item) =>
        item.price >= Number(min.value) && item.price <= Number(max.value)
    );
  } else {
    heritageData.value = data; // If price range is invalid or empty, show all data
    min.value = "";
    max.value = "";
  }
}

function filterProperty() {
  if (propertyFilter.value.trim() === "") {
    heritageData.value = data; // Reset to original data if filter is empty
  } else {
    heritageData.value = data.filter((item) =>
      item.key_features.some((feature) =>
        feature.toLowerCase().includes(propertyFilter.value.toLowerCase())
      )
    );
  }
}

function reset() {
  heritageData.value = data;
  min.value = "";
  max.value = "";
  propertyFilter.value = "";
}
</script>

<template>
  <section class="bg-green-100 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-2xl font-bold text-green-500 mb-6 text-center">
        {{ heritageData.length < 1 ? "No Item" : "Heritage Homes" }}
      </h2>
      <div :class="viewToggleClass">
        <Card
          v-for="item in heritageData"
          :key="item.id"
          :item="item"
          :gridView="gridView"
        ></Card>
      </div>
    </div>
  </section>

  <section class="flex justify-around w-full my-10 px-6">
    <section class="flex w-1/3">
      <Button
        class="bg-green-500 text-white w-[100px] h-auto"
        @click="priceFilter"
        >Filter</Button
      >
      <input
        class="border-4 w-1/4"
        type="text"
        v-model="min"
        placeholder="Min Amount"
      />
      <input
        class="border-4 w-1/4"
        type="text"
        v-model="max"
        placeholder="Max Amount"
      />
      <Button class="bg-red-500 text-white w-[100px] h-auto" @click="reset"
        >Reset</Button
      >
    </section>
    <Button
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      @click="viewToggle"
      >{{ gridView ? "List View" : "Grid View" }}</Button
    >
    <section class="flex">
      <Button
        class="bg-green-500 text-white w-[100px] h-auto"
        @click="filterProperty"
        >Filter</Button
      >
      <input
        class="border-4"
        type="text"
        v-model="propertyFilter"
        placeholder="Filter with Features"
      />
      <Button class="bg-red-500 text-white w-[100px] h-auto" @click="reset"
        >Reset</Button
      >
    </section>
  </section>
</template>
