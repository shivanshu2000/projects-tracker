<template>
  <div
    style="text-align:center; font-size:16px;font-weight:bold;background:white;padding:1rem 1.5rem; border-radius:15px;margin:0 auto;width:50%;letter-spacing:3px"
    v-if="projects.length === 0"
  >
    No projects. Add a new project
  </div>
  <div v-if="projects.length">
    <div class="list__container">
      <Project
        v-for="project in projects"
        :key="project.id"
        @delete-project="deleteProject"
        @change-status="changeStatus"
        @edit-project="editProject"
        :project="project"
      />
    </div>
  </div>
  <div>
    <div @click="toggleVisibility" class="add__project">
      <p>New project</p>
      <span class="material-icons add">
        add
      </span>
    </div>
    <NewProject
      :showButton="showForm"
      class="form__container"
      :class="{ show__form: showForm }"
      :title="title"
      :details="details"
      :edit="editMode"
      :id="id"
      @add-data="addProject"
      @edit-details="editDetails"
    />
  </div>
</template>

<script>
import Project from '@/components/Project.vue';
import NewProject from '@/components/NewProject.vue';

export default {
  name: 'Home',
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Title 1',
          details: 'this is title 1',
          completed: false,
        },
        {
          id: 2,
          title: 'Title 2',
          details: 'This is title 2',
          completed: false,
        },
      ],
      id: '',
      showForm: false,
      editMode: false,
      title: '',
      details: '',
    };
  },

  components: {
    Project,
    NewProject,
  },

  methods: {
    toggleVisibility() {
      {
        (this.showForm = !this.showForm), (this.editMode = false);
        this.title = '';
        this.details = '';
      }
    },

    deleteProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },

    changeStatus(id) {
      this.projects = this.projects.map((project) => {
        if (project.id === id) {
          return {
            ...project,
            completed: !project.completed,
          };
        }
        return project;
      });
    },

    addProject(title, details) {
      this.projects.push({
        id: Math.floor(Math.random() * 2500),
        title,
        details,
        completed: false,
      });
    },

    editProject(id) {
      const data = this.projects.find((project) => project.id == id);
      this.id = id;
      this.title = data.title;
      this.details = data.details;

      this.showForm = true;
      this.editMode = true;
    },

    editDetails(id, title, details) {
      this.projects = this.projects.map((project) => {
        if (project.id === id) {
          return {
            ...project,
            title: title,
            details: details,
          };
        }
        return project;
      });

      this.showForm = false;
    },
  },
};
</script>

<style>
.add__project {
  width: 150px;
  display: flex;
  justify-content: space-around;
  padding: 3px 7px;
  align-items: center;
  background-color: white;
  margin: 2rem auto;
  border-radius: 15px;
  cursor: pointer;
}

.form__container {
  visibility: hidden;
  max-height: 0;
  transition: max-height 0.43s ease-in-out, visibility 0.44s ease-in-out;
}

.form__container.show__form {
  height: auto;
  max-height: 900px;
  visibility: visible;
}

.add__project .add {
  color: black;
}
</style>
