<template>
    <div class="flex h-screen">
        <!-- Sidebar -->
        <aside class="w-64 bg-gray-800 text-white flex flex-col">
            <div class="p-4 flex flex-col items-center">
                <img :src="logo" alt="Company Logo" />
                <span class="mt-2 text-lg font-bold">HITACHI - ITPS</span>
            </div>
            <nav class="mt-4 flex-1">
                <router-link to="/dashboard" class="block px-4 py-2 text-gray-200 hover:bg-gray-700">Dashboard</router-link>
                <router-link to="/" class="block px-4 py-2 text-gray-200 hover:bg-gray-700">Home</router-link>
                <router-link to="/profile" class="block px-4 py-2 text-gray-200 hover:bg-gray-700">Profile</router-link>
                <router-link to="/users" class="block px-4 py-2 text-gray-200 hover:bg-gray-700">Users</router-link>
            </nav>
        </aside>

        <!-- Main Content -->
        <div class="flex-1 flex flex-col">
            <!-- Header -->
            <header class="flex justify-between items-center p-4 bg-white shadow-md">
                <div></div>
                <div class="flex items-center">
                    <span class="mr-4">Username</span>
                    <div class="relative">
                        <button @click="toggleDropdown" class="focus:outline-none">
                            <svg class="h-6 w-6 text-gray-700" fill="currentColor" viewBox="0 0 24 24">
                                <path
                                    d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm0 18c-4.418 0-8-3.582-8-8s3.582-8 8 8-3.582 8-8 8zm-1-11h2v6h-2zm0-4h2v2h-2z" />
                            </svg>
                        </button>
                        <div v-if="dropdownOpen"
                            class="absolute right-0 mt-2 w-48 bg-white border border-gray-200 rounded-md shadow-lg">
                            <a href="#" class="block px-4 py-2 text-gray-700 hover:bg-gray-100">Profile</a>
                            <a href="#" class="block px-4 py-2 text-gray-700 hover:bg-gray-100">Logout</a>
                        </div>
                    </div>
                </div>
            </header>

            <!-- Page Content -->
            <main class="flex-1 p-4 bg-gray-100">
                <router-view />
            </main>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            dropdownOpen: false,
            logo: require('@/assets/images/logo-no-background.png'),
        };
    },
    methods: {
        toggleDropdown() {
            this.dropdownOpen = !this.dropdownOpen;
        },
    },
};
</script>

<style scoped>
/* Add any custom styles if needed */
</style>