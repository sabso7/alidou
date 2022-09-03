<template>
    <div class="grid grid-flow-col place-items-center h-screen">
        <div class="justify-center col-span-1 row-span-3">
            <WorkshopForm @refreshWorkshop="refreshWorkshop"></WorkshopForm>
        </div>
        <div class="row-span-3">
            <div v-for="(workshop, index) in workshopData" key="index">
            <h4>{{workshop}}</h4>
            </div>
        </div>
    </div>
</template>
<script setup>

const refreshWorkshop = () =>{ refreshNuxtData('workshopData')};
const { data: workshopData } = useLazyAsyncData('workshopData', () => $fetch(import.meta.env.VITE_API_ENDPOINT+'/api/workshop').then(function(response) {
    return JSON.parse(response);
}));

</script>