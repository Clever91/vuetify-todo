<template>
  <div class="home">
    <v-text-field
      outlined
      label="Add new task"
      append-icon="mdi-plus"
      class="pa-3"
      hide-details="false"
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"
      v-model="newTaskName"
    ></v-text-field>
    <v-list
      flat
      class="pt-0"
    >
      <div v-for="task in tasks" :key="task.id">
        <v-list-item 
          @click="doneTask(task.id)"
          :class="{'blue lighten-4': task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through': task.done}">{{ task.name }}</v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon @click="deleteTask(task.id)">
                <v-icon color="teal lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>

export default {
  name: 'List',
  data () {
    return {
      newTaskName: '',
      tasks: [
        {
          id: 1,
          name: 'Wake Up',
          done: false
        },
        {
          id: 2,
          name: 'Running',
          done: true
        },
      ],
    }
  },
  methods: {
    doneTask (id) {
      var task = this.tasks.filter(task => task.id == id)[0]
      task.done = !task.done
    },
    deleteTask (id) {
      this.tasks = this.tasks.filter(task => task.id != id)
    },
    addTask () {
      let newTask = {
        id: Date.now(),
        name: this.newTaskName,
        done: false
      }
      this.tasks.push(newTask)
      this.newTaskName = ''
    }
  }
}
</script>
