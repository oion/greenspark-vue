<script setup lang="ts">
import Spark from "../icons/Spark.vue";
import { Color } from "~/types/product.js";

interface iProps {
  action: string;
  amount: number;
  color: Color;
  isLinked: boolean;
  profileLink?: string;
  type: string;
}

const props = withDefaults(defineProps<iProps>(), {
  action: "",
  amount: 0,
  color: Color.BLACK,
  isLinked: false,
  profileLink: "",
  type: "",
});

const COLOR_CLASSES = {
  [Color.BEIGE]: "bg-beige text-green",
  [Color.BLACK]: "bg-black text-white",
  [Color.BLUE]: "bg-blue text-white",
  [Color.GREEN]: "bg-green text-white",
  [Color.WHITE]: "bg-white text-green",
} as const;

const classes = computed(() => [
  COLOR_CLASSES[props.color],
  {
    "hover:shadow-lg hover:pointer hover:-translate-y-1 transition duration-300":
      props.isLinked,
  },
]);

const attributes = computed(() =>
  props.isLinked && !!props.profileLink
    ? { href: `${props.profileLink}`, target: "_blank" }
    : {}
);
</script>

<template>
  <component
    :is="`a`"
    class="flex items-center gap-4 rounded-md p-4"
    :class="classes"
    v-bind="attributes"
  >
    <Spark />

    <h4 class="flex flex-col flex-wrap gap-0">
      <span class="text-xs">This product {{ props.action }}</span>
      <span class="text-xl font-bold">{{ props.amount }} kgs of carbon</span>
    </h4>
  </component>
</template>
