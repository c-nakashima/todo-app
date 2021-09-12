<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      label="Add Task"
      @click:append="addTask()"
      @keyup.enter="addTask()"
      class="pa-4"
      append-icon="mdi-plus"
      color="brown lighten-2"
      outlined
      hide-details
      clearable
    ></v-text-field>
    <v-list flat class="pt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'grey lighten-2': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done, '-unactive': task.done }"
                class="color-purple"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon>
                <v-icon
                  color="brown lighten-2"
                  @click.stop="deleteTask(task.id)"
                  >mdi-delete</v-icon
                >
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
    <v-snackbar
      v-model="snackbar"
    >
      {{ text }}
      <!-- {{ texts[0].message }} -->
      <template v-slot:action="{ attrs }">
        <v-btn
          class="color-baige"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data () {
    return {
      newTaskTitle: '',
      tasks: [
      ],
      snackbar: false,
      text: 'New tasks has been added!'
      // TODO: タスク追加時と削除時でメッセージを変えたい
      // texts: [
      //   {
      //     action: 'add',
      //     message: 'New tasks has been added!'
      //   },
      //   {
      //     action: 'delete',
      //     message: 'New tasks has been deleted!'
      //   }
      // ]
    }
  },
  methods: {
    addTask () {
      const newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }
      if (this.newTaskTitle) {
        this.tasks.push(newTask)
        this.snackbar = true
      }
      this.newTaskTitle = ''
    },
    doneTask (id) {
      const task = this.tasks.filter((task) => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask (id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
      this.snackbar = true
    }
  }
}
</script>

<style scoped>
  .-unactive{
    opacity: .5;
  }
  .color-black{
    color: #36312E;
  }
  .color-purple{
    color: #716679;
  }
  .color-baige{
    color: #FDF4E7;
  }
  .color-brown{
    color: #AE9C94;
  }
  .color-green{
    color: #93A8B2;
  }
</style>