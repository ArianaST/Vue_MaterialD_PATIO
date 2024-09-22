<script setup>
import CountTo from "vue-count-to/src";

defineProps({
  count: {
    type: Number,
    required: true,
  },
  suffix: {
    type: String,
    default: "",
  },
  duration: {
    type: Number,
    default: 4000,
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  color: {
    validator(value) {
      return [
        "primary",
        "secondary",
        "info",
        "success",
        "warning",
        "error",
        "light",
        "dark",
      ].includes(value);
    },
  },
  divider: {
    validator(value) {
      return ["vertical"].includes(value);
    },
  },
});
</script>
<template>
    <div class="p-0">
    <h5 class="mb-0">{{ title }}</h5>
    <p class="mb-2 text-right font-weight-normal ">
      {{ description }}
    </p>

  <hr :class="`${divider ? divider : ''} `" />
  <div class="text-right">
    <div :style="{ color: color }">
    <h1 :class="` text-${color ?? 'white'}`">
      {{
        suffix
      }}
      <CountTo :start-val="0" :end-val="count" :duration="duration" />
      <hr :class="`${divider ? divider : ''} dark`" />
    </h1>
  </div>
</div>
  </div>
</template>
