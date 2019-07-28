<template>
  <div class="container">
    <!-- Cover -->
    <div class="cover">
      <img src="/images/zenidex.png" />
    </div>

    <!-- Searchbar -->
    <div class="field m-t">
      <search @onSearchChange="onSearchChange" />
    </div>
    <result :criteria="searchCriteria" />
  </div>
</template>

<script>
import Search from "../components/Search";
import Result from "../components/Result";
import { value } from "vue-function-api";

export default {
  name: "home",
  components: {
    Search,
    Result
  },
  setup() {
    let searchCriteria = new value("");

    const onSearchChange = newValue => {
      searchCriteria.value = newValue;
    };

    return {
      searchCriteria,
      onSearchChange
    };
  }
};
</script>

<style></style>
