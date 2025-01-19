<script setup lang="ts">
import type { Color } from "~/types/product.js";

const initialWigets = [
  {
    id: 1,
    type: "carbon",
    amount: 50,
    action: "offsets",
    active: true,
    linked: true,
    selectedColor: "beige",
    profileLink: "http://google.com",
  },
  {
    id: 2,
    type: "plastic bottles",
    amount: 200,
    action: "collects",
    active: false,
    linked: false,
    selectedColor: "black",
  },
  {
    id: 3,
    type: "trees",
    amount: 10,
    action: "plants",
    active: false,
    linked: true,
    selectedColor: "white",
  },
  {
    id: 4,
    type: "carbon",
    amount: 75,
    action: "offsets",
    active: false,
    linked: true,
    selectedColor: "black",
  },
  {
    id: 5,
    type: "plastic bottles",
    amount: 500,
    action: "collects",
    active: false,
    linked: false,
    selectedColor: "beige",
  },
  {
    id: 6,
    type: "trees",
    amount: 20,
    action: "plants",
    active: false,
    linked: true,
    selectedColor: "blue",
  },
  {
    id: 7,
    type: "carbon",
    amount: 30,
    action: "offsets",
    active: false,
    linked: false,
    selectedColor: "white",
  },
  {
    id: 8,
    type: "plastic bottles",
    amount: 150,
    action: "collects",
    active: false,
    linked: true,
    selectedColor: "green",
  },
  {
    id: 9,
    type: "trees",
    amount: 5,
    action: "plants",
    active: false,
    linked: false,
    selectedColor: "beige",
  },
];

const widgets = ref({ ...initialWigets });
</script>

<template>
  <div class="flex items-center justify-center p-8">
    <div class="w-full max-w-4xl rounded-lg p-9 shadow-lg bg-neutral-100">
      <h1 class="mb-6 border-b py-4 text-4xl font-bold text-black">
        Per Product Widgets
      </h1>

      <div class="grid gap-10 md:grid-cols-2 lg:grid-cols-3">
        <div
          v-for="widget in widgets"
          :key="widget.id"
          class="flex flex-col gap-4"
        >
          <ProductWidget
            :action="widget.action"
            :amount="widget.amount"
            :type="widget.type"
            :color="widget.selectedColor as Color"
            :profile-link="widget.profileLink"
            :is-linked="widget.linked"
          />
          <ProductWidgetSettings
            @change-color="(color) => (widget.selectedColor = color)"
          />
        </div>
      </div>
    </div>
  </div>
</template>
