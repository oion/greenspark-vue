<script setup lang="ts">
import { Color } from "~/types/product.js";

const colors = [Color.BEIGE, Color.GREEN, Color.BLACK, Color.BLUE, Color.WHITE];

const COLOR_CLASSES = {
  [Color.BEIGE]: "bg-beige",
  [Color.BLACK]: "bg-black",
  [Color.BLUE]: "bg-blue",
  [Color.GREEN]: "bg-green ",
  [Color.WHITE]: "bg-white",
};

const classColor = (color: Color) => COLOR_CLASSES[color];

const emit = defineEmits<{
  "change-color": [value: string];
}>();
</script>

<template>
  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Link to Public Profile</label>
    <input type="checkbox" checked />
  </div>

  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Activate Badge</label>
    <input type="checkbox" />
  </div>

  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Badge Color</label>

    <p class="flex gap-1">
      <button
        v-for="color in colors"
        @click="emit('change-color', color)"
        class="h-4 w-4"
        :class="classColor(color)"
      />
    </p>
  </div>
</template>
