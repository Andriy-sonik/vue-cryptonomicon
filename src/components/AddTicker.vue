<template>
  <section>
    <div class="flex">
      <div class="max-w-xs">
        <label for="wallet" class="block text-sm font-medium text-gray-700"
          >Тикер</label
        >
        <div class="mt-1 relative rounded-md shadow-md">
          <input
            v-model="ticker"
            @keydown.enter="add"
            type="text"
            name="wallet"
            id="wallet"
            class="block w-full pr-10 border-gray-300 text-gray-900 focus:outline-none focus:ring-gray-500 focus:border-gray-500 sm:text-sm rounded-md"
            placeholder="Например DOGE"
          />
        </div>
        <div class="flex bg-white shadow-md p-1 rounded-md flex-wrap">
          <span
            v-for="el of filterList"
            :key="el"
            @click="ticker = el"
            class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer"
          >
            {{ el }}
          </span>
        </div>
        <div class="text-sm text-red-600" v-show="tickersError">
          Такой тикер уже добавлен
        </div>
      </div>
    </div>
    <add-button @click="add" type="button" :disabled="disabled" class="my-4" />
  </section>
</template>

<script>
import AddButton from "./AddButton";
export default {
  components: {
    AddButton,
  },
  props: {
    tickersError: {
      type: Boolean,
      default: false,
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  emits: {
    "add-ticker": (value) => typeof value === "string",
  },
  data() {
    return {
      ticker: "",
      filterList: ["BTC", "DOGE", "BCH", "CHD"],
    };
  },
  methods: {
    add() {
      if (this.ticker.length === 0) {
        return;
      }
      this.$emit("add-ticker", this.ticker);
      this.ticker = "";
    },
  },
};
</script>

<style></style>
