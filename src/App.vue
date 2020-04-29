<template>
  <div id="app">
    <div class="add-ticket-wrapper">
      <form @submit.prevent="onSubmit">
        <div>
          <label for="">Type</label>
          <input type="text" v-model="form.type">
        </div>
        <div>
          <label for="">Description</label>
          <input type="text" v-model="form.desc">
        </div>
        <div>
          <label for="">Fine</label>
          <input type="number" v-model="form.fine">
        </div>
        <div>
          <label for="">isPaid</label>
          <input type="checkbox" v-model="form.isPaid">
        </div>

        <button type="submit">{{ isEditing ? "update":"add"}}</button>
        <button v-if="isEditing" v-on:click="cancel">cancel</button>
      </form>

    </div>


    <div>
        <table>
          <tr>
            <th>type</th>
            <th>desc</th>
            <th>fine</th>
            <th>isPaid</th>
          </tr>
          <tr v-for="(item, index) in sourceArray" :key="index" :class="{ editing:checkEditing(index)}">
            <th>{{item.type}}</th>
            <th>{{item.desc}}</th>
            <th>{{item.fine}}</th>
            <th>{{item.isPaid ? "จ่ายแล้ว":"ยังไม่จ่าย"}}</th>
            <th><button v-on:click="paid(index)">{{ !item.isPaid ? "จ่ายแล้ว":"ยังไม่จ่าย"}}</button><button v-on:click="editItem(index)">edit</button><button v-on:click="delItem(index)">delete</button></th>
            
          </tr>
        </table>
    </div>
  </div>


</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      isEditing:false,
      editIndex:-1,
      form: { type:'',desc:'',fine:0 ,isPaid:false},
      sourceArray:[
      ]
    }
  },
  methods:{
    checkEditing(index){
      return (this.editIndex === index)
    },
    cancel(){

      this.editIndex = -1
      this.isEditing = false
      this.form = { type:'',desc:'',fine:0 ,isPaid:false}
    },
    paid(index) {
      // this.sourceArray.remove
      this.sourceArray[index].isPaid = !this.sourceArray[index].isPaid
      
    },
    editItem(index) {
      // this.sourceArray.remove
      this.editIndex = index
      this.form = {...this.sourceArray[index]}
      this.isEditing = true
      
    },
    delItem(index) {
      // this.sourceArray.remove
      this.sourceArray.splice(index,1)
      // console.log(index)
    },
    onSubmit() {
      if (this.editIndex > -1) {
        this.sourceArray[this.editIndex] = {...this.form}
      }
      else {
        this.sourceArray = [...this.sourceArray, {...this.form} ]
      }
      this.editIndex = -1
      this.isEditing = false
      this.form = { type:'',desc:'',fine:0 ,isPaid:false}
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#table {
  border-width: 2px;
  border-color: aquamarine;
}

.editing {
  background: aquamarine;
}
</style>
