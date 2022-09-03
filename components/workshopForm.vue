<template>
    <div>
    <button class="bg-black text-white active:bg-pink-600 font-bold uppercase text-sm px-6 py-3 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" v-on:click="showModal = true">
      Ajouter un atelier
    </button>
    <transition name="fade" appear>
    <div v-if="showModal" class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex">
      <div class="relative w-auto my-6 mx-auto max-w-9xl">
        <!--content-->
        <div class="border-0 rounded-lg shadow-lg relative flex flex-col w-full bg-white outline-none focus:outline-none">
          <!--header-->
          <div class="flex items-start justify-between p-5 border-b border-solid border-slate-200 rounded-t">
            <h3 class="text-3xl font-semibold">
              Ajouter un atelier
            </h3>
          </div>
          <!--body-->
          <div class="relative p-6 flex-auto">
            <form @submit.prevent="formSubmit">
              <div class="mb-6">
                <label for="title" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Titre</label>
                <input ref="title" class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light" placeholder="titre">
              </div>
              <div class="mb-6">     
                <label for="description" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Description</label>
                <textarea id="description" ref="description" rows="4" class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="description"></textarea>
              </div>
              <div class="mb-6">
                <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300" for="user_avatar">Image</label>
                <input ref="file" class="block w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 cursor-pointer dark:text-gray-400 focus:outline-none dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400" aria-describedby="user_avatar_help" id="user_avatar" type="file">
              </div>
              <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Ajouter</button>
            </form>
            <button class="text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800" v-on:click="showModal = false">fermer</button>
          </div>
        </div>
      </div>
    </div>
    </transition>
    <div v-if="showModal" class="opacity-25 fixed inset-0 z-40 bg-black"></div>
  </div>
</template>

<script setup>
const emit = defineEmits(['inFocus', 'submit'])
const title = ref('');
const description = ref('');
const file = ref('');
const showModal = ref(false);

const formSubmit = () => {
    formRequest().then( (res) => {
        showModal.value = false;
        emit('refreshWorkshop');
    }).catch( (error) => {
        console.log('tets', error);
    });
}
async function formRequest(){

    const formData = new FormData();

    formData.append('description', description.value.value);
    formData.append('title', title.value.value);
    formData.append('image', file.value.files[0]);

    return await $fetch(import.meta.env.VITE_API_ENDPOINT+'/api/new-workshop', 
    {
        method: 'POST',
        headers: { 'Authorization': "Bearer " + JSON.parse(localStorage.getItem( 'token' )).token, 'Accept': 'application/json' },
        body: formData 
    })
}

</script>