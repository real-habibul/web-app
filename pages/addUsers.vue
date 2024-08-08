<template>
    <div>
        <h2 class="text-2xl font-bold mb-4">Add Users</h2>
        <p class="mb-4">Add new users in the system.</p>
        <div class="flex justify-between items-center mb-4">
            <button @click="backToUser"
                class="ml-auto bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                Back to Users
            </button>
        </div>
        <form @submit.prevent="submitForm" class="mb-4">
            <div class="mb-4">
                <label for="name" class="block text-gray-700">Name</label>
                <input v-model="form.name" type="text" id="name" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="email" class="block text-gray-700">Email</label>
                <input v-model="form.email" type="email" id="email" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="password" class="block text-gray-700">Password</label>
                <input v-model="form.password" type="password" id="password" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="first_name" class="block text-gray-700">First Name</label>
                <input v-model="form.first_name" type="text" id="first_name" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="last_name" class="block text-gray-700">Last Name</label>
                <input v-model="form.last_name" type="text" id="last_name" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <button type="submit" :disabled="loading" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                <span v-if="loading">Loading...</span>
                <span v-else>Submit</span>
            </button>
        </form>
    </div>
</template>

<script>
export default {
    layout: 'admin',
    data() {
        return {
            users: [],
            form: {
                name: '',
                email: '',
                first_name: '',
                last_name: ''
            },
            loading: false
        };
    },
    methods: {
        backToUser() {
            this.$router.push('/users');
        },
        async submitForm() {
            this.loading = true;
            try {
                const response = await fetch('http://localhost:9001/users', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.form)
                });
                if (response.ok) {
                    this.$router.push('/users');
                } else {
                    console.error('Failed to add user');
                }
            } catch (error) {
                console.error('Error:', error);
            } finally {
                this.loading = false;
            }
        }
    }
}
</script>

<style scoped>
/* Add any custom styles if needed */
</style>