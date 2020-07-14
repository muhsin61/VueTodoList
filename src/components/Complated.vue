<template>
  <div>
      <div>
        <ul>
          <li v-for="item in datas" :key="item.key">
            <div class="container">
              <input type="checkbox" value="item.id" @change="check(item.key)" :checked="!item.active" v-show="!item.active">
              <label for="checkbox" v-if="!item.active"><del>{{item.todo}}</del><span class="material-icons right" @click="deletes(item.key)">delete</span></label>
            
            </div>
          </li>
        </ul>
        <div class="btnchg"><button @click="deleteAll"> <i class="material-icons">delete</i>delete all</button></div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Complated",
  props:{
      datas: Array
  },
  methods:{
      deletes(key){
          this.$emit("deletes",key)
      },
      deleteAll(){
          this.$emit("deleteAll",true)
      },
      check(id) {
      this.$emit("changeKey",id)
    }
  }
};
</script>
<style scoped>
.container{
  text-align: left;
  width: 600px;
  position: relative;
  margin: auto;
}
.btnchg{
  position: relative;
  width: 600px;
  text-align: right;
  margin: auto;
}
input{
    position: relative;
    border: none;
    top: 5px;
    width: 25px;
    height: 25px;
}
ul {
  list-style-type: none;
  padding: 0;
}
.div{
  position: relative;
}
.right{
  display: inline-block;
  position: relative;
  cursor: pointer;
  color: #BDBDBD;
  font-size: 25px;
  right: 0;
}
i{
  position: relative;
  top: 5px;
}
label{
  font-family: Montserrat;
  font-style: normal;
  font-weight: 500;
  font-size: 18px;
  line-height: 22px;
  color: #000000;
  height: 22px;
}
button{
    position: relative;
    border: none;
    color: white;
    cursor: pointer;
    width: 124px;
    height: 40px;
    background: #F18989;
    border-radius: 4px;
    font-family: Montserrat;
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    color: #FFFFFF;
}
button::before{
    content: "";
    position: absolute;
    opacity: 0;
    left: 0px;
    width: 10px ;
    height: 45px;
    top: 0;
    background: gray;
}
button:hover::before{
  opacity: 0.5;
  animation: mymove infinite 1s;
}
@keyframes mymove {
  0% {left: 0px;}
  50% {left: 130px;}
  100% {left: 0px;}
}
</style>
