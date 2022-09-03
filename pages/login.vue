<template>
<div class="grid grid-flow-col place-items-center h-screen bg-alidou">
    <div class="justify-center col-span-1 row-span-3">
        <div class="w-full max-w-xs">
            <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="formSubmit">
                <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
                    Email
                </label>
                <input v-model="email" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="email" type="text" placeholder="ex: alidou@gmail.com">
                </div>
                <div class="mb-6">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                    Password
                </label>
                <input v-model="password" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="*****">
                </div>
                <div class="justify-center">
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                    Sign In
                </button>
                </div>
            </form>
        </div>
    </div>
    <div class="row-span-3">
        
    </div>
</div>
</template>

<script setup>

const email = ref('');
const password = ref('');
const route = useRouter();

const formSubmit = () => {
    formRequest().then( (res) => {
        localStorage.setItem( 'token', JSON.stringify(res) );
        route.push('/');
    }).catch( (error) => {
        console.log('tets', error);
    });
}

async function formRequest(){
    return await $fetch(import.meta.env.VITE_API_ENDPOINT+'/api/login_check', 
    {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        referrerPolicy: 'no-referrer',
        body: {
            'email': email.value,
            'password': password.value
        }
    })
}

</script>