<template>
  <form>
    <div class="error" v-if="error">
      <p>{{ error }}</p>
      <span style="color:white" @click="error = ''" class="material-icons">
        clear
      </span>
    </div>
    <label :class="{ grey: !showButton }">Title</label>
    <input
      :class="{ grey: !showButton }"
      :value="formTitle"
      @change="handleTitleChange"
      type="text"
    />
    <label :class="{ grey: !showButton }">Details</label>
    <textarea
      :class="{ grey: !showButton }"
      :value="formDetails"
      @change="handleDetailsChange"
    ></textarea>
    <button
      class="form__button"
      style="cursor:pointer"
      v-if="!editMode"
      @click.prevent="handleSubmit"
      :class="{ show__form__button: showButton }"
    >
      Add project
    </button>
    <button
      @click.prevent="editProject"
      class="form__button"
      v-if="editMode"
      style="cursor:pointer"
      :class="{ show__form__button: showButton }"
    >
      Edit project
    </button>
  </form>
</template>

<script>
export default {
  name: 'NewProject',
  data() {
    return {
      formTitle: '',
      formDetails: '',
      error: '',
      editMode: false,
      typing: false,
    };
  },
  props: ['showButton', 'title', 'details', 'edit', 'id'],

  updated() {
    if (this.typing) {
      return;
    }

    if (
      this.formTitle !== this.title ||
      this.formDetails !== this.details ||
      this.editMode !== this.edit
    ) {
      this.formTitle = this.title;
      this.formDetails = this.details;
      this.editMode = this.edit;
    }
  },
  methods: {
    handleTitleChange(e) {
      this.typing = true;
      this.formTitle = e.target.value;
    },

    handleDetailsChange(e) {
      this.typing = true;

      this.formDetails = e.target.value;
    },
    handleSubmit() {
      if (!!this.formTitle && !!this.formDetails) {
        this.$emit('add-data', this.formTitle, this.formDetails);
        this.formTitle = '';
        this.formDetails = '';
        this.typing = false;
        return;
      }
      return (this.error = 'All fields are required');
    },

    editProject() {
      if (!!this.formTitle && !!this.formDetails) {
        this.$emit('edit-details', this.id, this.formTitle, this.formDetails);
        this.formDetails = '';
        this.formTitle = '';
        this.typing = false;
        return;
      }
      this.error = 'Fields cannot be empty';
      this.typing = false;
    },
  },
};
</script>

<style>
.error {
  background: rgba(255, 0, 0, 0.3);
  color: white;
  font-size: 16px;
  font-weight: bold;
  border-radius: 15px;
  padding: 0.5rem 1.2rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-bottom: 1.5rem;
}

form {
  background: white;
  padding: 30px;
  border-radius: 10px;
  width: 50%;
  margin: 0 auto;
}

.grey {
  color: #ccc;
}

label {
  display: block;
  /* color: #ccc; */
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}

input {
  padding: 10px;
  border: 0;
  /* color: #ccc; */
  border-bottom: 1px solid #ccc;
  background-color: transparent;
  width: 100%;
  box-sizing: border-box;
}

textarea {
  border: 1px solid #ccc;
  padding: 10px;
  /* color: #ccc; */

  width: 100%;
  background-color: transparent;
  box-sizing: border-box;
  height: 100px;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}

input:focus,
textarea:focus {
  outline: none;
}

.form__button {
  visibility: hidden;
  transition: visibility 0.23s ease-in-out;
}

.form__button.show__form__button {
  visibility: visible;
}
</style>
