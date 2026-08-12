<template>
    <div class="container my-5 justify-content-center" id="projects">
        <div class="row">
            <div class="col-12 pt-5">
                <h2>My Projects</h2>
                <h3 class="pt-3">Main Course</h3>
            </div>
        </div>
        <div class="row px-3 justify-content-center">
            <div 
                v-for="(group, index) in chunkedProjects" 
                :key="index" 
                class="row my-5 g-4 justify-content-center w-100"
            >
                <div 
                    v-for="project in group" 
                    :key="project.id" 
                    class="col-12 col-md-6 col-lg-4"
                >
                    <ProjectCard :project="project" />
                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <h3 class="col-12 mt-5">Short Courses</h3>
        </div>
        <div class="row mt-3 px-3 pb-5 g-4 justify-content-center">
            <div 
                v-for="shortCourse in shortCourses" 
                :key="shortCourse.id" 
                class="col-12 col-md-6 col-lg-4"
            >
                <ShortCourseCard :shortCourse="shortCourse" />
            </div>
        </div>
    </div>
</template>
<script setup>
    import { computed } from 'vue';
    import ProjectCard from './ProjectCard.vue';
    import ShortCourseCard from './ShortCourseCard.vue';
    import projects from '../data/projects.json';
    import shortCourses from '../data/shortCourses.json';
    
    const chunkSize = 3;
    const chunkedProjects = computed(() => {
        const chunks = [];
        for (let i=0; i < projects.length; i += chunkSize) {
            chunks.push(projects.slice(i, i + chunkSize));
        }
        return chunks;
    })
    
</script>