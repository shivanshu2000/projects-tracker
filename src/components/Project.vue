<template>
  <div class="project" :class="{ completed: project.completed }">
    <div class="actions">
      <div class="left__section">
        <h3 @click="toggleDetails">{{ project.title }}</h3>
        <span
          @click="this.showDetails = !this.showDetails"
          :class="{ rotate: showDetails }"
          class="material-icons down"
        >
          expand_more
        </span>
      </div>
      <div class="icons">
        <span class="material-icons" @click="editProject">edit</span>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span class="material-icons tick" @click="changeStatus">done</span>
      </div>
    </div>
    <div class="divider" :class="{ show__divider: showDetails }" />
    <div class="details" :class="{ drop: showDetails }">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'project',
  props: ['project'],
  data() {
    return {
      showDetails: false,
    };
  },

  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },

    deleteProject() {
      this.$emit('delete-project', this.project.id);
    },

    changeStatus() {
      this.$emit('change-status', this.project.id);
    },

    editProject() {
      this.$emit('edit-project', this.project.id);
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 9px 0px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90874;
  overflow: hidden;
}

.details {
  max-height: 0px;
  visibility: hidden;
  padding: 0 1rem;
  transition: max-height 0.65s ease-in-out, visibility 0.51s ease-in-out 0.15s;
}

/* .drop{
    transition: height 3s linear;

} */

.details.drop {
  height: auto;
  max-height: 900px;
  visibility: visible;
}

h3 {
  cursor: pointer;
  text-align: center;
}

.actions {
  padding: 0 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.down.rotate {
  transform: rotate(180deg);
}

.left__section {
  flex: 1;
  padding-right: 19px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  cursor: pointer;
  font-size: 24px;
  margin-left: 9px;
  color: #ccc;
}

.material-icons:hover {
  color: #bbb;
}

.down {
  color: black;
  transition: transform 0.3s ease-in-out;
}

.down:hover {
  color: black;
}

.icons {
  margin-left: 1.5rem;
}

.project.completed {
  border-left: 4px solid #00ce89;
}

.project.completed .tick {
  color: #00ce89;
}
</style>
