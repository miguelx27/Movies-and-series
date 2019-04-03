<template>
  <div :class="['header', { 'header--row': rowLayout }]">
    <h1 class="header__title">Movies & series</h1>
    <div
      :class="['header__search', { 'header__search--centered': !rowLayout, 'ml-auto': rowLayout }]"
    >
      <div :class="['d-flex flex-column', { 'align-items-center': !rowLayout }]">
        <v-text-field
          v-model="search"
          append-icon="search"
          placeholder="Search"
          solo
          hide-details
        ></v-text-field>
        <v-radio-group v-model="row" row dark hide-details class="header__radios">
          <v-radio label="Movies" value="radio-1"></v-radio>
          <v-radio label="Series" value="radio-2"></v-radio>
        </v-radio-group>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',

  data() {
    return {
      search: '',
      row: ''
    };
  },

  computed: {
    rowLayout() {
      return this.search.length >= 3;
    }
  }
};
</script>

<style lang="scss">
.header {
  height: 100%;
  background-color: #3b7eca;
  padding: 20px;
  transition: height 1s;

  &--row {
    display: flex;
    height: 120px;

    .header__radios {
      margin-top: 10px;
      align-self: flex-end;
    }

    .header__search {
      margin-left: auto;
    }
  }

  &__search {
    &--centered {
      align-items: center;
      display: flex;
      flex-direction: column;
      height: 100%;
      justify-content: center;
    }
  }

  &__title {
    color: white;
  }
}
</style>
