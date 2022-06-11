<template>
  <a href="#/lenght">Convert Lenght</a> |
  <a href="#/liquid">Convert Liquid</a> |
  <a href="#/liquid">Convert Weight</a> |
  <component :is="currentView" />
</template>

<script>
import LengthConverter from "@/components/LengthConverter";
import LiquidConverter from "@/components/LiquidConverter";
import WeightConverter from "@/components/WeightConverter";

const routes = {
  "/lenght": LengthConverter,
  "/liquid": LiquidConverter,
  "/weight": WeightConverter,
};

export default {
  name: "SimpleRouter",
  data() {
    return {
      currentPath: window.location.hash,
    };
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || "/"];
    },
  },
  mounted() {
    window.addEventListener("hashchange", () => {
      this.currentPath = window.location.hash;
    });
  },
};
</script>