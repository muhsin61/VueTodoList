<template>
  <div>
    <form action="">
      <input
        id="input"
        type="text"
        placeholder="add details"
        value="addSomething"
        v-model="addSomething"
        @submit="add"
      />
      <input id="inputBtn" type="submit" value="Add" @click="add" />
    </form>
  </div>
</template>
<script>
export default {
  name: "Add",
  data: () => {
    return {
      addSomething: "",
    };
  },
  methods: {
    add(e) {
      if (this.addSomething != "") {
        this.$emit("handleAdd", this.addSomething);
        this.addSomething = "";
      }
      e.preventDefault();
    },
  },
};
</script>

<style scoped>
div {
  margin-top: 50px;
}
#input {
  position: relative;
  border: none;
  width: 476px;
  height: 56px;
  border: 1px solid #bdbdbd;
  box-sizing: border-box;
  border-radius: 12px;
}
#inputBtn {
  position: relative;
  border: none;
  cursor: pointer;
  width: 109px;
  height: 56px;
  background: #6da6f2;
  box-shadow: 0px 2px 6px rgba(127, 177, 243, 0.4);
  border-radius: 12px;
  font-family: Montserrat;
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 17px;
  color: #ffffff;
}
</style>
