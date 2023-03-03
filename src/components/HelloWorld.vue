<template>
  <h1 class="text-center fw-bold text-uppercase">{{ title }}</h1>
  <div class="row">
    <div class="col-md-10">
      <input type="text" class="form-control" v-model="itemInput" />
    </div>

    <div class="col-md-2">
      <button @click="addItem" class="btn btn-success">add item</button>
    </div>
  </div>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col" class="text-center">title</th>
        <th scope="col" class="text-center">status</th>
        <th scope="col" class="text-center">action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(task, index) in tasks" :key="index">
        <th scope="row">{{ index + 1 }}</th>
        <td class="text-center" :class="statusChecking(task.status)">{{ task.title }}</td>
        <td class="text-center">{{ task.status }}</td>
        <td class="text-danger text-center">
          <i class="bi bi-trash" @click="deleteItem(index)"></i>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script lang="js">
export default {
  name: "HelloWorld",

  data() {
    return {
      title: "To do list",
      itemInput: "",
      tasks: [
        {
          title: "go home",
          status: "to-do"
        },
        {
          title: "eat chocolate 1 kilogram in 1 hour",
          status: "finished"
        },
      ],
    }
  },
  methods: {
    addItem() {
      if(this.itemInput.length === 0){
        return alert("Please input");
      }
      this.tasks.push(
        {title:this.title,status:this.status}
      );
      this.itemInput = "";
    },
    deleteItem(index){
      this.tasks.splice(index,1);
    },
    statusChecking(_status){
      return{
        'finished' : _status === 'finished'
      }
    },
  }

}
</script>

<style scoped>
.finished {
  text-decoration: line-through;
}
</style>
