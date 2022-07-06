<template>
  <div class="container" style="max-width: 600px">
    <h2 class="text-center mt-5">Цитатник</h2>
    <div class="d-flex mt-5">
    <textarea
      type="text"
      v-model="task"
      @keydown.enter.exact.prevent="submitQuoteBook"
      class="w-100 form-control"
    ></textarea>
     <button class="btn btn-warning rounded-0" @click="submitTask">
        Отправить
      </button>
    </div>
    
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Цитаты</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td class="bodyblock">
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
      
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,

      tasks: [
        {
          name: "Господь, создавая человека, несколько переоценил свои силы. Оскар Уайльд",
        },
        {
          name: "Будь собой, остальные роли заняты. Оскар Уайльд",
        },
        {
          name: "Весь мир — театр, но труппа никуда не годится. Оскар Уайльд",
        },
      ],
    };
  },

  methods: {
     submitTask() {
      if (this.task.length === 0) return;

   
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
     
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      }

      this.task = "";
    },
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

 


    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    submitQuoteBook() {
      if (this.task.length === 0) return;
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        this.tasks.unshift({
          name: this.task,
          status: "todo",
        });
      }
      this.task= "";
    },
  },
};
</script>

<style scoped>
.bodyblock {
  border-radius: .5rem;
box-shadow: 0 3px 9px rgba(0,0,0,.082),0 2px 3px rgba(0,0,0,.05);
padding: 2em;
}
.btn-warning {
    margin-left: 20px;
}
.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}
.line-through {
  text-decoration: line-through;
}
</style>