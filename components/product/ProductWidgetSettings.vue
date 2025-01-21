<script setup lang="ts">
import { Color } from "~/types/product.js";

interface iProps {
  isLinked: boolean;
}

const props = defineProps<iProps>();

const colors = [Color.BEIGE, Color.GREEN, Color.BLACK, Color.BLUE, Color.WHITE];

const COLOR_CLASSES = {
  [Color.BEIGE]: "bg-beige",
  [Color.BLACK]: "bg-black",
  [Color.BLUE]: "bg-blue",
  [Color.GREEN]: "bg-green ",
  [Color.WHITE]: "bg-white",
};

const hasLink = ref<Boolean>(props.isLinked);

const activeBadge = ref<Boolean>(false);

const selectedColor = ref<Color | null>(null);

const classColor = (color: Color) => COLOR_CLASSES[color];

const setSelectedColor = (color: Color) => {
  if (activeBadge.value) {
    selectedColor.value = color;
    emit("change-color", color);
  }
};

const emit = defineEmits<{
  "change-color": [value: string];
}>();
</script>

<template>
  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Link to Public Profile</label>
    <input type="checkbox" v-model="hasLink" />
  </div>

  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Activate Badge</label>
    <input
      type="checkbox"
      v-model="activeBadge"
      @input="
        (event: Event) =>
          (activeBadge = (event.target as HTMLInputElement).checked)
      "
    />
  </div>

  <div class="flex justify-between items-center">
    <label class="text-sm text-green">Badge Color</label>

    <p class="flex gap-1">
      <button
        v-for="color in colors"
        @click="setSelectedColor(color)"
        class="h-4 w-4 transition hover:opacity-70"
        :disabled="!activeBadge"
        :class="[
          activeBadge ? classColor(color) : 'bg-gray-400',
          selectedColor === color
            ? 'shadow-[inset_0px_0px_0px_1px_rgba(0,_0,_0,_0.5)]'
            : '',
        ]"
      />
    </p>
  </div>
</template>
