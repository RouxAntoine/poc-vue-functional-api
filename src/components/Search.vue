<template>
  <div class="control has-icons-left has-icons-right">
    <input
      class="input is-danger"
      type="text"
      placeholder="Pokemon name"
      v-model="searchValue"
      @keyup="handleKeyUp"
    />
    <span class="icon is-small is-left">
      <i class="fa fa-search"></i>
    </span>
  </div>
</template>

<script>
import { value } from "vue-function-api";

export default {
  name: "search",
  setup(_, context) {
    const searchValue = new value("");

    const handleKeyUp = event => {
      context.emit("onSearchChange", event.target.value);
    };

    return {
      searchValue,
      handleKeyUp
    };
  }
};
</script>

<style></style>
