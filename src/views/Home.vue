<template>
 <div v-if="projects.length">
   <div v-for="project in projects" :key="project.id">
     <Project @delete-project="deleteProject" :project="project"/>
   </div> 
 </div>
</template>

<script>

import Project from '@/components/Project.vue'

export default {
  name: 'Home',
  data(){
    return{
      projects:[
         {
            id:1,
            title:"Title 1",
            details:"This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 This is title 1 "
        },
        {
            id:2,
            title:"Title 2",
            details:"This is title 2"

        }
      ]
    }
  },

  components:{
    Project
  },

  methods:{
    deleteProject(id){
      this.projects = this.projects.filter(project=> project.id!==id)
    }
  }
}
</script>
