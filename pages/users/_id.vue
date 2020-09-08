<template>
    <section>
        <h1>{{myuser.name}}</h1>
        <h3>{{myuser.email}}</h3>
    </section>
</template>
<script>
export default {
    validate({params}) {
        return /^\d+$/.test(params.id)
    },
    async fetch({store}) {
        if (store.getters['users/users'].length === 0) {
            await store.dispatch('users/fetch')
        }
    },
    computed: {
        myuser() {
            const user_id = parseInt(this.$route.params.id)
            const myuser = this.$store.getters['users/user'](user_id)
            return myuser
        },
    },
}
</script>