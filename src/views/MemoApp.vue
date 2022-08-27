<template>
  <h1>Vue メモ</h1>
  <div id="app">
    <div id="content" class="memo-list__container" draggable="true">
      <div
        v-for="(category, index) in displayCategories"
        :key="index"
        class="memo-list-a"
        style="min-width: 400px"
        @dragover="dragOverCategory(category)"
        draggable="true"
      >
        <div class="memo-list" @dragover="dragOverCategory(category)">
          {{ category.name }}
          <div
            v-for="(task, index) in category.tasks"
            :key="index"
            class="memo"
            @dragstart="dragTask(task)"
            @dragover="dragOverTask(task)"
            draggable="true"
          >
            <div class="memo__checkbox" draggable="false">
              <input type="checkbox" v-model="task.isDone" />
            </div>
            <div
              v-if="task.isDone"
              class="memo__text memo__text--done"
              draggable="false"
            >
              {{ task.name }}
            </div>
            <div v-else class="memo__text">{{ task.name }}</div>

            <button @click="deleteTask(task.id)" draggable="false">削除</button>
          </div>
        </div>
        <div class="add-memo-field">
          <input
            class="add-memo-field__input"
            type="text"
            v-model="inputMemo"
          />
          <button @click="addTask(index)" class="add-memo-field__button">
            追加
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      category: "",

      oid: 7,

      categories: [
        {
          id: 1,
          name: "テストA",
          collapsed: false,
        },
        {
          id: 2,
          name: "テストB",
          collapsed: false,
        },
        {
          id: 3,
          name: "テストC",
          collapsed: false,
        },
      ],

      tasks: [],

      // tasks: [
      //   {
      //     id: 1,
      //     category_id: 1,
      //     name: "テスト1",
      //   },
      //   {
      //     id: 2,
      //     category_id: 1,
      //     name: "テスト2",
      //   },
      //   {
      //     id: 3,
      //     category_id: 3,
      //     name: "テスト3",
      //   },
      //   {
      //     id: 4,
      //     category_id: 2,
      //     name: "テスト4",
      //   },
      //   {
      //     id: 5,
      //     category_id: 2,
      //     name: "テスト5",
      //   },
      //   {
      //     id: 6,
      //     category_id: 1,
      //     name: "テスト6",
      //   },
      // ],
    }
  },

  methods: {
    dragTask(task) {
      this.task = task
    },

    dragOverTask(overTask) {
      if (overTask.id !== this.task.id) {
        const deleteIndex = this.tasks.findIndex(
          (task) => task.id === this.task.id
        )
        const addIndex = this.tasks.findIndex((task) => task.id === overTask.id)
        this.tasks.splice(deleteIndex, 1)
        // カテゴリーid変更
        this.task.category_id = overTask.category_id
        this.tasks.splice(addIndex, 0, this.task)
      }
    },

    dragOverCategory(overCategory) {
      if (this.task.category_id !== overCategory.id) {
        const tasks = this.tasks.filter(
          (task) => task.category_id === overCategory.id
        )
        if (tasks.length === 0) this.task.category_id = overCategory.id
      }
    },

    addTask(index) {
      if (this.inputMemo) {
        if (this.inputTask !== "") {
          const task = {
            id: this.oid++,
            category_id: index + 1,
            name: this.inputMemo,
            isDone: false,
          }
          this.tasks.push(task)
          this.inputMemo = ""
          console.log(this.id)
        }
      }
    },

    deleteTask(index) {
      console.log(index)
      for (let i = 0; i < this.tasks.length; i++) {
        const task = this.tasks[i]
        if (task.id === index) {
          this.tasks.splice(this.tasks.indexOf(task), 1)
        }
      }
    },
  },

  computed: {
    displayCategories() {
      return this.categories.map((category) => {
        const tasks = this.tasks.filter(
          (task) => task.category_id === category.id
        )
        return {
          id: category.id,
          name: category.name,
          tasks,
        }
      })
    },
  },
}
</script>

<style scoped>
.memo-list__container {
  /* padding-left: 5rem;
  padding-right: 5rem; */
  padding: 2rem;
  margin: 2rem;
  display: flex;
  flex-direction: row;
}

.memo-list-a {
  min-width: 400px;
  /* padding-left: 5rem;
  padding-right: 5rem;
  display: flex;
  flex-direction: row;
  margin: auto; */
  /* align-items: stretch;
  max-width: 512px;
  margin-left: auto;
  margin-right: auto; */
}

.memo-list {
  background-color: gray;
  margin: 0.5rem;
  padding: 0.5rem;
  justify-content: space-between;
  /* padding-left: 5rem;
  padding-right: 5rem;
  display: flex;
  flex-direction: row;
  margin: auto; */
  /* align-items: stretch;
  max-width: 512px;
  margin-left: auto;
  margin-right: auto; */
}

.memo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0.5rem;
  padding: 0.5rem;
  border-radius: 5px;
  background-color: white;
}

.add-memo-field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;

  margin: auto;
}

.add-memo-field__input {
  padding: 10px;
  margin: 0rem 0.5rem;
}
.add-memo-field__button {
  padding: 0.5rem 0.5rem;
  margin: 0rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.memo:hover {
  color: white;
  background-color: #b23b61;
}

.memo__text {
  pointer-events: none;
  margin-left: 2rem;
  text-align: left;
}

.memo__text--done {
  text-decoration-line: line-through;
}

.memo__delete {
  margin-left: 1rem;
  padding: 0.5rem 0.5rem;
  border: solid 1px black;
  border-radius: 5px;
  background-color: white;
}

.memo__delete:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}

.add-memo-field__button:hover {
  background-color: #b2ae3b;
  border-radius: 5px;
}
</style>
