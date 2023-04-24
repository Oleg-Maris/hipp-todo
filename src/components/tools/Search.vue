<template>
  <v-text-field
    :class="{ closed: searchClosed && !$store.state.search }"
    :disabled="$store.state.sorting"
    :value="$store.state.search"
    @blur="searchClosed = true"
    @focus="searchClosed = false"
    @input="$store.commit('setSearch', $event)"
    class="expanding-search mt-1"
    placeholder="Search"
    prepend-inner-icon="mdi-magnify"
    clearable
    dense
    filled
  />
</template>

<script>
export default {
  data: () => ({
    searchClosed: true,
  }),
};
</script>

<style lang="sass">
.expanding-search
  transition: max-width 0.3s
  .v-input__slot
    cursor: pointer !important
    &:before, &:after
      border-color: transparent !important
  &.closed
    max-width: 45px
    .v-input__slot
      background: transparent !important
</style>
