<template>
  <div class="hero">
    <h2 class="title">Vue to-do list</h2>
    <input
      class="input"
      v-model.trim="task"
      placeholder="Add task"
      @keypress.enter="addToList"
    />
    <div v-if="taskList.length" class="taskList">
      <div
        class="taskItem"
        :class="activeTask === item && 'actTask'"
        v-for="item in taskList"
        :key="item"
        @click="activeTask ? (activeTask = '') : (activeTask = item)"
      >
        <div
          v-if="activeTask !== item"
          :class="{ ticked: completedTasks.includes(item) }"
        >
          {{ item }}
          <span v-if="completedTasks.includes(item)" class="statusText"
            >(completed)</span
          >
        </div>
        <div v-else class="active">
          <div class="completed" @click="tickTask(item)">
            {{ completedTasks.includes(item) ? "Incomplete ✖" : "Completed ✔" }}
          </div>
          <div class="deleted" @click="deleteTask(item)">Delete ✖</div>
        </div>
      </div>
    </div>
    <div v-else class="notasks">No tasks here...</div>
  </div>
</template>

<script>
export default {
  name: "Hero",
  data() {
    return { task: "", taskList: [], activeTask: "", completedTasks: [] };
  },
  created() {
    this.taskList = JSON.parse(localStorage.getItem("taskList")) || [];
    this.completedTasks =
      JSON.parse(localStorage.getItem("completedTasks")) || [];
  },
  methods: {
    addToList() {
      if (!this.task.trim() || this.task.length > 40) return;
      if (this.taskList.includes(this.task)) {
        this.task = "";
        return;
      }
      this.taskList.push(this.task);
      localStorage.setItem("taskList", JSON.stringify(this.taskList));
      this.task = "";
    },
    deleteTask(item) {
      this.taskList = this.taskList.filter((i) => i !== item);
      localStorage.setItem("taskList", JSON.stringify(this.taskList));
    },
    tickTask(item) {
      if (this.completedTasks.includes(item)) {
        this.completedTasks = this.completedTasks.filter((i) => i !== item);
      } else {
        this.completedTasks.push(item);
      }
      localStorage.setItem(
        "completedTasks",
        JSON.stringify(this.completedTasks)
      );
    },
  },
};
</script>

<style scoped>
.hero {
  display: flex;
  flex-direction: column;
  padding: 1.5rem;
  background: white;
  box-shadow: rgba(17, 17, 26, 0.3) 0px 8px 24px,
    rgba(17, 17, 26, 0.3) 0px 16px 56px, rgba(17, 17, 26, 0.3) 0px 24px 80px;
  border-radius: 5px;
  width: clamp(23ch, 75%, 46ch);
}
.input {
  min-width: 80%;
  border: none;
  padding: 0.75rem 1.5rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px,
    rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
  background: #fff2ef;
  border-radius: 50rem;
}
.input:focus {
  outline: none;
  border: none;
}
.taskList {
  padding-top: 1.5rem;
  text-align: left;
}
.taskItem {
  padding: 0.75rem 0 0.75rem 1.5rem;
  cursor: pointer;
}
.taskItem:hover {
  background: #e6f5ff;
  border-radius: 50rem;
}
.title {
  margin: 0.5rem 0 1.5rem;
}
.active {
  text-align: center;
  display: flex;
  justify-content: center;
}
.actTask {
  background: #fff2ef;
  border-radius: 50rem;
}
.completed {
  color: green;
  margin-right: 1.5rem;
}
.deleted {
  color: tomato;
}
.ticked {
  color: green;
  font-weight: bold;
}
.statusText {
  color: gray;
  font-style: italic;
  font-weight: normal;
}
.notasks {
  color: rgba(0, 0, 0, 0.3);
  font-style: italic;
  font-weight: normal;
  text-align: center;
  margin-top: 2rem;
}
</style>
