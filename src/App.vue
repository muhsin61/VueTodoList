<template>
  <div id="app">
    <h1>#todo</h1>
    <div class="center">
      <div class="header">
        <li class="firstLi" @click="handleClick(65)">All</li>
        <li class="firstLi" @click="handleClick(213)">Active</li>
        <li class="firstLi" @click="handleClick(386)">Complated</li>
      </div>
      
    </div>
    <div class="cizgi" ><div :style="{ left: hiza + 'px' }" class="cizgidiv"></div></div>
    <div class="bos"></div>
    <Add v-if="hiza<214" @handleAdd="handleAdd" />
    <All v-if="hiza===65" @changeKey="changeKey" :datas="datas"/>
    <Active v-if="hiza===213" @changeKey="changeKey" :datas="datas"/>
    <Complated v-if="hiza===386" @changeKey="changeKey" @deletes="deletes" @deleteAll="deleteAll" :datas="datas"/>
  </div>
</template>

<script>
import Add from "./components/Add.vue";
import All from "./components/All.vue";
import Active from "./components/Active.vue";
import Complated from "./components/Complated.vue";

export default {
  name: "App",
  components: {
    Add,
    All,
    Active,
    Complated
  },
  created: function () {
    if(localStorage.getItem("todos")){
      console.log("todos var")
      let actives = JSON.parse(localStorage.getItem("todos"))
      actives.forEach(item=>{
      console.log("item0" + item.muhsin)
      if(item!=""){this.datas.push({key:Math.random(),todo:item.todo,active:item.active})}
    })
    }else{
      const todos = [];
      localStorage.setItem("todos",todos)
      console.log("todos" + localStorage.getItem("todos"))
    }
    
  },
  data() {
    return {
      hiza: 65,
      datas: [
        { key: 1, todo: "bla bla bla", active: true },
        { key: 2, todo: "bla bla bla", active: false },
        { key: 3, todo: "deniisk", active: true }
      ]
    };
  },
  methods: {
    handleClick(sira) {
      this.hiza = sira;
    },
    handleAdd(add){
      let vat = true;
      console.log("addtype: " + typeof(add))
      this.datas.forEach(item=>{
        if(item.todo === add){
          console.log("aynı var")
          vat = false;
        }
      })
        if(vat){
          this.datas.push({key:Math.random(),todo:add,active:true})
        }
        let adds;
        if((localStorage.getItem("todos"))){
            let ekle = JSON.parse(localStorage.getItem("todos"))
            ekle.forEach(item=>{
              if(item.todo != add){
                ekle.push({"todo":add,"active":true})
                
              }//hatayı düzelt
              
            })
            ekle = JSON.stringify(ekle)
            localStorage.setItem("todos",ekle)
        }else{
          adds=([{"todo":add,"active":true}])
          localStorage.setItem("todos",JSON.stringify(adds))
        }
    },
    changeKey(id){
      let todo = JSON.parse(localStorage.getItem("todos"))
      let change = []
      this.datas.forEach(item => {
        console.log("item: " +  item)
        if(item.key==id){
          item.active = !item.active;
          console.log(  "length"+todo.length)
              todo.forEach(td => {
              if(item.todo == td.todo){
                console.log(" 1 tdactive...." + td.active)
                td.active = !td.active;
                console.log(" 2 tdactive...." + td.active)
                console.log("td: "+td)
                change.push(td)
              }
              else{
                change.push(td)
              }
            })
         }
        });
        localStorage.setItem("todos",JSON.stringify(change))
    },
    deletes(id){
      let copy = this.datas
      this.datas = []
      let todolar = []
      copy.forEach(item => {
        if(item.key!=id){this.datas.push(item)}
        else{
          let todos = JSON.parse(localStorage.getItem("todos"))
          todos.forEach(toDo=>{
            console.log(" 3 çalışıyor " + toDo.todo)
            console.log(" 3.5 çalışıyor localstorage " + toDo)
            if(toDo.todo !== item.todo){
              console.log(" 4 çalışıyor1 " + item.todo)
              todolar.push(toDo)
              console.log(" 5 todolar: " + todolar)
              console.log(" 6 todolar: " + JSON.stringify(todolar))
              }
          })
          localStorage.setItem("todos",JSON.stringify(todolar))
          console.log(" 7 todolar: " + todolar)}
        });
    },
    deleteAll(){
      let copy = this.datas
      this.datas = []
      let dltodo=[]
      const todos = JSON.parse(localStorage.getItem("todos"))
      todos.forEach(item=>{
          if(item.active){
            dltodo.push(item)
          }
      })
      localStorage.setItem("todos",JSON.stringify(dltodo))
      copy.forEach(item => {
        if(item.active){this.datas.push(item)}
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1{
  font-family: Raleway;
  font-style: normal;
  font-weight: bold;
  font-size: 36px;
  line-height: 42px;
  text-align: center;
  letter-spacing: -0.045em;
  color: #333333;
  right: 50px;
}
.header {
  position: relative;
  width: 600px;
  margin: auto;
}
.center{
  text-align: center;
}
.firstLi {
  padding: 0px 80px 0px 40px;
  font-family: Montserrat;
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 17px;
  color: #333333;
  display: inline-block;
  text-align: center;
}
.cizgi {
  position: relative;
  width: 600px;
  margin: auto;
  text-align: left;
  height: 0;
}
.cizgidiv{
  position: relative;
  width: 89px;
  height: 5px;
  background: #6DA6F2;
  border-radius: 4px 4px 0px 0px;
  bottom: 0px;
  transition: 0.8s;
  left: 0px;
}
.bos {
  position: relative;
  width: 600px;
  margin: auto;
  height: 1px;
  margin-top: 5px;
  background: #BDBDBD;
}

</style>

