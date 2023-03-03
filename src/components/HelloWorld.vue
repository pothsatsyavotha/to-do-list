<template>
  <h1 class="text-center fw-bold text-uppercase">{{ title }}</h1>
  <div class="row">
    <div class="col-md-10">
      <input type="text" class="form-control" v-model="itemInput" />
    </div>

    <div class="col-md-2">
      <button @click="addItem" class="btn btn-success">Add Item</button>
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
        <th scope="row">{{ index + 1 }} ./</th>
        <td class="text-center" :class="statusChecking(task.status)">{{ task.title }}</td>
        <td class="text-center">{{ task.status }}</td>
        <td class="text-center">
          <span class="text-danger" style="cursor: pointer" @click="deleteItem(index)"
            ><i class="bi bi-trash"></i>
          </span>
          <span class="text-primary" style="cursor: pointer" @click="editItem(index)"
            ><i class="bi bi-pencil"></i>
          </span>
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
      editTask: null,
      changeStatus : ["todo","inprogress","finished"],
      tasks: [{
        title : "dhwudodw",
        status : "todo"
      }],
    }
  },
  methods: {
    addItem() {
      if (this.itemInput.length === 0) {
        return alert("Please input");
      }
      if(this.editTask === null){
          this.tasks.push({
            title:this.itemInput,
            status: "to do"
          });
      }
      else{
        console.log(this.itemInput);
        console.log(this.tasks[this.editTask].title);
        this.tasks[this.editTask].title = this.itemInput;
        this.editTask = null;
      }

      this.itemInput = "";
    },
    deleteItem(index) {
      this.tasks.splice(index, 1);
    },

    statusChecking(_status) {
      return {
        'finished': _status  === 'finished'
      }
    },
    editItem(index){
      this.itemInput = this.tasks[index].title;
      this.editTask = index;
    }
  }

}
</script>

<style scoped>
th {
  font-weight: bold;
  text-transform: uppercase;
  font-family: sans-serif;
}

.finished {
  text-decoration: line-through;
}
</style>
