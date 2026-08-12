<template>
    <div class="card h-100" id="cards">
        <img :src="shortCourse.image" class="card-img-top mt-3" alt="...">
        <div class="card-body">
            <h4 class="card-title">{{ shortCourse.title }}</h4>
            <p class="card-text">
                {{ shortCourse.description }}
            </p>
            <div id="p_note">&copy; RSTJ_2026</div>
        </div>
    </div>
</template>
<script setup>
    import { defineProps } from 'vue';
    
    defineProps({
        shortCourse: Object
    })
    
</script>