<template>
    <div>
        <h2 class="text-2xl font-bold mb-4">Users</h2>
        <p class="mb-4">List of all users in the system.</p>
        <div class="flex justify-between items-center mb-4">
            <button @click="addUser"
                class="ml-auto bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                Add User
            </button>
        </div>
        <div class="overflow-x-auto">
            <table class="min-w-full bg-white">
                <thead>
                    <tr>
                        <th class="py-2 px-4 border-b">No</th>
                        <th class="py-2 px-4 border-b">ID</th>
                        <th class="py-2 px-4 border-b">Name</th>
                        <th class="py-2 px-4 border-b">Status</th>
                        <th class="py-2 px-4 border-b">Email</th>
                        <th class="py-2 px-4 border-b">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(user, index) in users" :key="user.id">
                        <td class="py-2 px-4 border-b">{{ index + 1 }}</td>
                        <td class="py-2 px-4 border-b">{{ user.ID }}</td>
                        <td class="py-2 px-4 border-b">{{ user.Username }}</td>
                        <td class="py-2 px-4 border-b">{{ user.Status }}</td>
                        <td class="py-2 px-4 border-b">{{ user.Email }}</td>
                        <td class="py-2 px-4 border-b">
                            <button @click="editUser(user.ID)"
                                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                                Edit
                            </button>
                            <button @click="deleteUser(user.ID)"
                                class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    layout: 'admin',
    data() {
        return {
            users: []
        };
    },
    async mounted() {
        try {
            const { default: axios } = await import('axios');
            const response = await axios.get('http://localhost:9001/users');
            this.users = response.data;
            console.log('Users:', this.users);
        } catch (error) {
            console.error('Error fetching users:', error);
        }
    },
    methods: {
        addUser() {
            this.$router.push('/users/add');
        },
        editUser(id) {
            this.$router.push(`/users/${id}`);
        },
        async deleteUser(id) {
            try {
                const { default: axios } = await import('axios');
                await axios.delete(`http://localhost:9001/users/${id}`);
                this.users = this.users.filter(user => user.ID !== id);
            } catch (error) {
                console.error('Error deleting user:', error);
            }
        }
    }
}
</script>

<style scoped>
/* Add any custom styles if needed */
</style>