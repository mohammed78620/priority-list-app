<template>
  <div class="container">
    <h2 class="text-center mt-5">Todo App</h2>
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <!-- <input v-model="priority" type="number" placeholder="Enter priority" value="1" min="1" max="10" class="form-control"> -->
      <select v-model="priority">
        <option value=1>1</option>
        <option value=2>2</option>
        <option value=3>3</option>
        <option value=4>4</option>
        <option value=5>5</option>
        <option value=6>6</option>
        <option value=7>7</option>
        <option value=8>8</option>
        <option value=9>9</option>
        <option value=10>10</option>
      </select>
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <div @click="hideOrShow()" class="text-center mt-5">
      <button >{{visible}}</button>
    </div>

    <div @click="orderByPriority()" class="text-center mt-5">
      <button >{{order}}</button>
    </div>

    <div class="text-center mt-5">
        <select v-model="priority1">
        <option value=1>1</option>
        <option value=2>2</option>
        <option value=3>3</option>
        <option value=4>4</option>
        <option value=5>5</option>
        <option value=6>6</option>
        <option value=7>7</option>
        <option value=8>8</option>
        <option value=9>9</option>
        <option value=10>10</option>
      </select>
      <button @click="filterByPriority()">filter</button>
    </div>
    

    

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">task</th>
          <th scope="col">priority</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>

        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td scope="row">{{task.name}}</td>
          <td>{{task.priority}}</td>
          <td >
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>          
            </div>

          </td>

        </tr>

      </tbody>
  </table>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      flag: true,
      flag1: true,
      flag2: true,
      task: '',
      priority:'',
      priority1:'',
      editedTask: null,

      tasks: [
        {
          name: 'task 1',
          priority: 3
        },
        {
          name: 'task 2',
          priority: 1
        }
        ,{
          name: 'task 3',
          priority: 6
        }
        ,{
          name: 'task 4',
          priority: 2
        }
      ],
      tempTask:[],
      order: "date",
      visible: "hide"

    }
  
  },
  methods: {
    submitTask(){
      if(this.task.length === 0 || this.priority.length === 0) return;
      if(this.editedTask.length === null){
        this.tasks.push({
          name: this.task,
          priority: this.priority
        })
        this.task = '';
        this.priority = '';
      }else{
        this.tasks[this.editedTask].name = this.task
        this.editedTask = null
      }
    },
    deleteTask(index){
      this.tasks.splice(index, 1);
    },
    orderByPriority(){
      
      if(this.flag){
        this.order = "priority"
        this.tempTask = [...this.tasks]
        this.tasks.sort(function(a,b){
          return a.priority-b.priority
        })
        this.flag = !this.flag
      }
      else{
        this.order = "date"
        this.tasks = [...this.tempTask]
        this.flag = !this.flag
      }
    },
    filterByPriority(){
      if(this.flag1){
        this.tempTask = [...this.tasks]
        this.tasks = this.tasks.filter(el => el.priority < this.priority1)
        this.flag1 = !this.flag1
      }else{
        this.tasks = [...this.tempTask]
        this.flag1 = !this.flag1
      }
    },
    hideOrShow(){
      if(this.flag2){
        this.tempTask = [...this.tasks]
        this.tasks = []
        this.visible = "show"
        this.flag2 = !this.flag2
      }
      else{
        this.tasks = [...this.tempTask]
        this.visible = "hide"
        this.flag2 = !this.flag2
      }

    },
    editTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
    }
  }
}
</script>

