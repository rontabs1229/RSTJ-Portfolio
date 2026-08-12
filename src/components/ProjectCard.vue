<template>
    <div class="card h-100" id="cards">
        <img :src="project.image" class="card-img-top" alt="...">
        <div class="card-body">
            <h4 class="card-title">{{ project.title }}</h4>
            <p class="card-text">
                {{ project.description }}
            </p>
            <div id="p_note">&copy; RSTJ_2026</div>
        </div>
    </div>
</template>
<script setup>
    import { defineProps } from 'vue';
    
    defineProps({
        project: Object
    })
    
</script>