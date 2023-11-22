<script>
export default {
  name: "MenuItem",
  props: {
    menuData: {
      type: Object,
    },
    level: Number,
    count: Number,
    openArray: Array,
    handleOpenArray: Function,
    openFlag: Boolean,
  },
  data() {
    return {};
  },
  computed: {
    listChecker() {
      return (
        this.$props.menuData.children &&
        this.$props.menuData.children.length !== 0
      );
    },
  },
  methods: {
    handleClick() {
      this.$props.handleOpenArray(this.$props.level, this.$props.count);
    },
  },
};
</script>

<template>
  <li :class="{ 'menu--opened': $props.openFlag }">
    <label
      @click.stop="handleClick"
      class="label-name"
      :class="{ 'label-name--opened': $props.openFlag }"
    >
      {{ $props.menuData.text }}
    </label>
    <ul v-show="$props.openFlag" v-if="listChecker">
      <MenuItem
        v-for="(menuData, index) in $props.menuData.children"
        :menu-data="menuData"
        :key="menuData.key"
        :level="$props.level + 1"
        :count="index"
        :open-array="$props.openArray"
        :handle-open-array="$props.handleOpenArray"
        :open-flag="
          $props.openFlag && $props.openArray[$props.level + 1] === index
            ? true
            : false
        "
      ></MenuItem>
    </ul>
  </li>
</template>

<style scoped>
label {
  display: inline-block;
  width: 100%;
  padding: 10px 0;
}

ul {
  margin: 0;
  padding: 0;
}

li {
  margin: 0;
  padding: 0 0 0 1.5rem;
  list-style-type: none;
}

.label-name {
  color: white;
}

.menu--opened {
  background-color: gray;
}

.label-name--opened {
  color: yellow;
}
</style>
