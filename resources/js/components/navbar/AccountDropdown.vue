<template>
    <div class="relative inline-block text-left">
        <div>
            <span class="rounded-md shadow-sm">
                <button @click="isOpen = !isOpen" type="button"
                    class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-50 active:text-gray-800 transition ease-in-out duration-150"
                    id="options-menu" aria-haspopup="true" aria-expanded="true">
                    {{ name }}
                    <svg class="-mr-1 ml-2 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd"
                            d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
            </span>
        </div>

        <div :class="isOpen ? 'visible' : 'invisible'" class="origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg">
            <div class="rounded-md bg-white shadow-xs">
                <div class="py-1" role="menu" aria-orientation="vertical" aria-labelledby="options-menu">
                    <a href="#"
                        class="block px-4 py-2 text-sm leading-5 text-gray-700 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
                        role="menuitem">Account settings</a>
                    <form @submit.prevent="logout">
                        <button type="submit"
                            class="block w-full text-left px-4 py-2 text-sm leading-5 text-gray-700 hover:bg-gray-100 hover:text-gray-900 focus:outline-none focus:bg-gray-100 focus:text-gray-900"
                            role="menuitem">
                            Sign out
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['name'],
        data() {
            return {
                isOpen: false,
                csrf: document.querySelector('meta[name="csrf-token"]').getAttribute('content')
            }
        },
        methods: {
            logout() {
                axios.post('/logout',`{${this.csrf}}`)
                .then(res => {
                    location.reload();
                })
                .catch(err => {
                    console.error(err); 
                })
            }
        },
    }

</script>

<style>

</style>
