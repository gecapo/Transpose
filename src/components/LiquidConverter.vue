<template>
  <div>

    <div>
        <div>
          <input v-model="absoluteUnit" type="number" />
        </div>

        <select v-model="unitOfMeasurement">
          <option v-for="unit in units" :value="unit.value" :key="unit.value">
            {{ unit.title }}
          </option>
        </select>

    </div>

    <div v-for="unit in filteredUnits" class="card" :key="unit.title">
        <span
          class="number"
          v-html="format((absoluteUnit * unitOfMeasurement) / unit.value)"
        />
        <span class="label">
          {{ unit.title }}
          <sup
            class="asterisk"
            v-if="(!isMetric && unit.metric) || (isMetric && !unit.metric)"
            >*</sup
          >
        </span>
    </div>

    <div>
        * Rounded; not precise
    </div>

  </div>
</template>

<script>
import frac from "frac";

export default {
  name: "LiquidConverter",
  data: () => ({
    units: [
      {
        title: "TSP",
        value: 0.5,
      },
      {
        title: "ML",
        value: 0.1014420675,
        metric: true,
      },
      {
        title: "TBSP",
        value: 1.5,
      },
      {
        title: "Oz",
        value: 3,
      },
      {
        title: "Cup",
        value: 24,
      },
      {
        title: "Pint",
        value: 48,
      },
      {
        title: "Quart",
        value: 96,
      },
      {
        title: "Liter",
        value: 101.4420675,
        metric: true,
      },
      {
        title: "Gallon",
        value: 384,
      },
    ],
    fractions: [128, 64, 32, 24, 16, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1],
    unitOfMeasurement: 3,
    absoluteUnit: 2,
  }),
  methods: {
    format(num) {
      num = Number(num);
      const [_, numerator, denominator] = frac(num, 128);
      if (
        numerator < denominator &&
        numerator > 0 &&
        this.fractions.includes(denominator)
      ) {
        console.log(_);
        return `${numerator} / ${denominator}`;
      }
      return parseInt(num) === num ? num : num.toString().substring(0, 10);
    },
    decimalToFraction(_decimal) {
      if (_decimal == 1) {

        return {
          top: 1,
          bottom: 1,
          display: 1 + ":" + 1,
        };

      } else {

        const gcd = (a, b) => {
          return b ? gcd(b, a % b) : a;
        };

        var top = _decimal.toString().replace(/\d+[.]/, "");
        var bottom = Math.pow(10, top.length);

        if (_decimal > 1) {
          top = +top + Math.floor(_decimal) * bottom;
        }

        var x = gcd(top, bottom);

        return {
          top: top / x,
          bottom: bottom / x,
          display: top / x + ":" + bottom / x,
        };
        
      }
    },
  },
  computed: {
    filteredUnits() {
      return this.units.filter((unit) => unit.value != this.unitOfMeasurement);
    },

    isMetric() {
      return this.unitOfMeasurement.toString().includes("4420675");
    },
  },
};
</script>


<style>
</style>