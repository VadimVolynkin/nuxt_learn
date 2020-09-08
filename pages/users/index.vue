<template>
    <section>
        <h1>{{pageTitle}}</h1>
        <ul>
            <li v-for="user of users" :key="user.id">
                <a :href="'users/' + user.id" @click.prevent="openUser(user)">{{user.name}}</a> 
            </li>
        </ul>
    </section>
</template>
<script>
export default {
    async fetch({store}) {
        if (store.getters['users/users'].length === 0) {
            await store.dispatch('users/fetch')
        }
    },
    computed: {
        users() {
            return this.$store.getters['users/users']
        }
    },
    data: () => ({
        pageTitle: 'Users page'
    }),
    methods: {
        openUser(user){
            this.$router.push('/users/' + user.id)
        }
    }
}
</script>


// TODO https://www.youtube.com/watch?v=lm9olMCRCIc