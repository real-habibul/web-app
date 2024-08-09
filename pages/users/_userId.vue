<template>
    <div>
        <h2 class="text-2xl font-bold mb-4">Edit User</h2>
        <p class="mb-4">Edit user details in the system.</p>
        <div class="flex justify-between items-center mb-4">
            <button @click="backToUser"
                class="ml-auto bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                Back to Users
            </button>
        </div>
        <form @submit.prevent="submitForm" class="mb-4">
            <!-- {{ form }} -->
            <div class="mb-4">
                <label for="username" class="block text-gray-700">Username</label>
                <input v-model="form.Username" type="text" id="username" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="email" class="block text-gray-700">Email</label>
                <input v-model="form.Email" type="email" id="email" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="password" class="block text-gray-700">Password</label>
                <input v-model="form.Password" type="password" id="password" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="firstname" class="block text-gray-700">First Name</label>
                <input v-model="form.FirstName" type="text" id="firstname" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
            </div>
            <div class="mb-4">
                <label for="lastname" class="block text-gray-700">Last Name</label>
                <input v-model="form.LastName" type="text" id="lastname" class="mt-1 block w-full border-gray-300 rounded-md shadow-sm">
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
                username: '',
                email: '',
                password: '',
                firstname: '',
                lastname: ''
            },
            loading: false
        };
    },
    created() {
        this.fetchUser();
    },
    methods: {
        backToUser() {
            this.$router.push('/users');
        },
        async fetchUser() {
            const userId = this.$route.params.userId;
            try {
                const response = await fetch(`http://localhost:9001/users/${userId}`);
                if (response.ok) {
                    const user = await response.json();
                    this.form = user;
                    console.log('this.form:', this.form);
                } else {
                    console.error('Failed to fetch user');
                }
            } catch (error) {
                console.error('Error:', error);
            }
        },
        async submitForm() {
            this.loading = true;
            const userId = this.$route.params.userId;
            try {
                const response = await fetch(`http://localhost:9001/users/${userId}`, {
                    method: 'PUT',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.form)
                });
                if (response.ok) {
                    this.$router.push('/users');
                } else {
                    console.error('Failed to update user');
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