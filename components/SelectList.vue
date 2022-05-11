<template>
  <ul
    :class="
      hasHeader ? 'search-container-column pa-0' : 'search-container-row pa-0'
    "
  >
    <li
      v-for="listItem in listItems"
      :key="listItem.id"
      :class="
        hasHeader
          ? listItem.isHeader
            ? 'search-item-start'
            : 'search-item-column'
          : 'search-item-row'
      "
      @click="select(listItem)"
    >
      <span>
        {{ listItem.name }}
      </span>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    listItems: {
      type: Array,
      required: true,
    },
    hasHeader: {
      type: Boolean,
      required: true,
    },
  },
  emits: ["select"],
  methods: {
    select(listItem) {
      this.$emit("select", listItem);
    },
  },
};
</script>

<style>
@media only screen and (max-width: 600px) {
  .search-container-column {
    display: flex;
    flex-direction: column;
  }
}
@media only screen and (min-width: 601) {
  .search-container-column {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: stretch;
    height: 450px;
    align-items: self-start;
    flex-grow: 1;
  }
}

.search-container-row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: stretch;
  height: 450px;
  align-items: self-start;
  flex-grow: 1;
}
.search-item-start {
  padding: 10px;
  flex-grow: 1;
  color: #06bdb3;
  list-style-position: inside;
  font-weight: bold;
}
.search-item-column {
  padding: 10px;
  margin: 5px;
  flex-grow: 1;
  list-style: none;
}
.search-item-row {
  flex-grow: 1;
  padding: 10px;
  max-width: 25%;
  margin: 5px;
  list-style: none;
}
.search-item-column:hover {
  border: 1px solid #06bdb3;
  border-radius: 5px;
  padding: 9px;
}
.search-item-row:hover {
  border: 1px solid #06bdb3;
  border-radius: 5px;
  padding: 9px;
}
</style>
