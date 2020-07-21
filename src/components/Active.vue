<template>
  <div>
    <ul>
      <li v-for="item in datas" :key="item.key" v-show="item.active == true">
        <div class="container">
          <input
            type="checkbox"
            value="item.id"
            @change="check(item.key)"
            :checked="!item.active"
          />
          <label for="checkbox" v-if="item.active">{{ item.todo }}</label>
          <label v-else for="checkbox">
            <del>{{ item.todo }}</del>
          </label>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "Active",
  props: {
    datas: Array,
  },
  methods: {
    check(id) {
      this.$emit("changeStatus", id);
    },
  },
};
</script>
<style scoped>
.container {
  text-align: left;
  width: 600px;
  position: relative;
  margin: auto;
}
ul {
  list-style-type: none;
  padding: 0;
  font-size: 25px;
}
input {
  position: relative;
  border: none;
  top: 5px;
  width: 25px;
  height: 25px;
}
label {
  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 18px;
  line-height: 22px;
  color: #000000;
  height: 22px;
}
</style>
