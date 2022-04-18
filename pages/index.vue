<template>
  <section>
    <Header />
    <div class="py-4">
      <div class="container">
        <div
          class="
            title
            border-bottom
            d-flex
            align-items-center
            justify-content-between
            py-2
          "
        >
          <h5>Task</h5>
          <div class="d-flex align-items-center ms-auto">
            <input
              type="text"
              class="form-control"
              placeholder="Search"
              v-model="category"
            />
            <div class="d-flex align-items-center justify-content-end w-100">
              <span class="me-2">View As</span>
              <button
                class="btn btn-outline-secondary py-1 px-3"
                @click="isGrid = !isGrid"
              >
                {{ isGrid ? "Grid" : "List" }}
              </button>
            </div>
            <div>&nbsp;</div>
            <select class="form-select" v-model="category">
              <option value="Mobil">Mobil</option>
              <option value="Motor">Motor</option>
            </select>
            <select class="form-select" v-model="sortby">
              <option value="asc">Ascending</option>
              <option value="desc">Descending</option>
            </select>
            <button
              class="btn btn-outline-primary py-1 px-3 me-4"
              @click="shuffle"
            >
              Shuffle!
            </button>
          </div>
        </div>
        <transition-group name="tasks" tag="div" class="list-task row">
          <CardItem
            v-for="tasks in resultQuery"
            :key="JSON.stringify(tasks.id)"
            :tasks="tasks"
            :isGrid="isGrid"
            :ok="ok"
          />
        </transition-group>
        <div class="action py-2">
          <a
            href="#"
            class="add-button"
            v-if="!isCreating"
            @click="isCreating = !isCreating"
            >Add Task</a
          >
          <div class="add-card" v-else>
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input
                  class="form-control border-0 mb-2"
                  placeholder="Title"
                  type="text"
                />
                <textarea
                  class="form-control border-0 small"
                  placeholder="Description"
                  rows="3"
                ></textarea>
              </div>
            </div>
            <div class="button-wrapper d-flex">
              <button class="btn btn-outline-primary me-2">Save</button>
              <button
                class="btn btn-outline-danger"
                @click="isCreating = !isCreating"
              >
                Cancel
              </button>
            </div>
          </div>
        </div>
        <div v-if="ok == true">
          <button @click="ok = !ok" class="btn btn-outline-success">
            Hide
          </button>
        </div>
        <div v-if="ok == false">
          <button @click="ok = !ok" class="btn btn-outline-success">
            Show all hidden
          </button>
        </div>
      </div>
    </div>
    <Footer />
  </section>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      ok: true,
      category: "",
      searchQuery: "",
      sortby: "title",
      isGrid: false,
      isCreating: false,
      // Daftar task
      tasks: [
        {
          id: 1,
          title: "Task 1",
          description: "ini deskripsi 1",
          category: "Mobil",
          isDone: false,
        },
        {
          id: 2,
          title: "Task 2",
          description: "ini deskripsi 2",
          category: "Motor",
          isDone: false,
        },
        {
          id: 3,
          title: "Task 3",
          description: "ini deskripsi 3",
          category: "Motor",
          isDone: false,
        },
        {
          id: 4,
          title: "Task 4",
          description: "ini deskripsi 4",
          category: "Mobil",
          isDone: false,
        },
      ],
    };
  },
  computed: {
    resultQuery() {
      if (this.category) {
        return this.tasks.filter((item) => {
          return this.category
            .toLowerCase()
            .split("")
            .every((v) => item.category.toLowerCase().includes(v));
        });
      } else {
        return this.tasks;
      }
    },
    Category() {
      if (tasks.category == "Mobil") {
        alert("Kategori Mobil");
      }
      if (tasks.category == "Motor") {
        alert("Kategori Motor");
      } else {
        alert("Kabeh Di Pilih");
        return this.tasks;
      }
    },
  },
  methods: {
    handleSubmit() {
      console.log(this.form);
      this.tasks.push(this.form);
      this.isCreating = false;
    },
    shuffle() {
      this.tasks = _.shuffle(this.tasks);
    },
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
};
</script>
<style>
.tasks-move {
  transition: 0.4s;
}
</style>
