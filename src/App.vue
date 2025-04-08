<template>
  <div id="app">
    <div class="container">
      <h1>Список задач</h1>
      <ul class="task-list">
        <li v-for="task in tasks" :key="task.id" class="task-item">
          <input
            type="checkbox"
            v-model="task.done"
            @change="saveTasks"
            class="task-checkbox"
          />
          <span :class="{ done: task.done }" class="task-title">{{ task.title }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [], 
    };
  },
  methods: {
    // Метод для загрузки задач из tasks.json
    async loadTasksFromJson() {
      try {
        const response = await fetch("./tasks.json");
        const tasks = await response.json();
        return tasks;
      } catch (error) {
        console.error("Ошибка загрузки задач из JSON:", error);
        return [];
      }
    },

    // Метод для сохранения задач в локальное хранилище
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },

    // Метод для загрузки задач из локального хранилища
    loadTasksFromLocalStorage() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    },
  },
  async mounted() {
    // Сначала загружаем задачи из локального хранилища
    this.loadTasksFromLocalStorage();
    
    // Если в локальном хранилище нет данных, загружаем из tasks.json
    if (!this.tasks.length) {
      const tasksFromJson = await this.loadTasksFromJson();
      this.tasks = tasksFromJson;
    }
  },
};
</script>

<style scoped>
/* Общие стили для приложения */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Arial', sans-serif;
}

body {
  background-color: #f4f4f9;
  color: #333;
  padding: 20px;
}

/* Стиль контейнера */
.container {
  max-width: 600px;
  margin: 0 auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Заголовок */
h1 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 20px;
  color: #4caf50;
}

/* Стили для списка задач */
.task-list {
  list-style: none;
  padding-left: 0;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 12px;
  border-bottom: 1px solid #e0e0e0;
  transition: background-color 0.3s ease;
}

.task-item:hover {
  background-color: #f1f1f1;
}

.task-checkbox {
  margin-right: 15px;
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.task-title {
  font-size: 1.1rem;
  color: #333;
  transition: color 0.3s ease;
}

.task-title.done {
  text-decoration: line-through;
  color: #aaa;
}

/* Адаптивность */
@media (max-width: 600px) {
  .container {
    padding: 15px;
  }

  h1 {
    font-size: 1.5rem;
  }
}
</style>
