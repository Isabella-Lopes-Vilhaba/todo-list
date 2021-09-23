<template>
  <li :class="mode">
    <span class="list-item">
      <input
        type="checkbox"
        :id="index"
        class="item-checkbox"
        v-model="item.checked"
      />
      <label :for="index" :class="getItemClass(item.checked)">{{
        item.label
      }}</label>
    </span>
    <span v-html="deleteIcon" @click="deleteItem(index)"></span>
  </li>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "ListItem",
  props: {
    item: Object,
    index: Number,
    mode: String
  },
  computed: {
    deleteIcon() {
      return feather.icons.trash.toSvg({ width: 20, color: "rgb(255, 0, 85)" });
    },
  },
  methods: {
    getItemClass(itemChecked) {
      return itemChecked ? "item-checked" : "";
    },
    deleteItem(index) {
      this.$emit("delete-item", index);
    },
  },
};
</script>

<style scoped>
li {
  width: 100%;
}

li,
.list-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

input[type="checkbox"] {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

input[type="checkbox"] + label {
  position: relative;
  cursor: pointer;
  padding-left: 40px;
}

input[type="checkbox"] + label::before {
  content: "";
  position: absolute;
  width: 15px;
  height: 15px;
  left: 0;
  bottom: 0;
  border: solid 2px #2c3e504f;
  vertical-align: bottom;
}

.dark input[type="checkbox"] + label::before {
  border: solid 2px #e2e8ee4f;
}

input[type="checkbox"]:checked + label::after {
  content: "";
  position: absolute;
  left: 7px;
  bottom: 6px;
  width: 10px;
  height: 20px;
  border-right: solid 3px green;
  border-bottom: solid 3px green;
  transform: rotate(45deg);
}

.item-checked {
  text-decoration: line-through;
}
</style>
