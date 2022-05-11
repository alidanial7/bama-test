<template>
  <div>
    <ul v-if="hasHeader" class="search-container-column pa-0">
      <li
        v-for="listItem in listItems"
        :key="listItem.id"
        :class="listItem.isHeader ? 'search-item-start' : 'search-item-column'"
        @click="select(listItem)"
      >
        {{ listItem.name }}
      </li>
    </ul>
    <ul v-else class="search-container-row pa-0">
      <span v-for="listItem in listItems" :key="listItem.id" style="width: 20%">
        <li class="search-item-column" @click="select(listItem)">
          {{ listItem.name }}
        </li>
      </span>
    </ul>
  </div>
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
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: stretch;
    align-items: self-start;
  }
  .search-container-row {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: stretch;
    height: 150px;
    align-items: self-start;
  }
}
@media only screen and (min-width: 601px) {
  .search-container-column {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: stretch;
    height: 450px;
    align-items: self-start;
  }
  .search-container-row {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: stretch;
    height: 450px;
    align-items: self-start;
  }
}

.search-item-start {
  padding: 10px;
  color: #06bdb3;
  list-style-position: inside;
  font-weight: bold;
}
.search-item-column {
  padding: 10px;
  margin: 5px;
  list-style: none;
}
.search-item-row {
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

.test1 {
  width: 20%;
}
</style>
